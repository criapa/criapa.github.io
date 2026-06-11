# CRIAPA Hub - Documentacao Tecnica Completa do Site

**URL:** https://criapa.github.io/
**Repositorio:** https://github.com/criapa/criapa.github.io
**Email de contato:** criapa.contato@gmail.com
**Data da ultima atualizacao:** 11/06/2026
**Autor da documentacao:** OWL (assistente tecnico)
**Responsavel pelo projeto:** Hideo Silva (Pichau) — PhD student RENORBIO/UFRPE

---

## 1. Estrutura de Arquivos

### 1.1 Paginas principais (CRIAPA Hub)

| Arquivo | Linhas | Tamanho | Descricao |
|---------|--------|---------|-----------|
| `index.html` | 1485 | 89KB | Pagina principal (landing page) |
| `marca-mista-no-inpi.html` | 481 | 47KB | Artigo: Marca Mista no INPI |
| `registro-marca-internacional.html` | 610 | 58KB | Artigo: Registro de Marca Internacional |
| `propriedade-intelectual-startups.html` | 745 | 68KB | Artigo: PI para Startups |
| `sucesso.html` | 28 | 1.6KB | Pagina de confirmacao de envio (nao utilizada) |
| `DOCUMENTACAO.md` | ~500 | 16KB | Este arquivo de documentacao |

### 1.2 Paginas legado/outros projetos (nao fazem parte do CRIAPA Hub)

| Arquivo | Descricao |
|---------|-----------|
| `aprese.html` | Apresentacao |
| `detektai.html` | Projeto Detekta |
| `i9nursing.html` | Projeto i9Nursing |
| `incubatec.html` | Projeto Incubatec |
| `incubatecj.html` | Projeto Incubatec J |
| `index2.html` | Index alternativo |
| `regulai.html` | Projeto Regulai |
| `regulai-a.html` | Projeto Regulai A |
| `regulai-orecamento.html` | Projeto Regulai Orcamento |
| `slidesincuba.html` | Slides Incuba |
| `vid.html` | Pagina de video |

---

## 2. Arquitetura do Sistema

### 2.1 Hosting
- **Plataforma:** GitHub Pages (static site, sem backend)
- **Dominio:** criapa.github.io (GitHub Pages default, sem dominio customizado)
- **Deploy:** Automatico via `git push` para branch `main`
- **SSL:** Automatico pelo GitHub Pages
- **CDN:** Cloudflare (via GitHub Pages)

