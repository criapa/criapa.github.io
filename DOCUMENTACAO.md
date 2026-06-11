# CRIAPA Hub - Documentacao Tecnica Completa do Site

**URL:** https://criapa.github.io/
**Repositorio:** https://github.com/criapa/criapa.github.io
**Email de contato:** criapa.contato@gmail.com
**WhatsApp:** (81) 99724-4535
**Data da ultima atualizacao:** 11/06/2026
**Autor da documentacao:** OWL (assistente tecnico)
**Responsavel pelo projeto:** Hideo Silva (Pichau) — PhD student RENORBIO/UFRPE

---

## 1. Estrutura de Arquivos

### 1.1 Paginas principais (CRIAPA Hub)

| Arquivo | Linhas | Tamanho | Descricao |
|---------|--------|---------|-----------|
| `index.html` | ~1490 | ~90KB | Pagina principal (landing page) |
| `marca-mista-no-inpi.html` | ~485 | ~47KB | Artigo: Marca Mista no INPI |
| `registro-marca-internacional.html` | ~617 | ~59KB | Artigo: Registro de Marca Internacional |
| `propriedade-intelectual-startups.html` | ~747 | ~68KB | Artigo: PI para Startups |
| `classificacao-nice.html` | ~720 | ~45KB | Lista completa das 45 classes de Nice |
| `sucesso.html` | 28 | 1.6KB | Pagina de confirmacao de envio (nao utilizada) |
| `DOCUMENTACAO.md` | ~900 | ~35KB | Este arquivo de documentacao |
| `PLANEJAMENTO_INTEGRACAO.md` | ~855 | ~25KB | Planejamento de integracao site + scripts |

### 1.2 Imagens

| Arquivo | Tamanho | Uso |
|---------|---------|-----|
| `criapa.png` | ~90KB | Logo do site (header), thumbnail WhatsApp/Facebook, favicon |
| `favicon.ico` | ~14KB | Favicon do navegador (32x32, fundo transparente) |
| `madruga.png` | ~72KB | Imagem decorativa (removida do index) |

### 1.3 Paginas legado/outros projetos (nao fazem parte do CRIAPA Hub)

`aprese.html`, `detektai.html`, `i9nursing.html`, `incubatec.html`, `incubatecj.html`, `index2.html`, `regulai.html`, `regulai-a.html`, `regulai-orecamento.html`, `slidesincuba.html`, `vid.html`

---

## 2. Arquitetura do Sistema

### 2.1 Hosting
- **Plataforma:** GitHub Pages (static site, sem backend)
- **Dominio:** criapa.github.io (GitHub Pages default, sem dominio customizado)
- **Deploy:** Automatico via `git push` para branch `main`
- **SSL:** Automatico pelo GitHub Pages
- **CDN:** Cloudflare (via GitHub Pages)

### 2.2 Stack Tecnologico
- **Frontend:** HTML5 + CSS3 + JavaScript vanilla (sem frameworks)
- **CSS:** Variaveis CSS custom properties (`:root`), Flexbox, Grid, animacoes CSS
- **JS:** Vanilla JS (ES6+), sem dependencias externas
- **Fontes:** Google Fonts (Raleway para headings, system-ui para corpo)
- **Formulario:** FormSubmit.co (gratuito, ilimitado, sem API key)
- **Analytics:** Google Analytics 4 (G-T51W2YTBM0)
- **Imagens:** PNG locais no repositorio
- **SEO:** Meta tags Open Graph, Twitter Cards, canonical URLs

### 2.3 Deploy Workflow
```bash
cd C:\Users\Pichau\criapa-repo
git add -A
git commit -m "descricao da alteracao"
git push
```

**REGRA CRITICA:** Nunca copiar workspace (`criapahub-site`) para repo (`criapa-repo`) cegamente. O repo tem arquivos unicos que o workspace nao tem. Sempre usar `git diff` antes de push.

### 2.4 Regra de Aprovacoes
- **Padrao:** "Allow once" — cada acao precisa de aprovacao individual do usuario
- **Nunca:** Aprovar em batch, auto-aprovar, ou executar multiplas acoes sem aprovacao
- **Aplicacao:** Instalacoes, criacao de arquivos, comandos que modificam estado, escrita de credenciais

---

## 3. Design System

### 3.1 Paleta de Cores (CSS Variables)

