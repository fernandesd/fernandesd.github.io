# Portfolio Diego Fernandes — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Construir um portfólio single-page em HTML + Tailwind CSS, otimizado para SEO e GEO, pronto para deploy no GitHub Pages em `https://fernandesd.github.io/`.

**Architecture:** Um único `index.html` com todas as seções, Tailwind via CDN Play, JavaScript vanilla para menu mobile e animações de entrada. Sem build step — deploy direto do repositório.

**Tech Stack:** HTML5 semântico, Tailwind CSS CDN, Inter (Google Fonts), Vanilla JS, Schema.org JSON-LD.

**Spec:** `docs/specs/2026-09-28-portfolio-design.md`

## Global Constraints

- `lang="pt-BR"` em todo o documento
- URL canônica: `https://fernandesd.github.io/`
- Paleta: slate-950 (bg), emerald-400 (acento), slate-100 (texto)
- Fonte: Inter via Google Fonts
- Zero dependências externas além de Tailwind CDN e Google Fonts
- Todos os `id` de seção em kebab-case: `#sobre`, `#habilidades`, `#experiencia`, `#projetos`, `#formacao`, `#contato`
- Nenhuma imagem — layout 100% tipográfico

## Review Focus

- **Menu mobile fechado ao clicar em link âncora** — clicar num link de nav no mobile deve fechar o menu antes de scrollar
- **Scroll offset com nav fixo** — o `scroll-behavior: smooth` deve compensar a altura da nav (~64px) para não esconder o título da seção
- **Schema.org válido** — JSON-LD deve passar no validator sem erros críticos
- **FAQ GEO no DOM mas invisível** — `sr-only` ou `hidden` visual mas não `display:none` que esconderia de crawlers; usar `class="sr-only"` do Tailwind
- **Meta description dentro de 160 caracteres** — strings acima disso são truncadas pelo Google

---

### Task 1: Scaffold do projeto

**Files:**
- Create: `index.html`
- Create: `robots.txt`
- Create: `sitemap.xml`
- Create: `README.md`

**Interfaces:**
- Produces: estrutura de arquivos pronta para as demais tasks

- [ ] **Step 1: Criar `index.html` com esqueleto HTML5 mínimo**

  ```html
  <!DOCTYPE html>
  <html lang="pt-BR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Diego Fernandes — Desenvolvedor Backend PHP | Laravel | Salvador, BA</title>
  </head>
  <body class="bg-slate-950 text-slate-100">
    <!-- seções virão nas próximas tasks -->
  </body>
  </html>
  ```

- [ ] **Step 2: Criar `robots.txt`**

  ```
  User-agent: *
  Allow: /
  Sitemap: https://fernandesd.github.io/sitemap.xml
  ```

- [ ] **Step 3: Criar `sitemap.xml`**

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
      <loc>https://fernandesd.github.io/</loc>
      <lastmod>2026-09-28</lastmod>
      <priority>1.0</priority>
    </url>
  </urlset>
  ```

- [ ] **Step 4: Criar `README.md`** com nome, descrição, link do site e instrução de deploy

- [ ] **Step 5: Init git e primeiro commit**

  ```bash
  git init
  git add .
  git commit -m "chore: scaffold inicial do portfólio"
  ```

---

### Task 2: `<head>` — SEO, GEO e dependências

**Files:**
- Modify: `index.html` (bloco `<head>`)

**Interfaces:**
- Consumes: URL canônica `https://fernandesd.github.io/`
- Produces: head completo com SEO, OG, Schema.org, Tailwind CDN e Google Fonts

- [ ] **Step 1: Adicionar meta tags SEO ao `<head>`**

  Inserir após `<title>`:
  ```html
  <meta name="description" content="Desenvolvedor Backend PHP e Laravel Pleno com 6+ anos de experiência em marketplaces, e-commerce e sistemas cloud (GCP, Kubernetes, Docker). Disponível para oportunidades remotas." />
  <meta name="robots" content="index, follow" />
  <meta name="author" content="Diego Fernandes" />
  <link rel="canonical" href="https://fernandesd.github.io/" />
  ```