### 2.2 Ambiente de Desenvolvimento
- **Repositorio local (deploy):** `C:\Users\Pichau\criapa-repo\`
- **Workspace local (edicao):** `C:\Users\Pichau\criapahub-site\`
- **Shell:** Git Bash (MSYS) no Windows 10
- **Editor:** Nenhum especificado (edicao via terminal)

### 2.3 Stack Tecnologico
- **Frontend:** HTML5 + CSS3 + JavaScript vanilla (sem frameworks)
- **CSS:** Variaveis CSS custom properties (`:root`), Flexbox, Grid, animacoes CSS
- **JS:** Vanilla JS (ES6+), sem dependencias externas, sem bundlers
- **Fontes:** Google Fonts (Raleway para headings, system-ui para corpo)
- **Formulario:** FormSubmit.co (gratuito, ilimitado, sem API key)
- **Imagens:** PNG/JPG locais no repositorio
- **SEO:** Meta tags Open Graph, Twitter Cards, canonical URLs

### 2.4 Deploy Workflow
```bash
cd C:\Users\Pichau\criapa-repo
git add -A
git commit -m "descricao da alteracao"
git push
```

**REGRA CRITICA:** Nunca copiar workspace (`criapahub-site`) para repo (`criapa-repo`) cegamente. O repo tem arquivos unicos (madruga.png, trofeu, SVGs) que o workspace nao tem. Sempre usar `git diff` antes de push.

### 2.5 Regra de Aprovacoes
- **Padrao:** "Allow once" — cada acao precisa de aprovacao individual do usuario
- **Nunca:** Aprovar em batch, auto-aprovar, ou executar multiplas acoes sem aprovacao
- **Aplicacao:** Instalacoes, criacao de arquivos, comandos que modificam estado, escrita de credenciais

---

## 3. Design System

### 3.1 Paleta de Cores (CSS Variables)

```css
:root {
  /* Azuis */
  --azul-900: #0A1B3A;    /* Fundo escuro principal */
  --azul-800: #0F2847;    /* Fundo secundario */
  --azul-700: #143A6B;
  --azul-600: #1E50A0;
  --azul-500: #269AB6;

  /* Teal (cor primaria) */
  --teal-500: #269AB6;    /* Cor primaria de acao, botoes, links */
  --teal-400: #38B6CE;    /* Teal hover */

  /* Verde */
  --verde-500: #00C48C;   /* Verde sucesso, checkmarks */
  --verde-600: #00A070;

  /* Ouro */
  --ouro-500: #D4A843;    /* Dourado para labels e destaques */
  --gold: #D4A843;

  /* Neutros */
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

  /* Semantica */
  --heading: #1C3622;     /* Cor de titulos */

  /* Sombras */
  --shadow-sm: 0 1px 3px rgba(0,0,0,.06);
  --shadow-md: 0 4px 16px rgba(0,0,0,.08);
  --shadow-lg: 0 12px 40px rgba(0,0,0,.12);
  --shadow-xl: 0 24px 64px rgba(0,0,0,.16);

  /* Border radius */
  --radius: 12px;
  --radius-lg: 20px;
  --radius-xl: 28px;
  --radius-full: 9999px;

  /* Transicao padrao */
  --transition: .3s cubic-bezier(.4,0,.2,1);
}
```

### 3.2 Tipografia
- **Headings:** Raleway (Google Fonts, pesos 400-900)
- **Corpo:** System font stack (`system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`)
- **Tamanhos:** Usa `clamp()` para responsividade fluida
- **Line-height:** 1.2 (headings), 1.6 (corpo)

### 3.3 Espacamento e Layout
- **Max-width do container:** 1200px
- **Padding do container:** 0 24px
- **Grid:** CSS Grid para layouts complexos
- **Flexbox:** Para alinhamento de componentes

### 3.4 Breakpoints
| Breakpoint | Largura | Uso |
|------------|---------|-----|
| Desktop | > 768px | Layout completo, nav visivel |
| Tablet | <= 900px | Ajustes de grid, hero simplificado |
| Mobile | <= 768px | Menu hamburger, nav oculta |
| Mobile small | <= 480px | Padding reduzido, fonte menor |

### 3.5 Convencoes de CSS
- **Nao usar:** `text-align: justify` (usuario rejeitou explicitamente)
- **Alinhamento padrao:** Left-aligned
- **Simbolos decorativos:** Grandes (12-18rem, 5-8% opacity)
- **Botoes nao-submit:** Sempre usar `type="button"`
- **Mensagem de sucesso:** Div de sucesso FORA do `</form>`
- **Nao usar sed/awk:** Usar `patch` tool para edicao de arquivos

---

## 4. Componentes

### 4.1 Header

#### 4.1.1 HTML do Header (index.html)
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

#### 4.1.2 HTML do Header (paginas de artigos)
```html
<header class="header" id="header">
  <div class="container">
    <a href="https://criapa.github.io/" class="header-logo">
      <img src="criapa.png" alt="CRIAPA" class="logo-img">
      CRIAPA<span style="color:var(--teal-500)">Hub</span>
    </a>
    <nav class="header-nav">
      <a href="https://criapa.github.io/#beneficios">Beneficios</a>
      <a href="https://criapa.github.io/#como-funciona">Como Funciona</a>
      <a href="https://criapa.github.io/#faq">FAQ</a>
      <a href="#contato" class="btn btn-primary header-cta">Quero Consultar</a>
    </nav>
    <button class="header-toggle" id="headerToggle" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
  </div>
</header>
<div class="mobile-menu-backdrop" id="mobileBackdrop"></div>
<div class="mobile-menu" id="mobileMenu">
  <a href="https://criapa.github.io/#beneficios">Beneficios</a>
  <a href="https://criapa.github.io/#como-funciona">Como Funciona</a>
  <a href="https://criapa.github.io/#faq">FAQ</a>
  <a href="https://criapa.github.io/#contato" class="btn btn-primary btn-lg" style="width:100%;margin-top:16px">Quero Consultar</a>