```css
:root {
  --azul-900: #0A1B3A;    /* Fundo escuro principal */
  --azul-800: #0F2847;    /* Fundo secundario */
  --teal-500: #269AB6;    /* Cor primaria de acao, botoes, links */
  --teal-400: #38B6CE;    /* Teal hover */
  --verde-500: #00C48C;   /* Verde sucesso, checkmarks */
  --ouro-500: #D4A843;    /* Dourado para labels e destaques */
  --heading: #1C3622;     /* Cor de titulos */
  --transition: .3s cubic-bezier(.4,0,.2,1);
}
```

### 3.2 Tipografia
- **Headings:** Raleway (Google Fonts, pesos 400-900)
- **Corpo:** System font stack (`system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`)
- **Tamanhos:** Usa `clamp()` para responsividade fluida

### 3.3 Breakpoints
| Breakpoint | Largura | Uso |
|------------|---------|-----|
| Desktop | > 768px | Layout completo, nav visivel |
| Mobile | <= 768px | Menu hamburger, nav oculta |
| Mobile small | <= 480px | Padding reduzido, fonte menor |

### 3.4 Convencoes de CSS
- **Nao usar:** `text-align: justify` em textos longos (usuario rejeitou)
- **Excecao:** Textos de FAQ e artigos usam `text-align:justify`
- **Simbolos decorativos:** Grandes (12-18rem, 5-8% opacity)
- **Botoes nao-submit:** Sempre usar `type="button"`
- **Mensagem de sucesso:** Div de sucesso FORA do `</form>`

---

## 4. Componentes

### 4.1 Header

#### HTML (index.html)
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
```

#### CSS do Header (identico em todas as paginas)
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
.header-logo { color: var(--white); }
.header.scrolled .header-logo { color: var(--heading); }
.header-nav a { color: rgba(255,255,255,.8); }
.header.scrolled .header-nav a { color: var(--gray-600); }
.header-toggle span { background: var(--white); }
.header.scrolled .header-toggle span { background: var(--azul-900); }

@media(max-width:768px) {
  .header-nav { display: none; }
  .header-cta { display: none; }
  .header-toggle { display: flex; }
}
```

#### JS do Header (identico em todas as paginas)
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

#### Logo
- **Arquivo:** `criapa.png` (36x36px, border-radius: 8px, object-fit: cover)
- **Substituiu:** `<div class="logo-mark">CR</div>` (quadrado com letras "CR")
- **Favicon:** `favicon.ico` (32x32, fundo transparente, gerado a partir da criapa.png)

### 4.2 Hero Section (index.html)

#### Frases do Hero (estado atual)
- **Line 1 (label):** "Registro de Marca no INPI"
- **Line 2 (titulo principal):** "Sua ideia tem valor. Nao deixe que uma marca desprotegida coloque tudo a perder"
- **CTA Final:** "Registre sua marca de forma agil e descomplicada"

### 4.3 Secao "Como Funciona" (index.html)

#### Frase de conclusao
```html
<p style="text-align:center"><strong>Pronto!</strong><br>Deixe a burocracia com a gente</p>
```
- "Pronto!" em cima (negrito)
- "Deixe a burocracia com a gente" embaixo

### 4.4 Formulario de Contato (Modal)

#### Campos do Modal (3 steps)

**Step 1 — Nome da marca:**
- `id="stepMarca"` — Input type="text"
- Placeholder: "Qual o nome da marca que deseja consultar?"
- Icone: Lupa SVG (class `modal-icon-search`, 18x18px)

**Step 2 — Dados pessoais:**
- `id="stepNome"` — Input type="text" — "Seu nome completo"
- `id="stepEmail"` — Input type="email" — "Seu melhor e-mail"
- `id="stepWhatsapp"` — Input type="tel" — "WhatsApp (com DDD)"
- `id="stepRedeSocial"` — Input type="text" — "Rede social (Instagram, Facebook, etc.)"

**Step 3 — Servico e mensagem:**
- `id="stepServico"` — Select com opcoes (Busca de Anterioridade, Registro de Marca, Monitoramento, Consultoria PI)
- `id="stepMensagem"` — Textarea — "Mensagem (opcional)"

#### JS do Submit (estado atual)
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

**Nota:** O seletor usa `href*="#contato"` (attribute contains) para capturar tanto `#contato` quanto `https://criapa.github.io/#contato`.

