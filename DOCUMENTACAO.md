# CRIAPA Hub - Documentacao Tecnica do Site

**URL:** https://criapa.github.io/
**Repositorio:** https://github.com/criapa/criapa.github.io
**Email de contato:** criapa.contato@gmail.com
**Data da ultima atualizacao:** 11/06/2026

---

## 1. Estrutura de Arquivos

### Paginas principais (CRIAPA Hub)
| Arquivo | Linhas | Descricao |
|---------|--------|-----------|
| `index.html` | 1485 | Pagina principal (landing page) |
| `marca-mista-no-inpi.html` | 481 | Artigo: Marca Mista no INPI |
| `registro-marca-internacional.html` | 610 | Artigo: Registro de Marca Internacional |
| `propriedade-intelectual-startups.html` | 745 | Artigo: PI para Startups |
| `sucesso.html` | 28 | Pagina de confirmacao de envio |

### Paginas legado/outros projetos (nao fazem parte do CRIAPA Hub)
`aprese.html`, `detektai.html`, `i9nursing.html`, `incubatec.html`, `incubatecj.html`, `index2.html`, `regulai.html`, `regulai-a.html`, `regulai-orecamento.html`, `slidesincuba.html`, `vid.html`

---

## 2. Arquitetura do Sistema

### 2.1 Hosting
- **Plataforma:** GitHub Pages (static site)
- **Dominio:** criapa.github.io (GitHub Pages default)
- **Deploy:** Automatico via `git push` para branch `main`
- **Repositorio local:** `C:\Users\Pichau\criapa-repo\`
- **Workspace local:** `C:\Users\Pichau\criapahub-site\`

### 2.2 Stack Tecnologico
- **Frontend:** HTML5 + CSS3 + JavaScript vanilla (sem frameworks)
- **CSS:** Variaveis CSS custom properties (`:root`), Flexbox, Grid, animacoes CSS
- **JS:** Vanilla JS (ES6+), sem dependencias externas
- **Fontes:** Google Fonts (Raleway para headings, Inter para corpo)
- **Formulario:** FormSubmit.co (gratuito, ilimitado)
- **Imagens:** PNG/JPG locais no repositorio

### 2.3 Deploy Workflow
```bash
cd C:\Users\Pichau\criapa-repo
git add -A
git commit -m "descricao"
git push
```
O GitHub Pages faz deploy automatico. IMPORTANTE: nunca copiar workspace para repo cegamente — o repo tem arquivos unicos (madruga.png, trofeu, SVGs) que o workspace nao tem.

---

## 3. Design System

### 3.1 Paleta de Cores (CSS Variables)
```css
:root {
  --azul-900: #0A1B3A;    /* Fundo escuro principal */
  --azul-800: #0F2847;    /* Fundo secundario */
  --azul-700: #143A6B;
  --azul-600: #1E50A0;
  --azul-500: #269AB6;    /* Teal principal */
  --teal-500: #269AB6;    /* Cor primaria de acao */
  --teal-400: #38B6CE;    /* Teal hover */
  --verde-500: #00C48C;   /* Verde sucesso/check */
  --verde-600: #00A070;
  --ouro-500: #D4A843;    /* Dourado (labels, destaques) */
  --gold: #D4A843;
  --white: #FFFFFF;
  --gray-50: #F8FAFC;
  --gray-100: #F1F5F9;
  --gray-200: #E2E8F0;
  --gray-300: #CBD5E1;
  --gray-400: #94A3B8;
  --gray-500: #64748B;
  --gray-600: #475569;
  --gray-700: #334155;
  --gray-800: #1E293B;
  --gray-900: #0F172A;
  --heading: #1C3622;     /* Cor de titulos */
}
```

### 3.2 Tipografia
- **Headings:** Raleway (400, 500, 600, 700, 800, 900)
- **Corpo:** Inter (herdado do sistema)
- **Tamanhos:** Usa `clamp()` para responsividade

### 3.3 Espacamento e Layout
- **Max-width do container:** 1200px
- **Padding do container:** 0 24px
- **Border-radius:** 12px (padrao), 20px (lg), 28px (xl), 9999px (full/pill)
- **Transicoes:** `.3s cubic-bezier(.4,0,.2,1)`

### 3.4 Breakpoints
- **Desktop:** > 768px
- **Mobile:** <= 768px
- **Mobile small:** <= 480px
- **Tablet:** <= 900px

---

## 4. Componentes

### 4.1 Header

#### HTML (index.html, linhas 459-484)
```html
<header class="header" id="header">
  <div class="container">
    <a href="#hero" class="header-logo">
      <img src="criapa.png" alt="CRIAPA" class="logo-img">
      CRIAPA<span style="color:var(--teal-500)">Hub</span>
    </a>
    <nav class="header-nav">
      <a href="#beneficios">Beneficios</a>
      <a href="#como-funciona">Como Funciona</a>
      <a href="#faq">FAQ</a>
      <a href="#contato" class="btn btn-primary header-cta">Quero Consultar</a>
    </nav>
    <button class="header-toggle" id="headerToggle" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
  </div>