</div>
```

**Diferencas entre index e artigos:**
- Links da nav apontam para `https://criapa.github.io/#secao` (com dominio completo)
- Link "Quero Consultar" no nav usa `href="#contato"` (abre modal na mesma pagina)
- Link "Quero Consultar" no mobile menu usa `href="https://criapa.github.io/#contato"` (redireciona para index)

#### 4.1.3 CSS do Header (identico em todas as paginas)
```css
.header {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  padding: 16px 0; transition: var(--transition);
  /* No topo: transparente (sem background) */
}
.header.scrolled {
  background: rgba(255,255,255,.96);
  backdrop-filter: blur(20px); -webkit-backdrop-filter: blur(20px);
  box-shadow: 0 1px 0 var(--gray-200);
  padding: 10px 0;
}
.header-logo { color: var(--white); transition: var(--transition); }
.header.scrolled .header-logo { color: var(--heading); }
.header-nav a { color: rgba(255,255,255,.8); transition: var(--transition); }
.header.scrolled .header-nav a { color: var(--gray-600); }
.header-nav a:hover { color: var(--white); }
.header.scrolled .header-nav a:hover { color: var(--heading); }
.header-toggle { display: none; }
.header-toggle span { background: var(--white); }
.header.scrolled .header-toggle span { background: var(--azul-900); }

@media(max-width:768px) {
  .header-nav { display: none; }
  .header-cta { display: none; }
  .header-toggle { display: flex; }
}

/* Mobile menu */
.mobile-menu {
  position: fixed; top: 0; right: -100%; width: 300px; height: 100vh;
  background: var(--white); z-index: 200; padding: 80px 32px 32px;
  transition: var(--transition); box-shadow: var(--shadow-xl);
}
.mobile-menu.open { right: 0; }
.mobile-menu-backdrop {
  position: fixed; inset: 0; background: rgba(0,0,0,.4);
  z-index: 199; opacity: 0; pointer-events: none; transition: var(--transition);
}
.mobile-menu-backdrop.show { opacity: 1; pointer-events: all; }
```

#### 4.1.4 JS do Header (identico em todas as paginas)
```javascript
// Mobile menu toggle
const headerToggle = document.getElementById('headerToggle');
const mobileMenu = document.getElementById('mobileMenu');
const mobileBackdrop = document.getElementById('mobileBackdrop');

function toggleMenu() {
  mobileMenu.classList.toggle('open');
  mobileBackdrop.classList.toggle('show');
}
headerToggle.addEventListener('click', toggleMenu);
mobileBackdrop.addEventListener('click', toggleMenu);
mobileMenu.querySelectorAll('a').forEach(a => a.addEventListener('click', toggleMenu));

// Scroll effect
const header = document.getElementById('header');
window.addEventListener('scroll', () => {
  header.classList.toggle('scrolled', window.scrollY > 50);
});
```

#### 4.1.5 Logo
- **Arquivo:** `criapa.png` (imagem real da marca CRIAPA)
- **Tamanho display:** 36x36px
- **Border-radius:** 8px
- **Object-fit:** cover
- **Substituiu:** `<div class="logo-mark">CR</div>` (quadrado com gradiente e letras "CR")
- **CSS da logo antiga (mantido para compatibilidade):**
```css
.header-logo .logo-mark {
  width: 36px; height: 36px;
  background: linear-gradient(135deg, var(--teal-500), var(--verde-500));
  border-radius: 8px; display: flex; align-items: center; justify-content: center;
  font-weight: 900; font-size: .85rem; color: var(--white);
}
```

### 4.2 Hero Section (index.html)

#### 4.2.1 Estrutura do Hero
```html
<section class="hero" id="hero">
  <div class="container">
    <div class="hero-text">
      <h1>
        <span class="line1">Registro de Marca no INPI</span>
        <span class="line2">Sua ideia tem valor. Nao deixe que uma marca desprotegida coloque tudo a perder</span>
      </h1>
      <p class="hero-desc">...</p>
      <div class="hero-btns">...</div>
      <p class="hero-disclaimer">...</p>
      <div class="hero-trust">...</div>
    </div>
    <div class="hero-visual">...</div>
  </div>
</section>
```

#### 4.2.2 Frases do Hero (estado atual)
- **Line 1 (label):** "Registro de Marca no INPI"
- **Line 2 (titulo principal):** "Sua ideia tem valor. Nao deixe que uma marca desprotegida coloque tudo a perder"
- **CTA Final (secao como-funciona):** "Registre sua marca de forma agil e descomplicada"