### 4.5 FormSubmit.co
- **URL de acao:** `https://formsubmit.co/criapa.contato@gmail.com`
- **Limite:** Ilimitado (gratuito, sem API key)
- **Formato de email:** Tabela (`_template=table`)
- **Captcha:** Desabilitado (`_captcha=false`)
- **Assunto:** "Nova consulta CRIAPA Hub" (`_subject`)

### 4.6 WhatsApp Flutuante
- **Numero:** (81) 99724-4535
- **Link:** `https://wa.me/5581997244535?text=Ola!%20Vi%20o%20site%20da%20CRIAPA%20Hub%20e%20quero%20saber%20mais%20sobre%20registro%20de%20marca`
- **Mensagem pre-preenchida:** Identifica que o usuario veio do site

### 4.7 Google Analytics 4
- **ID de medicao:** `G-T51W2YTBM0`
- **Script adicionado em:** Todas as 5 paginas (index, 3 artigos, classificacao-nice)
- **Localizacao:** No `<head>`, apos as meta tags de Open Graph

```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-T51W2YTBM0"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-T51W2YTBM0');
</script>
```

### 4.8 Meta Tags de Compartilhamento (Open Graph / Twitter Cards)

```html
<meta property="og:title" content="CRIAPA Hub | Registro de Marca no INPI">
<meta property="og:description" content="Assessoria completa em registro de marcas no INPI. Proteja sua marca com segurança e agilidade.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://criapa.github.io/">
<meta property="og:image" content="https://criapa.github.io/criapa.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta property="og:locale" content="pt_BR">
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="CRIAPA Hub | Registro de Marca no INPI">
<meta name="twitter:description" content="Assessoria completa em registro de marcas no INPI. Proteja sua marca com segurança e agilidade.">
<meta name="twitter:image" content="https://criapa.github.io/criapa.png">
```

### 4.9 Favicon
- **Arquivo:** `favicon.ico` (32x32, fundo transparente)
- **Gerado a partir de:** `criapa.png` original (767x696, RGBA)
- **Tags no HTML:**
```html
<link rel="icon" type="image/x-icon" href="https://criapa.github.io/favicon.ico">
<link rel="shortcut icon" type="image/x-icon" href="https://criapa.github.io/favicon.ico">
```

---

## 5. Paginas de Artigos — Detalhamento Completo

### 5.1 Marca Mista no INPI
**Arquivo:** `marca-mista-no-inpi.html`
**URL:** https://criapa.github.io/marca-mista-no-inpi.html
**Titulo:** "Marca Mista no INPI: o que esta protegido e o que ainda pode estar em risco"
**Data:** 10 de junho de 2026
**Tempo de leitura:** 12 min

**Estrutura do conteudo:**
1. Introducao — O problema da marca mista
2. O que e uma marca mista?
3. Os 4 tipos de marca reconhecidos pelo INPI (tabela comparativa)
4. Os riscos da marca mista (4 riscos detalhados)
5. Caso real: quando a marca mista nao bastou
6. A estrategia ideal: protecao em camadas (4 camadas)
7. Como saber se sua marca mista esta bem protegida? (checklist)
8. O processo de registro no INPI (8-14 meses)
9. Conclusao

### 5.2 Registro de Marca Internacional
**Arquivo:** `registro-marca-internacional.html`
**URL:** https://criapa.github.io/registro-marca-internacional.html
**Titulo:** "Registro de Marca Internacional: como chegar a outros paises"
**Data:** 10 de junho de 2026
**Tempo de leitura:** 15 min

**Estrutura do conteudo:**
1. Introducao — O desafio da protecao internacional
2. O que e o Sistema de Madri? (Acordo de Madri, Protocolo de Madri, Brasil aderiu em 2019)
3. Quais paises sao membros? (tabela por regiao)
4. Requisitos para usar o Sistema de Madri (5 requisitos)
5. Passo a passo do processo
6. **Custos envolvidos (atualizado em 2026):**
   - Taxa basica OMPI: 653 CHF (PB) / 903 CHF (cores) + 100 CHF/classe adicional
   - Taxa por pais designado (tabela com 9 mercados)
   - Taxa do INPI (GRU codigo 3004)
7. Prazos tipicos
8. Casos praticos e exemplos
9. Conclusao

### 5.3 Propriedade Intelectual para Startups
**Arquivo:** `propriedade-intelectual-startups.html`
**URL:** https://criapa.github.io/propriedade-intelectual-startups.html
**Titulo:** "Propriedade Intelectual para Startups: o que voce precisa saber"
**Data:** 10 de junho de 2026
**Tempo de leitura:** 18 min

