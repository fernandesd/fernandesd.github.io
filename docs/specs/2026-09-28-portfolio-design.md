# Portfolio Diego Fernandes — Design Spec
**Data:** 2026-09-28
**Status:** Aprovado

---

## 1. Visão Geral

Site portfólio pessoal de Diego Fernandes, Desenvolvedor Backend PHP/Laravel Pleno, hospedado no **GitHub Pages**. O objetivo é servir como cartão de visita digital para recrutadores e empresas, complementando o LinkedIn e o currículo.

**Metas:**
- Aparecer em buscas por "desenvolvedor backend PHP Laravel Salvador" e variações
- Ser citado por IAs (ChatGPT, Perplexity, Google AI) ao responder perguntas sobre o perfil
- Transmitir credibilidade técnica em segundos para recrutadores
- Carregar rápido e funcionar bem em mobile

---

## 2. Stack Técnica

| Item | Decisão |
|---|---|
| Estrutura | HTML5 semântico, single-page |
| CSS | Tailwind CSS via CDN (Play CDN) |
| JS | Vanilla JS (~50 linhas) |
| Fontes | Inter via Google Fonts |
| Hospedagem | GitHub Pages |
| Build step | Nenhum |

---

## 3. Estrutura de Arquivos

```
/
├── index.html      # página principal com todas as seções
├── robots.txt      # permite indexação, aponta sitemap
└── sitemap.xml     # URL canônica para crawlers e IAs
```

---

## 4. SEO

### Meta tags (no `<head>`)
- `<html lang="pt-BR">`
- `<meta charset="UTF-8">`
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
- `<title>Diego Fernandes — Desenvolvedor Backend PHP | Laravel | Salvador, BA</title>`
- `<meta name="description" content="Desenvolvedor Backend PHP e Laravel Pleno com 6+ anos de experiência em marketplaces, e-commerce e sistemas cloud (GCP, Kubernetes, Docker). Disponível para oportunidades remotas.">`
- `<meta name="robots" content="index, follow">`
- `<link rel="canonical" href="https://<usuario>.github.io/">`

### Open Graph (para LinkedIn e WhatsApp)
- `og:title`, `og:description`, `og:type = "website"`, `og:url`, `og:locale = "pt_BR"`

### Semântica HTML
- Um único `<h1>` no hero com nome completo
- `<h2>` em cada seção (Sobre, Habilidades, etc.)
- `<h3>` nos itens internos (empresas, projetos)
- Tags semânticas: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`
- `id` em cada seção para âncoras de navegação

---

## 5. GEO (Generative Engine Optimization)

### Schema.org JSON-LD (no `<head>`)
Tipo `Person` com:
- `name`, `jobTitle`, `url`, `email`
- `address` (cidade e estado)
- `sameAs`: LinkedIn
- `knowsAbout`: array com todas as tecnologias
- `worksFor`: empresa atual (CVLB)
- `alumniOf`: UFBA, Faculdade Vasco da Gama

### Conteúdo em prosa
- Seção "Sobre" em parágrafos corridos (não só bullets) — IAs extraem entidades de texto corrido mais facilmente
- Cada experiência com uma frase introdutória antes dos bullets

### FAQ no rodapé (oculto visualmente, visível para crawlers)
Perguntas e respostas em `<details>`/`<summary>` ou texto simples:
- "Quais tecnologias Diego Fernandes domina?"
- "Diego Fernandes tem experiência com Kubernetes?"
- "Diego Fernandes está disponível para trabalho remoto?"
- "Qual a experiência de Diego Fernandes com Laravel?"

---

## 6. Design System

### Paleta de cores
| Token | Tailwind class | Hex |
|---|---|---|
| bg-primary | `bg-slate-950` | `#020617` |
| bg-card | `bg-slate-900` | `#0f172a` |
| border | `border-slate-700` | `#334155` |
| text-primary | `text-slate-100` | `#f1f5f9` |
| text-secondary | `text-slate-400` | `#94a3b8` |
| accent | `text-emerald-400` | `#34d399` |
| accent-hover | `text-emerald-300` | `#6ee7b7` |

### Tipografia
- Fonte: **Inter** (Google Fonts)
- h1: `text-5xl md:text-7xl font-bold`
- h2: `text-3xl font-semibold` + borda esquerda emerald
- Corpo: `text-base md:text-lg text-slate-300`

### Componentes reutilizáveis
- **Badge de skill:** `px-3 py-1 rounded-full border border-emerald-400/30 text-emerald-400 text-sm bg-emerald-400/5`
- **Card:** `bg-slate-900 border border-slate-700 rounded-xl p-6 hover:border-emerald-400/50 transition`
- **Botão primário:** `bg-emerald-400 text-slate-950 font-semibold px-6 py-3 rounded-lg hover:bg-emerald-300 transition`
- **Botão outline:** `border border-emerald-400 text-emerald-400 px-6 py-3 rounded-lg hover:bg-emerald-400/10 transition`

---

## 7. Seções — Conteúdo e Layout

### 7.1 `<nav>`
- Fixo no topo (`sticky top-0 z-50`)
- Fundo: `bg-slate-950/90 backdrop-blur`
- Links: Sobre · Habilidades · Experiência · Projetos · Formação · Contato
- Mobile: menu hamburguer com toggle JS
- Logo/nome à esquerda: "Diego Fernandes" em emerald