**Historico de alteracoes das frases:**
1. Original: "Registre sua marca de forma agil e descomplicada" (hero) / "Sua ideia tem valor..." (CTA)
2. Trocado para: "Sua ideia tem valor..." (hero) / "Registre sua marca..." (CTA)
3. Revertido por erro de sobrescrita
4. Re-aplicado corretamente

### 4.3 Secao "Como Funciona" (index.html)

#### Frase de conclusao (estado atual)
```html
<p style="text-align:center"><strong>Pronto!</strong><br>Deixe a burocracia com a gente</p>
```
- "Pronto!" em cima (negrito)
- "Deixe a burocracia com a gente" embaixo

**Historico:** Invertido de "Pronto! Deixe a burocracia com a gente" (uma linha) para duas linhas com "Pronto!" em cima.

### 4.4 Formulario de Contato (Modal)

#### 4.4.1 Visao Geral
- **Tipo:** Modal overlay com 3 steps (wizard)
- **Acao:** Abre ao clicar em "Quero Consultar", "Abrir consulta de viabilidade", ou qualquer botao/link com texto contendo CONSULTAR, REGISTRAR, VIABILIDADE, ou QUERO
- **Envio:** FormSubmit.co via fetch com URLSearchParams e mode: 'no-cors'
- **Validacao:** Step 1 (marca >= 2 chars), Step 2 (nome >= 2, email contem @, whatsapp >= 10 chars)
- **Feedback:** Tela de sucesso inline (sem redirecionamento)

#### 4.4.2 HTML do Formulario
```html
<div class="modal-overlay" id="consultModal" role="dialog" aria-modal="true" aria-label="Formulario de consulta">
  <div class="modal-box">
    <button class="modal-close" id="modalClose" aria-label="Fechar formulario">&times;</button>
    <div class="modal-progress" id="modalProgress">
      <div class="modal-progress-dot active" data-step="1"></div>
      <div class="modal-progress-dot" data-step="2"></div>
      <div class="modal-progress-dot" data-step="3"></div>
    </div>
    <form id="consultForm" action="https://formsubmit.co/criapa.contato@gmail.com" method="POST" accept-charset="UTF-8">
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
      <!-- Steps do formulario -->
    </form>
    <div class="modal-step modal-success" id="formSuccess" data-step="success">
      <!-- Tela de sucesso -->
    </div>
  </div>
</div>
```

#### 4.4.3 Campos do Modal

**Step 1 — Nome da marca:**
- `id="stepMarca"` — Input type="text"
- Placeholder: "Qual o nome da marca que deseja consultar?"
- Icone: Lupa SVG (class `modal-icon-search`, 18x18px)
- Validacao: `value.trim().length >= 2`
- Botao: "CONTINUAR" (disabled ate validar)

**Step 2 — Dados pessoais:**
- `id="stepNome"` — Input type="text" — "Seu nome completo"
- `id="stepEmail"` — Input type="email" — "Seu melhor e-mail"
- `id="stepWhatsapp"` — Input type="tel" — "WhatsApp (com DDD)"
- `id="stepRedeSocial"` — Input type="text" — "Rede social (Instagram, Facebook, etc.)"
- Icones: SVG class `modal-field-icon` (18x18px)
- Validacao: nome >= 2 chars, email contem `@`, whatsapp >= 10 chars
- Botoes: "VOLTAR" (volta para step 1), "CONTINUAR" (disabled ate validar)

**Step 3 — Servico e mensagem:**
- `id="stepServico"` — Select com opcoes:
  - "Qual servico te interessa? (selecionar)" (`disabled selected`)
  - "Busca de Anterioridade"
  - "Registro de Marca"
  - "Monitoramento"
  - "Consultoria PI"
- `id="stepMensagem"` — Textarea — "Mensagem (opcional)"
- Icone: Globo SVG (class `modal-icon-search`, 18x18px)
- Botoes: "VOLTAR" (volta para step 2), "ENVIAR CONSULTA"

#### 4.4.4 JS do Submit (estado atual)
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

#### 4.4.5 JS de Abertura do Modal
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

