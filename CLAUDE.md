# Top Achados da Babi — Contexto para Claude Code

## O projeto
Site de nicho de produtos infantis que exibe artigos para bebês da Amazon.
Visitantes chegam ao site, descobrem produtos e são direcionados à Amazon
via links de afiliado com comissão.

## Identidade
- **Nome:** Top Achados da Babi
- **Slogan:** Os melhores achados para o seu bebê
- **Nicho:** Produtos infantis — brinquedos, fraldas, mamadeiras, pomadas
- **Partner Tag:** topachadosdab-20
- **Paleta:** rose/pink — #F43F5E (rose-500), branco, cinza-claro
- **Tom de voz:** acolhedor, prático, confiável para pais e mães

## Regras inegociáveis
- NUNCA usar web scraping — apenas Amazon PA-API oficial
- NUNCA commitar .env ou arquivos .db
- Todos os links de produto DEVEM conter `tag=topachadosdab-20`
- Disclosure de afiliado em TODAS as páginas (ver frase abaixo)
- Preços devem mostrar "atualizado em [timestamp]"

## Frase de disclosure obrigatória (rodapé de todas as páginas)
"Como Associada Amazon, ganho comissões com compras qualificadas."

## Busca de produtos
A PA-API usa busca por KEYWORD (não browse_node_id).
Cada categoria tem um campo "keywords" no config.json.

## Stack
- Fase 1: HTML puro + Tailwind CSS via CDN
- Fase 2+: Python 3, Flask, Jinja2, SQLite, Render.com

## Como rodar (Fase 2+)
- App: python3 run.py
- Fetch manual: python3 scripts/fetch_products.py
- Admin: streamlit run admin/app.py

## Fase atual
Atualizar este campo conforme avança:
- [x] Fase 1 — Site estático no ar (scaffold implementado; falta publicar no
      GitHub Pages e inserir 5+ produtos reais com links de afiliado manuais)
- [ ] Fase 2 — Flask no Render (BLOQUEADA — requer credenciais PA-API após 3 vendas)
- [ ] Fase 3 — Admin e editorial (BLOQUEADA — requer Fase 2 no ar)

## Notas de execução
- A Fase 2 (`app/`, `scripts/`, `render.yaml`, `requirements.txt`) só deve ser
  implementada quando `AMAZON_ACCESS_KEY` e `AMAZON_SECRET_KEY` estiverem em mãos.
- Os cards em `static_site/index.html` são exemplos (template). Substitua o
  `ASIN_AQUI` e os dados por produtos reais com links gerados via SiteStripe
  ou o Link Builder do painel de Associados. Todo link precisa de `tag=topachadosdab-20`.