</header>
<div class="mobile-menu-backdrop" id="mobileBackdrop"></div>
<div class="mobile-menu" id="mobileMenu">
  <a href="#beneficios">Beneficios</a>
  <a href="#como-funciona">Como Funciona</a>
  <a href="#faq">FAQ</a>
  <a href="#contato" class="btn btn-primary btn-lg" style="width:100%;margin-top:16px">Quero Consultar</a>
</div>
```

#### CSS do Header (index.html, linhas 87-119)
```css
.header {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  padding: 16px 0; transition: var(--transition);
  /* No topo: transparente */
}
.header.scrolled {
  background: rgba(255,255,255,.96);
  backdrop-filter: blur(20px);
  box-shadow: 0 1px 0 var(--gray-200);
  padding: 10px 0;
}
.header-logo { color: var(--white); }           /* No topo: branco */
.header.scrolled .header-logo { color: var(--heading); } /* Scroll: escuro */
.header-nav a { color: rgba(255,255,255,.8); }  /* No topo: branco */
.header.scrolled .header-nav a { color: var(--gray-600); } /* Scroll: cinza */
.header-toggle span { background: var(--white); } /* No topo: branco */
.header.scrolled .header-toggle span { background: var(--azul-900); } /* Scroll: escuro */
```

#### JS do Scroll (index.html, linhas 1224-1227)
```javascript
const header = document.getElementById('header');
window.addEventListener('scroll', () => {
  header.classList.toggle('scrolled', window.scrollY > 50);
});
```

#### Logo
- **Arquivo:** `criapa.png` (36x36px, border-radius: 8px)
- **Substituiu:** `<div class="logo-mark">CR</div>` (quadrado com letras "CR")
- **Tamanho:** 36x36px, border-radius: 8px, object-fit: cover

#### Header nas paginas de artigos
- Links apontam para `https://criapa.github.io/#secao` (com dominio completo)
- Link "Quero Consultar" usa `href="#contato"` (abre modal na mesma pagina)
- CSS e JS copiados do index.html

### 4.2 Hero Section (index.html)

#### Frases do Hero (linhas 487-530)
```html
<h1>
  <span class="line1">Registro de Marca no INPI</span>
  <span class="line2">Sua ideia tem valor. Não deixe que uma marca desprotegida coloque tudo a perder</span>
</h1>
```

#### CTA Final
```html
<p>Registre sua marca de forma ágil e descomplicada</p>
```

### 4.3 Como Funciona (index.html, linhas ~670-695)

#### Frase de conclusao
```html
<p style="text-align:center"><strong>Pronto!</strong><br>Deixe a burocracia com a gente</p>
```
- "Pronto!" em cima (negrito)
- "Deixe a burocracia com a gente" embaixo

### 4.4 Formulario de Contato (Modal)

#### HTML do Formulario (index.html, linhas 1123-1270)
```html
<form id="consultForm" action="https://formsubmit.co/criapa.contato@gmail.com" method="POST">
  <input type="hidden" name="_subject" value="Nova consulta CRIAPA Hub">
  <input type="hidden" name="_captcha" value="false">
  <input type="hidden" name="_template" value="table">
  <input type="hidden" name="Marca" id="formMarca">
  <input type="hidden" name="Nome" id="formNome">
  <input type="hidden" name="Email" id="formEmail">
  <input type="hidden" name="WhatsApp" id="formWhatsapp">
  <input type="hidden" name="RedeSocial" id="formRedeSocial">
  <input type="hidden" name="Servico" id="formServico">
  <input type="hidden" name="Mensagem" id="formMensagem">
</form>
```

#### Campos do Modal (3 steps)

**Step 1 - Nome da marca:**
- `id="stepMarca"` - Input text
- Placeholder: "Qual o nome da marca que deseja consultar?"
- Icone: Lupa (SVG com class `modal-icon-search`, 18x18px)
- Validacao: minimo 2 caracteres

**Step 2 - Dados pessoais:**
- `id="stepNome"` - Input text - "Seu nome completo"
- `id="stepEmail"` - Input email - "Seu melhor e-mail"
- `id="stepWhatsapp"` - Input tel - "WhatsApp (com DDD)"
- `id="stepRedeSocial"` - Input text - "Rede social (Instagram, Facebook, etc.)"
- Icones: SVG com class `modal-field-icon` (18x18px)
- Validacao: nome >= 2 chars, email contem @, whatsapp >= 10 chars