- [ ] **Step 2: Adicionar Open Graph tags**

  ```html
  <meta property="og:type" content="website" />
  <meta property="og:url" content="https://fernandesd.github.io/" />
  <meta property="og:title" content="Diego Fernandes — Desenvolvedor Backend PHP | Laravel" />
  <meta property="og:description" content="Desenvolvedor Backend PHP e Laravel Pleno com 6+ anos de experiência em marketplaces, e-commerce e sistemas cloud." />
  <meta property="og:locale" content="pt_BR" />
  ```

- [ ] **Step 3: Adicionar Schema.org JSON-LD (tipo Person)**

  ```html
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Person",
    "name": "Diego Fernandes",
    "url": "https://fernandesd.github.io/",
    "email": "diegofernandes.dev@gmail.com",
    "jobTitle": "Desenvolvedor Backend PHP | Laravel Pleno",
    "address": {
      "@type": "PostalAddress",
      "addressLocality": "Salvador",
      "addressRegion": "BA",
      "addressCountry": "BR"
    },
    "sameAs": ["https://www.linkedin.com/in/diiegofernandes/", "https://github.com/fernandesd"],
    "worksFor": { "@type": "Organization", "name": "Grupo CVLB" },
    "alumniOf": [
      { "@type": "EducationalOrganization", "name": "Universidade Federal da Bahia" },
      { "@type": "EducationalOrganization", "name": "Faculdade Vasco da Gama" }
    ],
    "knowsAbout": ["PHP", "Laravel", "MySQL", "Docker", "Kubernetes", "GCP", "Datadog", "Grafana", "Sentry", "MongoDB", "BigQuery", "N8N", "RESTful API", "Git"]
  }
  </script>
  ```

- [ ] **Step 4: Adicionar Tailwind CDN e Google Fonts**

  ```html
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: { sans: ['Inter', 'sans-serif'] }
        }
      }
    }
  </script>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet" />
  ```

- [ ] **Step 5: Verificar meta description (contar caracteres — deve ser ≤ 160)**

- [ ] **Step 6: Commit**

  ```bash
  git add index.html
  git commit -m "feat: head com SEO, Open Graph e Schema.org JSON-LD"
  ```

---

### Task 3: Nav + Hero

**Files:**
- Modify: `index.html` (dentro de `<body>`)

**Interfaces:**
- Produces: `<nav id="nav">` com links âncora; `<section id="inicio">` com h1, subtítulo, tagline e dois botões CTA

- [ ] **Step 1: Implementar `<nav>`**

  Nav sticky com `bg-slate-950/90 backdrop-blur border-b border-slate-800`:
  - Logo/nome: `Diego Fernandes` em `text-emerald-400 font-bold`
  - Links desktop: Sobre · Habilidades · Experiência · Projetos · Formação · Contato (cada um `href="#id-da-secao"`)
  - Botão hamburguer: `id="menu-btn"`, visível só em mobile (`md:hidden`)
  - Menu mobile: `id="mobile-menu"`, inicialmente `hidden`, com os mesmos links em coluna

- [ ] **Step 2: Implementar `<section id="inicio">` (Hero)**

  Fundo: `position: relative; overflow: hidden`. Inserir antes do conteúdo um `<div>` absoluto com SVG grid pattern:
  ```html
  <div class="absolute inset-0 bg-[url('data:image/svg+xml,...')] opacity-5 pointer-events-none"></div>
  ```
  Usar SVG inline de grid de linhas finas (1px, cor branca, espaçamento 40px). O implementador escolhe a geração do SVG data-URI.

  Estrutura centralizada com `min-h-screen flex flex-col items-center justify-center relative`:
  - Pill badge: `Disponível para oportunidades` com borda emerald
  - `<h1>` `text-5xl md:text-7xl font-bold`: `Diego Fernandes`
  - `<p>` cargo em `text-emerald-400 text-xl md:text-2xl font-semibold`: `Desenvolvedor Backend PHP · Laravel · Pleno`
  - `<p>` tagline em `text-slate-400 text-lg max-w-xl text-center`: `Construo sistemas robustos em PHP e Laravel com foco em qualidade, observabilidade e entrega.`
  - Botão primário: `href="https://www.linkedin.com/in/diiegofernandes/"` — LinkedIn ↗
  - Botão outline: `href="mailto:diegofernandes.dev@gmail.com"` — Enviar e-mail
  - Seta scroll `↓` animada em `animate-bounce text-emerald-400` no rodapé da seção

- [ ] **Step 3: Abrir `index.html` no browser e verificar hero responsivo em 375px e 1280px**