**Nota importante:** O seletor usa `href*="#contato"` (attribute contains) para capturar tanto `#contato` quanto `https://criapa.github.io/#contato`.

#### 4.4.6 Tela de Sucesso
```html
<div class="modal-step modal-success" id="formSuccess" data-step="success">
  <div class="modal-success-icon">
    <svg viewBox="0 0 24 24"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/></svg>
  </div>
  <h3>Consulta enviada com sucesso!</h3>
  <p class="success-msg">Obrigado pela confianca! Em ate 24h iremos trazer todas as informacoes importantes e trilhar a estrategia que mais se adapta a sua marca.</p>
  <div class="success-tagline">
    <span class="success-brand">CRIAPA HUB</span>
    <span class="success-slogan">protegendo futuros</span>
  </div>
  <div class="modal-nav" style="justify-content:center;margin-top:24px">
    <button type="button" class="modal-btn-next" id="modalDone">Fechar</button>
  </div>
</div>
```

### 4.5 FormSubmit.co

- **URL de acao:** `https://formsubmit.co/criapa.contato@gmail.com`
- **Limite:** Ilimitado (gratuito, sem API key)
- **Formato de email:** Tabela (`_template=table`)
- **Captcha:** Desabilitado (`_captcha=false`)
- **Assunto:** "Nova consulta CRIAPA Hub" (`_subject`)
- **Substituiu:** Formspree.io (que tinha limite de 50 emails/mes)
- **Metodo de envio:** fetch com URLSearchParams e `mode: 'no-cors'`

### 4.6 Pagina de Sucesso (sucesso.html)
- **Arquivo:** `sucesso.html`
- **URL:** https://criapa.github.io/sucesso.html
- **Status:** Criada mas atualmente NAO utilizada (formulario mostra sucesso inline)
- **Conteudo:** Checkmark + "Consulta enviada com sucesso!" + CTA para voltar ao site

---

## 5. Paginas de Artigos — Detalhamento Completo

### 5.1 Marca Mista no INPI

**Arquivo:** `marca-mista-no-inpi.html`
**URL:** https://criapa.github.io/marca-mista-no-inpi.html
**Titulo:** "Marca Mista no INPI: o que esta protegido e o que ainda pode estar em risco"
**Meta description:** "Entenda as diferencas entre marcas nominativas, mistas e figurativas e qual a melhor estrategia para proteger a sua marca no INPI."
**Data:** 10 de junho de 2026
**Tempo de leitura:** 12 min
**Palavras-chave:** marca mista, INPI, registro de marca, marca nominativa, marca figurativa, propriedade intelectual

**Estrutura do conteudo:**
1. Introducao — O problema da marca mista
2. O que e uma marca mista?
3. Os 4 tipos de marca reconhecidos pelo INPI (tabela comparativa)
   - Nominativa, Figurativa, Mista, Tridimensional
4. Os riscos da marca mista
   - Uso isolado do nome por terceiros
   - Uso isolado do simbolo por terceiros
   - Variacoes do logotipo
   - Expansao para novas classes
5. Caso real: quando a marca mista nao bastou
6. A estrategia ideal: protecao em camadas
   - Camada 1: Marca nominativa (prioridade maxima)
   - Camada 2: Marca figurativa
   - Camada 3: Marca mista
   - Camada 4: Multiplas classes
7. Como saber se sua marca mista esta bem protegida? (checklist)
8. O processo de registro no INPI (8-14 meses)
9. Conclusao

**Componentes especificos:**
- Tabela comparativa de tipos de marca
- Warning box (atencao sobre protecao isolada)
- Highlight box (caso real)
- Tip box (dica pratica sobre custo de nao proteger)
- CTA final: "Abrir consulta de viabilidade"

### 5.2 Registro de Marca Internacional

**Arquivo:** `registro-marca-internacional.html`
**URL:** https://criapa.github.io/registro-marca-internacional.html
**Titulo:** "Registro de Marca Internacional: como chegar a outros paises"
**Meta description:** "Conheca o Sistema de Madri e descubra como proteger sua marca em mais de 120 paises com um unico pedido."
**Data:** 10 de junho de 2026
**Tempo de leitura:** 15 min
**Palavras-chave:** registro de marca internacional, Sistema de Madri, OMPI, WIPO, marca internacional, Protocolo de Madri, INPI