**Estrutura do conteudo:**
1. Introducao — O momento em que o investidor pergunta sobre PI
2. Por que a PI e crucial para startups? (3 razoes)
3. Os tipos de PI relevantes para startups (tabela com 7 tipos)
4. A ordem ideal de protecao
5. Como investidores avaliam PI
6. Checklist pratico por estagio
7. Erros comuns
8. **Como registrar marca para startup: as classes essenciais**
   - Classe 9 (Software e equipamentos digitais)
   - Classe 35 (Publicidade e negocios)
   - Classe 42 (Servicos tecnologicos e cientificos)
   - Link para a pagina de classificacao completa das 45 classes
9. Conclusao

### 5.4 Classificacao de Nice — 45 Classes
**Arquivo:** `classificacao-nice.html`
**URL:** https://criapa.github.io/classificacao-nice.html
**Titulo:** "Classificacao Internacional de Nice: Lista Completa das 45 Classes"
**Data:** 11 de junho de 2026
**Edicao:** 13a edicao (NCL 13-2026)

**Estrutura do conteudo:**
1. O que e a Classificacao de Nice?
2. Por que a classe certa importa (warning box)
3. Como identificar sua classe (4 passos)
4. **Classes 1 a 34 — Produtos** (34 cards com numero, nome, descricao, exemplos)
5. **Classes 35 a 45 — Servicos** (11 cards com numero, nome, descricao, exemplos)
6. Dica sobre consulta a especialista
7. CTA para consulta de viabilidade

**Layout:** Cards em grid responsivo (2 colunas em desktop, 1 em mobile), com tags visuais diferenciando Produto (azul) e Servico (verde).

---

## 6. Fluxo de Navegacao

### 6.1 Fluxo do Visitante
```
Visitante acessa o site
    → Le artigos / navega pelo site
    → Clica "Quero Consultar" (header, hero, CTA final, artigos)
        → Modal abre com formulario de 3 steps
            → Step 1: Nome da marca
            → Step 2: Dados pessoais (nome, email, WhatsApp, rede social)
            → Step 3: Servico e mensagem
                → Envia formulario
                    → FormSubmit.co envia email para criapa.contato@gmail.com
                    → Tela de sucesso aparece no modal
    → OU clica no WhatsApp flutuante
        → Abre WhatsApp com mensagem pre-preenchida
```

### 6.2 Fluxo de Leads (apos integracao)
```
Lead preenche formulario → Email chega via FormSubmit
    → Script importa email para SQLite (leads_site)
    → Lead aparece no banco com status 'novo'
    → Equipe contata lead via WhatsApp/email
    → Status atualizado: novo → contatado → respondeu → cliente
```

---

## 7. Regras e Convencoes de Desenvolvimento

### 7.1 Aprovacoes
- **Padrao:** "Allow once" — cada acao precisa de aprovacao individual
- **Nunca:** Aprovar em batch ou auto-aprovar

### 7.2 CSS
- **Nao usar:** `text-align: justify` em textos longos (usuario rejeitou)
- **Excecao:** Textos de FAQ e artigos usam `text-align:justify`
- **Alinhamento padrao:** Left-aligned
- **Simbolos decorativos:** Grandes (12-18rem, 5-8% opacity)
- **Botoes nao-submit:** Sempre usar `type="button"`
- **Mensagem de sucesso:** Div de sucesso FORA do `</form>`

### 7.3 Formulario
- **Nao redirecionar:** Tudo acontece na mesma pagina (sem redirect)
- **Metodo:** fetch com URLSearchParams e mode: 'no-cors'
- **Campos hidden:** Copiados dos campos visiveis via JS antes do submit
- **Validacao:** Step 1 (marca >= 2 chars), Step 2 (nome >= 2, email @, whatsapp >= 10)

### 7.4 Header
- **No topo (scrollY <= 50):** Transparente, texto branco
- **Ao scroll (scrollY > 50):** Branco com blur, texto escuro
- **Logo:** criapa.png 36x36px, border-radius: 8px
- **Mobile (<= 768px):** Menu hamburger com 3 barrinhas