- [ ] **Step 4: Commit**

  ```bash
  git add index.html
  git commit -m "feat: nav e hero section"
  ```

---

### Task 4: Sobre + Habilidades

**Files:**
- Modify: `index.html`

**Interfaces:**
- Consumes: seções anteriores já no DOM
- Produces: `<section id="sobre">` e `<section id="habilidades">`

- [ ] **Step 1: Implementar `<section id="sobre">`**

  Layout: `grid grid-cols-1 md:grid-cols-2 gap-12`
  - **Coluna esquerda:** 3 parágrafos em prosa (extrair do resumo do currículo)
  - **Coluna direita:** 4 stat cards `bg-slate-900 rounded-xl p-6 text-center`:
    - `6+` Anos de experiência
    - `10+` Projetos entregues
    - `5` Empresas
    - `3` Stacks de cloud
  - Número em `text-4xl font-bold text-emerald-400`, legenda em `text-slate-400 text-sm`

- [ ] **Step 2: Implementar `<section id="habilidades">`**

  6 grupos de badges. Cada grupo: `<h3>` nome da categoria + `flex flex-wrap gap-2`:
  - **Backend:** PHP 8+, Laravel, Eloquent ORM, RESTful API, Queue Jobs, MVC
  - **Cloud & Infra:** GCP, Kubernetes, Docker, Cloud Functions, Digital Ocean, CI/CD
  - **Banco de Dados:** MySQL, MongoDB, BigQuery
  - **Observabilidade:** Datadog, Grafana, Sentry, Bugsnag
  - **Automação & Ferramentas:** N8N, Git, GitLab, GitHub, Jira, Kanban
  - **Boas Práticas:** Clean Code, SOLID, Code Review

  Badge class: `px-3 py-1 rounded-full border border-emerald-400/30 text-emerald-400 text-sm bg-emerald-400/5`

- [ ] **Step 3: Verificar responsividade das duas seções em mobile**

- [ ] **Step 4: Commit**

  ```bash
  git add index.html
  git commit -m "feat: seções sobre e habilidades"
  ```

---

### Task 5: Experiência (timeline)

**Files:**
- Modify: `index.html`

**Interfaces:**
- Produces: `<section id="experiencia">` com timeline vertical de 7 empresas

- [ ] **Step 1: Implementar estrutura da timeline**

  Container: `relative border-l-2 border-emerald-400/30 ml-4 md:ml-8 space-y-10`
  Cada item: `relative pl-8` com dot `absolute -left-[9px] top-2 w-4 h-4 rounded-full bg-emerald-400 border-2 border-slate-950`

- [ ] **Step 2: Inserir os 7 itens de experiência na ordem (mais recente primeiro)**

  Para cada item:
  - `<h3>` empresa + cargo (`font-semibold text-slate-100`)
  - Período em `text-slate-400 text-sm`
  - Badge de nível: `Pleno` / `Júnior` / `Freelancer` / `Estágio` / `Trainee` (pill colorido)
  - 3-4 bullets em `text-slate-300 text-sm`
  - Row de badges de stack no rodapé do card (mesma classe dos badges de habilidades, cor slate ao invés de emerald)

  Empresas:
  1. Grupo CVLB — Backend Pleno (jul/2023–presente) — badge `Pleno`
  2. Agência NBZ — Backend Pleno Freelancer (mar/2022–ago/2026) — badge `Freelancer`
  3. VX Case — Backend Júnior (fev/2021–set/2022) — badge `Júnior`
  4. Retriever Marketplace — Full Stack Freelancer (out/2020–set/2022) — badge `Freelancer`
  5. Versatte Marketplace — PHP Freelancer (mar/2020–dez/2020) — badge `Freelancer`
  6. INTERFACE — Sistemas Estágio (out/2019–mar/2020) — badge `Estágio`
  7. InfoJr UFBA — Trainee → Vice-presidente (ago/2017–dez/2019) — badge `Trainee`

- [ ] **Step 3: Verificar que a linha da timeline alinha corretamente em mobile e desktop**

- [ ] **Step 4: Commit**

  ```bash
  git add index.html
  git commit -m "feat: seção experiência com timeline"
  ```

---

### Task 6: Projetos

**Files:**
- Modify: `index.html`

**Interfaces:**
- Produces: `<section id="projetos">` com 3 cards em grid