**Step 3 - Servico e mensagem:**
- `id="stepServico"` - Select com opcoes:
  - "Qual serviço te interessa? (selecionar)" (disabled selected)
  - "Busca de Anterioridade"
  - "Registro de Marca"
  - "Monitoramento"
  - "Consultoria PI"
- `id="stepMensagem"` - Textarea - "Mensagem (opcional)"
- Icone: Globo (SVG com class `modal-icon-search`, 18x18px)

#### JS do Submit (index.html, linhas ~1395-1445)
```javascript
consultForm.addEventListener('submit', function(e) {
  e.preventDefault();
  // Copia valores dos campos visiveis para hidden inputs
  formMarca.value = stepMarca.value.trim();
  formNome.value = stepNome.value.trim();
  formEmail.value = stepEmail.value.trim();
  formWhatsapp.value = stepWhatsapp.value.trim();
  formRedeSocial.value = stepRedeSocial.value.trim();
  formServico.value = stepServico.value;
  formMensagem.value = stepMensagem.value.trim();

  // Loading state
  var submitBtn = document.getElementById('modalSubmit');
  var originalText = submitBtn.textContent;
  submitBtn.textContent = 'Enviando...';
  submitBtn.disabled = true;

  // Envia via fetch com URLSearchParams
  var data = new URLSearchParams();
  data.append('Marca', formMarca.value);
  data.append('Nome', formNome.value);
  data.append('Email', formEmail.value);
  data.append('WhatsApp', formWhatsapp.value);
  data.append('RedeSocial', formRedeSocial.value);
  data.append('Servico', formServico.value);
  data.append('Mensagem', formMensagem.value);
  data.append('_subject', 'Nova consulta CRIAPA Hub');
  data.append('_captcha', 'false');
  data.append('_template', 'table');

  fetch('https://formsubmit.co/criapa.contato@gmail.com', {
    method: 'POST',
    body: data,
    mode: 'no-cors'
  })
  .then(function() {
    consultForm.style.display = 'none';
    formSuccess.style.display = 'block';
  })
  .catch(function() {
    consultForm.style.display = 'none';
    formSuccess.style.display = 'block';
  })
  .finally(function() {
    submitBtn.textContent = originalText;
    submitBtn.disabled = false;
  });
});
```

#### Abertura do Modal
```javascript
document.querySelectorAll('a[href*="#contato"], .header-cta, .btn-primary, .article-cta a').forEach(btn => {
  btn.addEventListener('click', function(e) {
    const t = this.textContent.trim().toUpperCase();
    if (t.includes('CONSULTAR') || t.includes('REGISTRAR') || t.includes('VIABILIDADE') || t.includes('QUERO')) {
      e.preventDefault();
      openModal();
    }
  });
});
```
**Nota:** Usa `href*="#contato"` (contains) para capturar tanto `#contato` quanto `https://criapa.github.io/#contato`.

### 4.5 FormSubmit.co
- **URL:** https://formsubmit.co/criapa.contato@gmail.com
- **Limite:** Ilimitado (gratuito)
- **Formato de email:** Tabela (_template=table)
- **Captcha:** Desabilitado (_captcha=false)
- **Substituiu:** Formspree.io (que tinha limite de 50 emails/mes)

### 4.6 Pagina de Sucesso
- **Arquivo:** `sucesso.html`
- **URL:** https://criapa.github.io/sucesso.html
- **Conteudo:** Checkmark animado + "Consulta enviada com sucesso!" + CTA para voltar
- **Status:** Criada mas nao utilizada (formulario fica na mesma pagina)

---

## 5. Paginas de Artigos

### 5.1 Marca Mista no INPI
- **URL:** https://criapa.github.io/marca-mista-no-inpi.html
- **Linhas:** 481
- **Conteudo:** Tipos de marca, riscos da marca mista, estrategia de protecao em camadas

### 5.2 Registro de Marca Internacional
- **URL:** https://criapa.github.io/registro-marca-internacional.html
- **Linhas:** 610

### 5.3 Propriedade Intelectual para Startups
- **URL:** https://criapa.github.io/propriedade-intelectual-startups.html
- **Linhas:** 745

### Estrutura comum das paginas de artigos:
1. **Header** (igual ao index, com links para o index)
2. **Article Hero** (titulo, meta, label)
3. **Conteudo** (h2, h3, tabelas, listas)
4. **CTA Final** ("ABRIR CONSULTA DE VIABILIDADE")
5. **Navegacao** (Voltar / Proximo artigo)
6. **Footer** (servicos, institucional, contato)
7. **Modal de formulario** (identico ao index)

---

## 6. Regras e Convencoes

