# DashLogisticaHTML.BI

README — Dashboard Logística (Power BI + HTML/DAX)
🎯 Objetivo
Dashboard executivo de logística no Power BI, com filtros internos em HTML que recalculam tudo client-side, a partir do [JSON Gold Dashboard Logistica].

🧱 Arquitetura em 3 camadas

Camada	Medida DAX	Função
1. Filtros	HTML Filtros Dashboard Logistica	Renderiza 5 <select> (Mês, Região, Categoria, Transportadora, Modal) + botão Limpar + seletor Dark/Light

2. Dashboard	HTML Dashboard Logistica	Lê o JSON Gold, escuta eventos de filtro e recalcula tudo em JS

3. Dados	JSON Gold Dashboard Logistica	Fonte única, contém meta, kpis, séries, rankings e baseInterativa

🔄 Fluxo de comunicação
text
[Filtros HTML]  --ld-filter-change-->  [Dashboard HTML]

                 --ld-theme-change-->   (recalcula client-side)
                 
Estado persistido em sessionStorage (chave ld-filters-v1)

Filtros externos do Power BI são preservados (o JSON já vem filtrado)

🗂️ Campos esperados em baseInterativa
Campo	Significado
m	Mês (YYYY-MM)
r	Região
t	Transportadora
o	Modal
c	Categoria
pr	Produto
qt	Quantidade
p	Pedidos
q / qe	Pedidos OTIF / elegíveis
cp	Custo logístico
lt / ln	Soma lead time / nº observações
co	Emissões CO₂
at / an	Soma atraso / nº observações
dv / av / ex	Devoluções / avarias / extravios
⚠️ Sem baseInterativa completa, os filtros renderizam mas não recalculam.

🧩 Componentes renderizados
Header com estrada animada + carros

Ticker de top 4 produtos

5 KPI cards (Pedidos, OTIF, Custo, Lead Time, Emissões) com variação vs mês anterior

Gráfico mensal (barras + linha OTIF + mediana tracejada)

Leitura executiva (3 insights dinâmicos)

3 rankings (OTIF por transportadora, custo por região, risco por modal)

Tabela comparativa ordenável por clique

✅ Funcionalidades
Filtros combinados e persistentes

Botão Limpar filtros

Tema Dark / Light

Tooltip HTML própria

Estado vazio em cada bloco

aria-sort, aria-label, aria-live

Respeita prefers-reduced-motion

Zero dependências externas (sem CDN, API ou biblioteca)

🚀 Como usar
Crie as medidas na ordem: JSON Gold → Filtros → Dashboard

Formate todas como Texto

Insira na página:

Visual HTML Content → HTML Filtros Dashboard Logistica (topo)

Visual HTML Content → HTML Dashboard Logistica (abaixo)

Ambos precisam estar na mesma página para os eventos window funcionarem

🧪 Checklist rápido
□ Sem filtros → totais globais corretos
□ Filtro isolado (Mês, Região, Categoria, Transportadora, Modal)
□ Filtros combinados
□ Botão Limpar
□ Alternância Dark/Light
□ Estado vazio
□ Ordenação da tabela
□ Renderização no Power BI (visual HTML Content)
⚠️ Limitações conhecidas
Medida DAX não filtra o modelo — a filtragem é client-side via JS

Depende do JSON Gold conter baseInterativa completa

O Power BI pode re-renderizar o visual ao mudar contexto externo (estado é restaurado via sessionStorage)

Slicers nativos do Power BI não são acionados pelo HTML (a menos que você implemente a ponte com data-ld-slicer)

📌 Regras de negócio preservadas
OTIF exige On Time e In Full no mesmo pedido

Pedidos pendentes permanecem na fato

Lead time só considera entregas concluídas

Pendentes não são classificados como atrasados sem regra confirmada

Percentuais entre 0% e 100%

OTIF ≤ elegíveis ≤ total de pedidos