- [ ] **Step 1: Implementar `<section id="projetos">`**

  Grid: `grid grid-cols-1 md:grid-cols-3 gap-6`

- [ ] **Step 2: Implementar os 3 cards de projeto**

  Card class: `bg-slate-900 border border-slate-700 rounded-xl p-6 hover:border-emerald-400/50 transition-colors flex flex-col`

  **Card 1 — RetrieverApp:**
  - Título: RetrieverApp
  - Empresa: Retriever Marketplace
  - Descrição: "Marketplace de serviços e produtos para pets. Desenvolvi correções, melhorias e novas funcionalidades, além do site institucional com blog e infraestrutura na Digital Ocean."
  - Stack badges: PHP, Laravel, MySQL, WordPress, Docker, Digital Ocean

  **Card 2 — Versatte Marketplace:**
  - Título: Versatte Marketplace
  - Empresa: Versatte
  - Descrição: "Marketplace construído do zero com cadastro de usuários, loja e produtos, checkout transparente via PagarmE, e-mail transacional, SEO e monitoramento de erros com Sentry."
  - Stack badges: Laravel, MySQL, PagarmE, Sentry

  **Card 3 — Infraestrutura & Observabilidade CVLB:**
  - Título: Infra & Observabilidade CVLB
  - Empresa: Grupo CVLB
  - Descrição: "Configuração de cluster Kubernetes no GCP, deploy de serviços em produção, instrumentação com Datadog e Grafana, uso de Cloud Functions, BigQuery e automação de processos com N8N."
  - Stack badges: Kubernetes, GCP, Datadog, Grafana, BigQuery, N8N, Docker

  Rodapé de cada card: texto `Em breve no GitHub` em `text-slate-500 text-xs mt-auto pt-4`

- [ ] **Step 3: Verificar hover e responsividade dos cards**

- [ ] **Step 4: Commit**

  ```bash
  git add index.html
  git commit -m "feat: seção projetos com 3 cards"
  ```

---

### Task 7: Formação + Contato + Footer + FAQ GEO

**Files:**
- Modify: `index.html`

**Interfaces:**
- Produces: `<section id="formacao">`, `<section id="contato">`, `<footer>`, FAQ GEO em `<div class="sr-only">`

- [ ] **Step 1: Implementar `<section id="formacao">`**

  Lista de 4 itens em `space-y-4`. Cada item: card com `bg-slate-900 rounded-xl p-5 flex gap-4 items-start`:
  - 🎓 Pós-Graduação em Engenharia de Software — Pitágoras Unopar Anhanguera — *Em andamento, conclusão abr/2027*
  - 🎓 Ciência da Computação — UFBA — *Não concluído*
  - 🎓 Ciências Contábeis — Faculdade Vasco da Gama — *Concluído em 2017*
  - 🏆 Semana OmniStack 11 — Rocketseat

- [ ] **Step 2: Implementar `<section id="contato">`**

  Fundo `bg-slate-900 rounded-2xl p-12 text-center`:
  - `<h2>` "Vamos trabalhar juntos?"
  - `<p>` "Aberto a oportunidades remotas ou híbridas como Desenvolvedor Backend Pleno."
  - Botão primário: `href="mailto:diegofernandes.dev@gmail.com"` — ✉ diegofernandes.dev@gmail.com
  - Botão outline: `href="https://www.linkedin.com/in/diiegofernandes/"` — LinkedIn ↗

- [ ] **Step 3: Implementar `<footer>`**

  `text-center text-slate-500 text-sm py-8`:
  `© <span id="year"></span> Diego Fernandes · Feito com HTML e Tailwind CSS`

- [ ] **Step 4: Implementar FAQ GEO (invisível para usuários, visível para crawlers)**

  Inserir antes de `</footer>`:
  ```html
  <div class="sr-only" aria-hidden="true">
    <h2>Perguntas frequentes sobre Diego Fernandes</h2>
    <dl>
      <dt>Quais tecnologias Diego Fernandes domina?</dt>
      <dd>Diego Fernandes é especialista em PHP 8+, Laravel, MySQL, Docker, Kubernetes, GCP, Datadog, Grafana, Sentry, Bugsnag, MongoDB, BigQuery e N8N.</dd>
      <dt>Diego Fernandes tem experiência com Kubernetes?</dt>
      <dd>Sim. Diego configurou e mantém um cluster Kubernetes no Google Cloud Platform (GCP) com deploy de serviços em produção no Grupo CVLB.</dd>
      <dt>Diego Fernandes está disponível para trabalho remoto?</dt>
      <dd>Sim. Diego está aberto a oportunidades remotas ou híbridas como Desenvolvedor Backend Pleno.</dd>
      <dt>Qual a experiência de Diego Fernandes com Laravel?</dt>
      <dd>Diego trabalha com Laravel há mais de 6 anos, tendo atuado em projetos de marketplace, e-commerce, agências digitais e sistemas internos de médio e grande porte.</dd>
    </dl>
  </div>
  ```