### 7.5 Git/Deploy
- **Repositorio local:** `C:\Users\Pichau\criapa-repo\`
- **Workspace:** `C:\Users\Pichau\criapahub-site\`
- **Nunca:** Copiar workspace para repo cegamente
- **Sempre:** Usar `git diff` antes de push
- **Branch:** main
- **Mensagens de commit:** Em portugues, descritivas

### 7.6 JavaScript
- **Sem frameworks:** Vanilla JS apenas
- **Sem dependencias:** Zero bibliotecas externas
- **Validacao de sintaxe:** Testar com `node -e "new Function(code)"` apos substituicoes

### 7.7 Alegacoes e Compliance
- **Nao usar:** Estatisticas sem fonte (ex: "75% das empresas nao protegem")
- **Nao usar:** Numeros de clientes sem comprovacao (ex: "3.700 marcas")
- **Usar:** Linguagem qualitativa ("Muitas empresas...", "A maioria...")
- **LGPD:** Dados de leads sao publicos (CNPJ) ou fornecidos voluntariamente (formulario)
- **Opt-out:** Incluir opcao de descadastramento em mensagens WhatsApp

---

## 8. Historico Completo de Commits

```
fa8089f Remove 'an' de 'sem an surpresas' no FAQ
71c0edc Justifica textos das respostas do FAQ
ba7c6f9 Adiciona Google Analytics 4 (G-T51W2YTBM0) em todas as paginas
904e497 Recria favicon.ico com fundo transparente
9a2109f Adiciona favicon.ico e atualiza og:image para criapa.png
43d6831 Ajusta proporção folder.png para crop 1200x630 sem distorção
9e718bd Redimensiona folder.png para 1200x630 (otimizar carregamento)
21e1571 Adiciona imagem folder.png para thumbnail WhatsApp
3a09598 Corrige ortografia: procuracao -> procuração
a7387a4 Adiciona pagina com lista completa das 45 classes de Nice
9d17cec Atualiza custos do Sistema de Madri com valores 2026
960f70f Update README.md
b2ccb49 Corrige botoes: Quero Consultar abre modal, WhatsApp flutuante com link correto
1541b65 Corrige telefone WhatsApp para numero real (81) 99724-4535
2740caa Remove alegacoes nao comprovadas e padroniza MDIC
3359ae6 Remove imagem madruga.png do index
09db385 Documentacao tecnica completa do site CRIAPA Hub
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
```

---

## 9. Problemas Conhecidos, Causas e Solucoes

### 9.1 Formulario nao enviava no mobile
- **Causa:** FormSubmit bloqueia CORS de dispositivos mobile
- **Solucao:** fetch com URLSearchParams e mode: 'no-cors'

### 9.2 Header sempre branco nas paginas de artigos
- **Causa:** CSS do header tinha `background:rgba(255,255,255,.96)` fixo
- **Solucao:** Copiar CSS do index com `.header.scrolled` e JS do scroll

### 9.3 Menu mobile nao abria nas paginas de artigos
- **Causa 1:** Seletor JS `a[href="#contato"]` nao capturava links com dominio completo
- **Solucao 1:** Mudar para `a[href*="#contato"]`
- **Causa 2:** Erro de sintaxe JS `}););););` quebrava todo o script
- **Solucao 2:** Corrigir para `});` — validar JS com `node -e "new Function(code)"`

### 9.4 Icones do formulario enormes
- **Causa:** CSS `.modal-icon-search` nao existia nas paginas de artigos
- **Solucao:** Adicionar CSS com `width:18px; height:18px`

### 9.5 Logo CR antiga nas paginas de artigos
- **Causa:** `<div class="logo-mark">CR</div>` ainda estava no HTML
- **Solucao:** Trocar por `<img src="criapa.png" class="logo-img">`

### 9.6 Rede social nao aparecia no email
- **Causa:** Faltava hidden input `formRedeSocial` e JS para copiar valor
- **Solucao:** Adicionar hidden input e `formRedeSocial.value = stepRedeSocial.value.trim()`

### 9.7 Sucesso prematuro do formulario
- **Causa:** `formTarget.onload` disparava quando o iframe carregava pela primeira vez
- **Solucao:** Flag `formSubmitted` para so disparar depois do submit real

### 9.8 CTA final apontava para WhatsApp em vez do modal
- **Causa:** Botao "Quero Consultar" do CTA final tinha `href="wa.me/..."`
- **Solucao:** Mudar para `href="#contato"` para abrir o modal

### 9.9 WhatsApp flutuante com link vazio
- **Causa:** `href="#"` nao levava a lugar nenhum
- **Solucao:** Adicionar link `wa.me/5581997244535` com mensagem pre-preenchida

### 9.10 Telefone falso no site
- **Causa:** Numero (81) 99999-9999 era placeholder
- **Solucao:** Substituir pelo numero real (81) 99724-4535

### 9.11 Alegacoes nao comprovadas
- **Causa:** "75% das empresas nao protegem" e "3.700 marcas" sem fonte
- **Solucao:** Remover e usar linguagem qualitativa

### 9.12 Inconsistencia MDIC/Ministerio da Economia
- **Causa:** Textos diferentes em paginas diferentes
- **Solucao:** Padronizar para "MDIC (Ministerio do Desenvolvimento, Industria, Comercio e Servicos)"

### 9.13 Imagem de thumbnail nao carregava
- **Causa:** Faltavam meta tags `og:image` e `twitter:image`
- **Solucao:** Adicionar tags apontando para `criapa.png`

### 9.14 Favicon sem transparencia
- **Causa:** Imagem convertida para RGB perdia o canal alpha
- **Solucao:** Usar imagem original RGBA e salvar como ICO

---

## 10. Licoes Aprendidas e Melhoria de Rigor

### 10.1 Validacao de Sintaxe JS
**Problema:** Substituicoes de JS via regex podem introduzir erros de sintaxe.
**Solucao:** Apos cada substituicao, validar com `node -e "new Function(code)"`.

### 10.2 Seletores CSS/JS
**Problema:** Seletores rigidos como `href="#contato"` falham quando o href inclui dominio completo.
**Solucao:** Usar seletores mais flexveis como `href*="#contato"`.

### 10.3 localhost no navegador do visitante
**Problema:** `fetch('http://localhost:5000')` roda no PC do visitante, nao no seu.
**Solucao:** Usar FormSubmit (email) como ponto de integracao, nao API local.

### 10.4 Alegacoes sem fonte
**Problema:** Estatisticas sem fonte podem configurar publicidade enganosa (CDC).
**Solucao:** Usar linguagem qualitativa ou citar fontes oficiais.

### 10.5 Teste Multi-Dispositivo
**Problema:** Funciona no desktop mas nao no mobile (ou vice-versa).
**Solucao:** Testar sempre em ambos os contextos.

### 10.6 Commits Atomicos
**Problema:** Multiplas alteracoes em um commit dificultam revert e debug.
**Solucao:** Commits atomicos, uma alteracao por commit, mensagens descritivas.

---

## 11. Contatos e Recursos

- **Email:** criapa.contato@gmail.com
- **WhatsApp:** (81) 99724-4535
- **GitHub:** https://github.com/criapa/criapa.github.io
- **Site:** https://criapa.github.io/
- **Analytics:** https://analytics.google.com (propriedade: criapa.github.io, ID: G-T51W2YTBM0)
- **FormSubmit:** https://formsubmit.co/criapa.contato@gmail.com
- **Logo:** criapa.png (36x36px)
- **Favicon:** favicon.ico (32x32, fundo transparente)
- **Thumbnail:** criapa.png (1200x630, crop centralizado)
- **Usuario:** Hideo Silva (Pichau) — PhD student RENORBIO/UFRPE
- **Estilo de comunicacao:** Direto, resultados imedios, sem batching

---

## 12. Proximos Passos (Planejamento de Integracao)

Veja o arquivo `PLANEJAMENTO_INTEGRACAO.md` para detalhes completos.

**Resumo das fases:**

| Fase | Tarefa | Status |
|------|--------|--------|
| 1 | Criar tabela `leads_site` no banco | Pendente |
| 1 | Criar importador IMAP (`leads_site.py`) | Pendente |
| 1 | Adicionar campo `pagina_origem` no formulario | Pendente |
| 2 | Implementar endpoint de link WhatsApp | Pendente |
| 2 | Criar templates de mensagem | Pendente |
| 3 | Configurar GA4 (eventos personalizados) | Pendente |
| 4 | Limpar scripts antigos + backups | Pendente |
| 4 | Adicionar campos `dor`, `necessidade`, `produto_interesse` | Pendente |
| 4 | Criar tabela `leads_historico` | Pendente |
| 4 | Implementar comando `limpar` e `relatorio` | Pendente |

---

**Fim do planejamento v3.1**