### 6.1 Aprovacoes
- **Padrao:** "Allow once" — cada acao precisa de aprovacao individual
- **Nunca:** Aprovar em batch ou auto-aprovar

### 6.2 CSS
- **Nao usar:** `text-align: justify` (usuario rejeitou)
- **Alinhamento:** Sempre left-aligned
- **Simbolos decorativos:** Grandes (12-18rem, 5-8% opacity)
- **Botoes nao-submit:** Usar `type="button"`
- **Mensagem de sucesso:** Div de sucesso FORA do `</form>`

### 6.3 Formulario
- **Nao redirecionar:** Tudo acontece na mesma pagina (index.html)
- **Metodo:** fetch com URLSearchParams e mode: 'no-cors'
- **Campos hidden:** Copiados dos campos visiveis via JS antes do submit
- **Validacao:** Step 1 (marca >= 2 chars), Step 2 (nome >= 2, email @, whatsapp >= 10)

### 6.4 Header
- **No topo:** Transparente, texto branco
- **Ao scroll (>50px):** Branco com blur, texto escuro
- **Logo:** criapa.png 36x36px, border-radius: 8px
- **Mobile:** Menu hamburger com 3 barrinhas

### 6.5 Git/Deploy
- **Repositorio local:** `C:\Users\Pichau\criapa-repo\`
- **Workspace:** `C:\Users\Pichau\criapahub-site\`
- **Nunca:** Copiar workspace para repo cegamente
- **Sempre:** Usar `git diff` antes de push
- **Branch:** main

---

## 7. Historico de Commits

```
e673eae Copia CSS header do index para paginas de artigos
1a46395 Adiciona efeito scroll no header das paginas de artigos
c46b278 Corrige seletor JS para abrir modal - href*=contato
7b68d6a Corrige submit form - fetch no-cors com URLSearchParams
e34736c Simplifica submit form - submit nativo com redirect
e0a55ff Corrige submit form para mobile - XMLHttpRequest POST
f6b181a Atualiza placeholder select: adiciona (selecionar)
5267826 Corrige placeholder do select de servico nas paginas de artigos
4307304 Corrige tamanho dos icones do formulario nas paginas de artigos
51f90c0 Troca logo CR pela criapa.png nas paginas de artigos
03075a0 Adiciona campo RedeSocial no form hidden e JS
f850aea Corrige ordem frase: Pronto! em cima
829297a Adiciona campo rede social no formulario de contato
66d9f81 Troca ordem frase: Deixe a burocracia com a gente / Pronto!
230dd28 Corrige flag formSubmitted - sucesso prematuro
d2593bc Corrige submit form - iframe target para mobile
599e7ae Corrige submit form para mobile (XMLHttpRequest)
6abac7d Troca Formspree por FormSubmit (ilimitado) + ajuste JS submit
03cc246 Troca logo CR pela logo CRIAPA oficial
555475c Add files via upload
```

---

## 8. Problemas Conhecidos e Solucoes

### 8.1 Formulario nao enviava no mobile
- **Causa:** FormSubmit bloqueia CORS de dispositivos mobile
- **Solucao:** fetch com URLSearchParams e mode: 'no-cors'
- **Tentativas anteriores:** XMLHttpRequest, iframe target, submit nativo

### 8.2 Header sempre branco nas paginas de artigos
- **Causa:** CSS do header tinha `background:rgba(255,255,255,.96)` fixo
- **Solucao:** Copiar CSS do index com `.header.scrolled` e JS do scroll

### 8.3 Modal nao abria no mobile menu
- **Causa:** Seletor JS `a[href="#contato"]` nao capturava links com dominio completo
- **Solucao:** Mudar para `a[href*="#contato"]` (contains)

### 8.4 Icones do formulario enormes
- **Causa:** CSS `.modal-icon-search` nao existia nas paginas de artigos
- **Solucao:** Adicionar CSS com `width:18px; height:18px`

### 8.5 Logo CR antiga nas paginas de artigos
- **Causa:** `<div class="logo-mark">CR</div>` ainda estava no HTML
- **Solucao:** Trocar por `<img src="criapa.png" class="logo-img">`

### 8.6 Rede social nao aparecia no email
- **Causa:** Faltava hidden input `formRedeSocial` e JS para copiar valor
- **Solucao:** Adicionar hidden input e `formRedeSocial.value = stepRedeSocial.value.trim()`

---

## 9. Contatos e Recursos

- **Email:** criapa.contato@gmail.com
- **GitHub:** https://github.com/criapa/criapa.github.io
- **Site:** https://criapa.github.io/
- **FormSubmit:** https://formsubmit.co/criapa.contato@gmail.com
- **Logo:** criapa.png (36x36px)
- **Usuario:** Hideo Silva (Pichau) — PhD student RENORBIO/UFRPE