### 7.2 Hero (`#inicio`)
- Full-viewport height (`min-h-screen`)
- Fundo: grade SVG sutil sobre slate-950
- Conteúdo centralizado:
  - Pill badge: `Disponível para oportunidades`
  - `<h1>`: "Diego Fernandes"
  - Subtítulo: "Desenvolvedor Backend PHP · Laravel · Pleno"
  - Tagline: "Construo sistemas robustos em PHP e Laravel com foco em qualidade, observabilidade e entrega."
  - Dois botões: [LinkedIn ↗] [Enviar e-mail]
  - Seta de scroll animada no rodapé

### 7.3 Sobre (`#sobre`)
- Dois painéis no desktop, empilhados no mobile
- **Esquerda:** 3 parágrafos em prosa (resumo profissional)
- **Direita:** 4 stat cards com número grande em emerald:
  - `6+` Anos de experiência
  - `10+` Projetos entregues
  - `5` Empresas
  - `3` Stacks de cloud

### 7.4 Habilidades (`#habilidades`)
- Grid de categorias, cada uma com título e badges:
  - **Backend:** PHP 8+, Laravel, Eloquent ORM, RESTful API, Queue Jobs, MVC
  - **Cloud & Infra:** GCP, Kubernetes, Docker, Cloud Functions, Digital Ocean, CI/CD
  - **Banco de Dados:** MySQL, MongoDB, BigQuery
  - **Observabilidade:** Datadog, Grafana, Sentry, Bugsnag
  - **Automação & Ferramentas:** N8N, Git, GitLab, GitHub, Jira, Kanban
  - **Boas Práticas:** Clean Code, SOLID, Code Review

### 7.5 Experiência (`#experiencia`)
- Timeline vertical com linha esquerda em emerald
- Ordem cronológica reversa (mais recente primeiro)
- Cada item:
  - Dot na linha emerald
  - Empresa + cargo (h3) + período (slate-400)
  - Badge de tipo: `Pleno`, `Júnior`, `Freelancer`, `Estágio`, `Trainee`
  - Bullets principais (3-4 por empresa)
  - Badge de stack no rodapé do card

**Empresas (do mais recente):**
1. Grupo CVLB — Backend Pleno (jul/2023–presente)
2. Agência NBZ — Backend Pleno Freelancer (mar/2022–ago/2026)
3. VX Case — Backend Júnior (fev/2021–set/2022)
4. Retriever Marketplace — Full Stack Freelancer (out/2020–set/2022)
5. Versatte Marketplace — PHP Freelancer (mar/2020–dez/2020)
6. INTERFACE — Sistemas Estágio (out/2019–mar/2020)
7. InfoJr UFBA — Trainee → Vice-presidente (ago/2017–dez/2019)

### 7.6 Projetos (`#projetos`)
- Grid de 3 cards
- Cada card:
  - Título do projeto (h3)
  - Contexto (empresa)
  - Descrição em 2-3 frases
  - Badges de stack
  - Sem link externo por enquanto (placeholder "Em breve no GitHub")

**Projetos:**
1. **RetrieverApp** — Marketplace de serviços e produtos para pets. PHP, Laravel, MySQL, Docker, Digital Ocean.
2. **Versatte Marketplace** — Marketplace do zero com checkout PagarmE, SEO e e-mail transacional. Laravel, Sentry.
3. **Infraestrutura CVLB** — Cluster Kubernetes no GCP com observabilidade via Datadog e Grafana, automações N8N. GCP, K8s, Datadog.

### 7.7 Formação (`#formacao`)
- Lista vertical com cards simples:
  - 🎓 Pós-Graduação em Engenharia de Software — Pitágoras Unopar Anhanguera (Em andamento, conclusão abr/2027)
  - 🎓 Ciência da Computação — UFBA (Não concluído)
  - 🎓 Ciências Contábeis — Faculdade Vasco da Gama (Concluído 2017)
  - 🏆 Semana OmniStack 11 — Rocketseat

### 7.8 Contato (`#contato`)
- Seção centralizada, fundo card slate-900
- Título: "Vamos trabalhar juntos?"
- Subtítulo: "Aberto a oportunidades remotas ou híbridas como Desenvolvedor Backend Pleno."
- Dois botões grandes:
  - [✉ diegofernandes.dev@gmail.com]
  - [in LinkedIn]

### 7.9 Footer
- Texto simples: "© 2026 Diego Fernandes · Feito com HTML e Tailwind CSS"
- FAQ oculto visualmente mas no DOM para crawlers (FAQ GEO)

---

## 8. JavaScript (vanilla, ~50 linhas)

- **Menu mobile:** toggle classe `hidden` no menu ao clicar no hamburguer
- **Scroll suave:** `scroll-behavior: smooth` via CSS + offset para nav fixo
- **Animação de entrada:** `IntersectionObserver` para fade-in das seções ao scrollar
- **Ano dinâmico:** footer `© <ano atual>` via `new Date().getFullYear()`

---

## 9. robots.txt

```
User-agent: *
Allow: /
Sitemap: https://<usuario>.github.io/sitemap.xml
```

---

## 10. sitemap.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://<usuario>.github.io/</loc>
    <lastmod>2026-09-28</lastmod>
    <priority>1.0</priority>
  </url>
</urlset>
```

---

## 11. Checklist pré-deploy

- [ ] Substituir `<usuario>` pelo username real do GitHub nas URLs
- [ ] Testar em mobile (320px, 375px, 768px)
- [ ] Validar Schema.org em https://validator.schema.org/
- [ ] Verificar meta tags com https://metatags.io/
- [ ] Habilitar GitHub Pages (Settings → Pages → branch main / root)
- [ ] Submeter URL ao Google Search Console