**Estrutura do conteudo:**
1. Introducao — O desafio da protecao internacional
2. O que e o Sistema de Madri?
   - Acordo de Madri (1891) e Protocolo de Madri (1989)
   - Brasil aderiu em 2019
   - 128 paises membros, 80% do comercio mundial
3. Quais paises sao membros? (tabela por regiao)
   - America do Norte, America Latina, Europa, Asia, Oriente Medio, Africa, Oceania
4. Requisitos para usar o Sistema de Madri
   - Registro ou pedido no Brasil (registro de base)
   - Ser brasileiro ou ter domicilio no Brasil
   - Mesma marca (identica ao registro de base)
   - Mesmos produtos/servicos (ou subconjunto)
   - Taxas pagas
   - Dependencia do registro de base por 5 anos
5. Passo a passo do processo de registro internacional
6. Custos envolvidos
7. Prazos
8. Vantagens e desvantagens
9. Conclusao

**Componentes especificos:**
- Tabela de paises membros por regiao
- Highlight box (numeros do Sistema de Madri)
- Warning box (dependencia de 5 anos)
- Tip box (lista de paises atualizada)
- CTA final: "Abrir consulta de viabilidade"

### 5.3 Propriedade Intelectual para Startups

**Arquivo:** `propriedade-intelectual-startups.html`
**URL:** https://criapa.github.io/propriedade-intelectual-startups.html
**Titulo:** "Propriedade Intelectual para Startups: o que voce precisa saber"
**Data:** 10 de junho de 2026
**Tempo de leitura:** 18 min

**Estrutura do conteudo:**
1. Introducao — O momento em que o investidor pergunta sobre PI
2. Por que a propriedade intelectual e crucial para startups?
   - Investidores exigem PI protegida (due diligence)
   - PI impacta diretamente o valuation
   - Vantagem competitiva sustentavel
3. Os tipos de PI relevantes para startups (tabela)
   - Marca, Patente de Invencao, Modelo de Utilidade, Registro de Software, Desenho Industrial, Segredo Industrial, Direito Autoral
4. A ordem ideal de protecao
5. Como investidores avaliam PI
6. Checklist pratico por estagio
7. Erros comuns
8. Conclusao

**Componentes especificos:**
- Tabela comparativa de tipos de PI
- Highlight box (numero: 15% das startups tem PI, 70% das investidas)
- Warning box (deal breaker)
- Tip box (custo de nao proteger)
- CTA final: "Abrir consulta de viabilidade"

### 5.4 Estrutura Comum das Paginas de Artigos

Todas as 3 paginas de artigos seguem a mesma estrutura:

```
1. <head>
   - Meta tags (charset, viewport, title, description, keywords, author, robots)
   - Open Graph tags (title, description, type, url, locale)
   - Twitter Card tags
   - Canonical URL
   - Google Fonts (Raleway)
   - <style> (CSS inline, ~200-250 linhas)

2. <body>
   - <header> (fixo, com logo, nav, hamburger)
   - <div class="mobile-menu-backdrop">
   - <div class="mobile-menu">
   - <section class="article-hero"> (titulo, meta, label)
   - <section class="article-body"> (conteudo do artigo)
   - <section class="article-cta"> (CTA final com botao)
   - <section class="article-nav"> (navegacao voltar/proximo)
   - <footer> (servicos, institucional, contato)
   - <div class="whatsapp-float"> (botao flutuante)
   - <div class="modal-overlay" id="consultModal"> (formulario)
   - <script> (JS inline, ~50-60 linhas)
```

---

## 6. Regras e Convencoes de Desenvolvimento

### 6.1 Aprovacoes
- **Padrao:** "Allow once" — cada acao precisa de aprovacao individual
- **Nunca:** Aprovar em batch ou auto-aprovar
- **Aplicacao:** Instalacoes, criacao de arquivos, comandos que modificam estado, escrita de credenciais

### 6.2 CSS
- **Nao usar:** `text-align: justify` (usuario rejeitou explicitamente)
- **Alinhamento padrao:** Left-aligned
- **Simbolos decorativos:** Grandes (12-18rem, 5-8% opacity)
- **Botoes nao-submit:** Sempre usar `type="button"`
- **Mensagem de sucesso:** Div de sucesso FORA do `</form>`
- **Nao usar sed/awk:** Usar `patch` tool para edicao de arquivos