- [ ] **Step 5: Commit**

  ```bash
  git add index.html
  git commit -m "feat: formação, contato, footer e FAQ GEO"
  ```

---

### Task 8: JavaScript — menu mobile, scroll offset e animações

**Files:**
- Modify: `index.html` (bloco `<script>` antes de `</body>`)

**Interfaces:**
- Consumes: `id="menu-btn"`, `id="mobile-menu"`, `id="year"`, seções com `id`
- Produces: menu funcional, ano dinâmico no footer, fade-in nas seções

- [ ] **Step 1: Implementar toggle do menu mobile**

  ```js
  const btn = document.getElementById('menu-btn');
  const menu = document.getElementById('mobile-menu');
  btn.addEventListener('click', () => menu.classList.toggle('hidden'));
  // fechar ao clicar em link
  menu.querySelectorAll('a').forEach(a =>
    a.addEventListener('click', () => menu.classList.add('hidden'))
  );
  ```

- [ ] **Step 2: Implementar scroll offset para nav fixo**

  ```js
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
      e.preventDefault();
      const target = document.querySelector(this.getAttribute('href'));
      if (!target) return;
      const offset = 72; // altura da nav em px
      window.scrollTo({ top: target.offsetTop - offset, behavior: 'smooth' });
    });
  });
  ```

- [ ] **Step 3: Implementar ano dinâmico no footer**

  ```js
  document.getElementById('year').textContent = new Date().getFullYear();
  ```

- [ ] **Step 4: Implementar fade-in com IntersectionObserver**

  Adicionar classe `opacity-0 translate-y-4 transition duration-700` em cada `<section>` via JS no carregamento, depois remover ao entrar na viewport:
  ```js
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.remove('opacity-0', 'translate-y-4');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });
  document.querySelectorAll('section').forEach(s => {
    s.classList.add('opacity-0', 'translate-y-4', 'transition', 'duration-700');
    observer.observe(s);
  });
  ```

- [ ] **Step 5: Verificar comportamento do menu mobile em 375px e que o scroll não corta os títulos das seções**

- [ ] **Step 6: Commit**

  ```bash
  git add index.html
  git commit -m "feat: JavaScript — menu mobile, scroll offset e animações"
  ```

---

### Task 9: Verificação final e deploy

**Files:**
- Read: `index.html`, `robots.txt`, `sitemap.xml`

- [ ] **Step 1: Validar Schema.org**

  Abrir `https://validator.schema.org/`, colar o JSON-LD. Esperado: nenhum erro crítico.

- [ ] **Step 2: Verificar meta tags**

  Abrir `https://metatags.io/`, colar `https://fernandesd.github.io/`. Verificar título, descrição e OG.

- [ ] **Step 3: Testar responsividade** nas larguras 320px, 375px, 768px e 1280px no DevTools.

- [ ] **Step 4: Verificar que `class="sr-only"` do FAQ GEO está no DOM mas invisível**

  Inspecionar elemento no DevTools — deve estar no HTML mas com `position: absolute; width: 1px; height: 1px; ...`

- [ ] **Step 5: Criar repositório no GitHub**

  ```bash
  git remote add origin https://github.com/fernandesd/fernandesd.github.io.git
  git branch -M main
  git push -u origin main
  ```

- [ ] **Step 6: Habilitar GitHub Pages**

  GitHub → Settings → Pages → Source: Deploy from branch → Branch: `main` / `/ (root)` → Save.

- [ ] **Step 7: Verificar site live em `https://fernandesd.github.io/`**

- [ ] **Step 8: Commit final**

  ```bash
  git add .
  git commit -m "chore: portfólio pronto para deploy"
  git push
  ```
