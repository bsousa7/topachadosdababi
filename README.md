# 🍼 Top Achados da Babi

Site de nicho de **produtos infantis** (fraldas, mamadeiras, pomadas, brinquedos e mais)
que apresenta artigos para bebês da Amazon Brasil e direciona o visitante à compra via
links de afiliado.

- **Slogan:** Os melhores achados para o seu bebê
- **Partner Tag:** `topachadosdab-20`
- **Stack:** HTML + Tailwind (Fase 1) · Python/Flask/SQLite/Render (Fase 2+)

---

## Arquitetura em duas etapas

A **PA-API da Amazon exige qualificação** (conta Associate com pelo menos 3 vendas), então
o projeto avança em fases:

| Fase | O que é | Depende de | Status |
|------|---------|-----------|--------|
| **1** | Site estático no GitHub Pages, com links de afiliado gerados **manualmente** (SiteStripe / Link Builder) | Conta Associate aprovada | ✅ Scaffold pronto |
| **2** | App Flask que busca produtos por keyword via PA-API e os serve dinamicamente (Render.com) | 3 vendas + credenciais PA-API | ⛔ Bloqueada |
| **3** | Painel admin em Streamlit (dashboard, histórico de preços, config) | Fase 2 no ar | ⛔ Bloqueada |

> A Fase 1 **já gera comissão** com links manuais. A PA-API só é necessária para automatizar
> a busca de produtos, o que acontece na Fase 2.

---

## Estrutura

```
topachadosdababi/
├── CLAUDE.md                 # contexto do projeto para o Claude Code
├── README.md
├── .gitignore
├── config/
│   └── config.json           # site, categorias e keywords (usado na Fase 2)
├── static_site/              # Fase 1 — site estático (GitHub Pages)
│   ├── index.html
│   ├── sobre.html
│   ├── politica-de-privacidade.html
│   ├── robots.txt
│   └── assets/style.css
├── app/                      # Fase 2 — Flask (a implementar com credenciais PA-API)
├── scripts/                  # Fase 2 — fetch_products.py (a implementar)
└── data/                     # Fase 2 — SQLite (não commitado)
```

---

## Fase 1 — como colocar no ar

1. **Publique no GitHub Pages:** Settings → Pages → *Deploy from a branch* →
   branch `main`, pasta `/static_site`. A URL fica
   `https://SEU_USUARIO.github.io/topachadosdababi`.
2. **Adicione produtos reais** em `static_site/index.html`: para cada produto, gere o link
   de afiliado pela barra **SiteStripe** (opção "Texto") ou pelo **Link Builder** do painel de
   Associados, e substitua nos `<article>` de exemplo: `href`, imagem, título, preço e desconto.
   Todo link precisa conter `tag=topachadosdab-20` e `rel="noopener sponsored"`.
3. **Submeta a URL** no cadastro do Amazon Associates e divulgue o site para gerar as
   primeiras visitas e vendas.

> **Portão de qualificação:** só avance para a Fase 2 com conta Associate ativa, site no ar,
> 3 vendas qualificadas e as credenciais PA-API (`Access Key ID` + `Secret Access Key`) em mãos.

---

## Fase 2+ (bloqueada até a qualificação)

Quando as credenciais PA-API chegarem, implementar `app/` (Flask + Jinja2), `scripts/fetch_products.py`,
`requirements.txt` e `render.yaml` conforme o plano do projeto, e criar um `.env` (nunca commitado)
com as variáveis:

```env
AMAZON_ACCESS_KEY=
AMAZON_SECRET_KEY=
AMAZON_PARTNER_TAG=topachadosdab-20
AMAZON_HOST=webservices.amazon.com.br
AMAZON_REGION=us-east-1
SECRET_KEY=   # python3 -c "import secrets; print(secrets.token_hex(32))"
```

---

## Conformidade Amazon Associates

- Disclosure *"Como Associada Amazon, ganho comissões com compras qualificadas."* no rodapé de **todas** as páginas.
- Links de produto sempre com `tag=topachadosdab-20` e `rel="noopener sponsored"`.
- Apenas PA-API oficial na Fase 2 — **nunca** web scraping.
- Preços com timestamp de atualização (Fase 2).
- Páginas `/sobre` e `/politica-de-privacidade` ativas; site indexável.