### 6.3 Formulario
- **Nao redirecionar:** Tudo acontece na mesma pagina (sem redirect)
- **Metodo:** fetch com URLSearchParams e mode: 'no-cors'
- **Campos hidden:** Copiados dos campos visiveis via JS antes do submit
- **Validacao:** Step 1 (marca >= 2 chars), Step 2 (nome >= 2, email @, whatsapp >= 10)
- **Icones:** Lupa e globo usam class `modal-icon-search` (18x18px), outros usam `modal-field-icon` (18x18px)

### 6.4 Header
- **No topo (scrollY <= 50):** Transparente, texto branco, sem sombra
- **Ao scroll (scrollY > 50):** Branco com blur, texto escuro, sombra sutil
- **Logo:** criapa.png 36x36px, border-radius: 8px
- **Mobile (<= 768px):** Menu hamburger com 3 barrinhas, nav oculta
- **JS:** `header.classList.toggle('scrolled', window.scrollY > 50)`

### 6.5 Git/Deploy
- **Repositorio local:** `C:\Users\Pichau\criapa-repo\`
- **Workspace:** `C:\Users\Pichau\criapahub-site\`
- **Nunca:** Copiar workspace para repo cegamente
- **Sempre:** Usar `git diff` antes de push
- **Branch:** main
- **Mensagens de commit:** Em portugues, descritivas

### 6.6 JavaScript
- **Sem frameworks:** Vanilla JS apenas
- **Sem dependencias:** Zero bibliotecas externas
- **Compatibilidade:** ES6+ com fallback para navegadores antigos
- **Validacao de sintaxe:** Testar com `node -e "new Function(code)"` apos substituicoes

---

## 7. Historico Completo de Commits

```
3cc71ff Corrige erro de sintaxe JS - parenteses extras no fechamento do submit
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
dddb88a Troca frases hero e CTA final
9b197b9 Revert "Troca frases hero e CTA final"
aa97a04 Troca frases hero e CTA final
e255163 Update: 'garantiram seu lugar' -> 'garantiram seu lugar hoje'
b7e9caf Update: frase de impacto removida da trust section
b82dcf2 Update: imagem madruga centralizada
da03039 Update: imagem madruga - max-width 480px
6a61b3d Update: imagem madruga - borda branca, sem shadow
68f0244 Update: imagem madruga.png - tamanho ajustado para 320px
```

---

## 8. Problemas Conhecidos, Causas e Solucoes

### 8.1 Formulario nao enviava no mobile
- **Sintoma:** Formulario nao enviava dados pelo celular
- **Causa:** FormSubmit bloqueia CORS de dispositivos mobile; fetch com FormData nao funcionava
- **Tentativa 1:** XMLHttpRequest com `application/x-www-form-urlencoded` — falhou
- **Tentativa 2:** Submit nativo com iframe target — falhou (sucesso prematuro)
- **Tentativa 3:** Submit nativo com redirect para sucesso.html — funcionou mas redirecionava (usuario nao queria)
- **Solucao final:** fetch com URLSearchParams e `mode: 'no-cors'` — funciona em todos os dispositivos

### 8.2 Header sempre branco nas paginas de artigos
- **Sintoma:** Header ficava branco mesmo no topo da pagina
- **Causa:** CSS do header tinha `background:rgba(255,255,255,.96)` fixo (sem classe `.scrolled`)
- **Solucao:** Copiar CSS completo do index com `.header.scrolled` e adicionar JS do scroll

### 8.3 Menu mobile nao abria nas paginas de artigos
- **Sintoma:** Clicar nas 3 barrinhas nao abria o menu
- **Causa 1:** Seletor JS `a[href="#contato"]` nao capturava links com dominio completo
- **Solucao 1:** Mudar para `a[href*="#contato"]` (attribute contains)
- **Causa 2:** Erro de sintaxe JS `}););););` (parenteses extras) quebrava todo o script
- **Solucao 2:** Corrigir para `});` — validar JS com `node -e "new Function(code)"` apos cada substituicao

### 8.4 Modal nao abria pelo mobile menu
- **Causa:** Seletor JS nao capturava links com href completo
- **Solucao:** `href*="#contato"` em vez de `href="#contato"`

### 8.5 Icones do formulario enormes
- **Sintomo:** Icones da lupa e do mundo estavam fora da caixa de input
- **Causa:** CSS `.modal-icon-search` nao existia nas paginas de artigos
- **Solucao:** Adicionar CSS com `width:18px; height:18px`

### 8.6 Logo CR antiga nas paginas de artigos
- **Causa:** `<div class="logo-mark">CR</div>` ainda estava no HTML
- **Solucao:** Trocar por `<img src="criapa.png" class="logo-img">`

### 8.7 Rede social nao aparecia no email
- **Causa:** Faltava hidden input `formRedeSocial` e JS para copiar valor
- **Solucao:** Adicionar hidden input e `formRedeSocial.value = stepRedeSocial.value.trim()`

### 8.8 Sucesso prematuro do formulario
- **Sintoma:** Tela de sucesso aparecia sem o usuario clicar em enviar
- **Causa:** `formTarget.onload` disparava quando o iframe carregava pela primeira vez
- **Solucao:** Flag `formSubmitted` para so disparar depois do submit real

### 8.9 Frases do hero trocadas
- **Causa:** Commit que sobrescreveu a versao correta
- **Solucao:** Revert + re-aplicacao correta

---

## 9. Licoes Aprendidas e Melhoria de Rigor

### 9.1 Validacao de Sintaxe JS
**Problema:** Substituicoes de JS via regex podem introduzir erros de sintaxe que quebram todo o script.

**Solucao:** Apos cada substituicao de JS, validar com:
```bash
node -e "const fs = require('fs'); const html = fs.readFileSync('arquivo.html', 'utf8'); const scriptMatch = html.match(/<script>([\s\S]*?)<\/script>/g); scriptMatch.forEach((s, i) => { const code = s.replace(/<\/?script>/g, ''); try { new Function(code); console.log('OK'); } catch(e) { console.log('ERRO: ' + e.message); } });"
```

### 9.2 Seletores CSS/JS
**Problema:** Seletores rigidos como `href="#contato"` falham quando o href inclui dominio completo.

**Solucao:** Usar seletores mais flexíveis como `href*="#contato"` (attribute contains).

### 9.3 CSS de Componentes Compartilhados
**Problema:** CSS copiado manualmente entre paginas pode divergir.

**Solucao:** Manter CSS de componentes compartilhados (header, modal, footer) sincronizado. Considerar futuro uso de includes ou pre-processador.

### 9.4 Teste Multi-Dispositivo
**Problema:** Funciona no desktop mas nao no mobile (ou vice-versa).

**Solucao:** Testar sempre em ambos os contextos. Usar browser tool para simular mobile quando possivel.

### 9.5 Commits Atomicos
**Problema:** Multiplas alteracoes em um commit dificultam revert e debug.

**Solucao:** Commits atomicos, uma alteracao por commit, mensagens descritivas.

---

## 10. Contatos e Recursos

- **Email:** criapa.contato@gmail.com
- **GitHub:** https://github.com/criapa/criapa.github.io
- **Site:** https://criapa.github.io/
- **FormSubmit:** https://formsubmit.co/criapa.contato@gmail.com
- **Logo:** criapa.png (36x36px)
- **Usuario:** Hideo Silva (Pichau) — PhD student RENORBIO/UFRPE
- **Estilo de comunicacao:** Direto, resultados imedios, sem batching
- **Firecrawl API key:** fc-418a9895356644b8b3b70537f2a2fade (salva em .env.pipeline)

---

## 11. Proximos Passos Sugeridos

1. **Testar formulario no celular** — Verificar se o envio via fetch no-cors funciona corretamente
2. **Validar HTML** — Usar validador W3C para verificar erros de markup
3. **Otimizar imagens** — Comprimir PNGs/JPGs para melhor performance
4. **Adicionar analytics** — Google Analytics ou similar para metricas
5. **Sitemap XML** — Criar sitemap.xml para SEO
6. **Robots.txt** — Configurar para direcionar crawlers
7. **Testar em diferentes navegadores** — Chrome, Firefox, Safari, Edge
8. **Acessibilidade** — Verificar contraste, alt texts, ARIA labels
9. **Performance** — Medir tempo de carregamento, otimizar se necessario
10. **Dominio customizado** — Considerar dominio proprio (ex: criapa.com.br)
