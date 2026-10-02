# DashLogisticaHTML.BI

Dashboard Logística 
Stack: Power BI + DAX + HTML/CSS/JS (client-side)

Medidas
Medida	Função
JSON Gold Dashboard Logistica	Fonte única de dados
HTML Filtros Dashboard Logistica	5 filtros + Limpar + Dark/Light
HTML Dashboard Logistica	KPIs, gráfico, rankings, tabela
Fluxo
Filtros → evento ld-filter-change → Dashboard recalcula em JS.

Fonte
baseInterativa do JSON Gold: m, r, t, o, c, pr, qt, p, q, qe, cp, lt, ln, co, at, an, dv, av, ex.

Como usar
Crie as 3 medidas (formato Texto).

Visual HTML Content para cada uma, na mesma página.

Filtros no topo, dashboard abaixo.

Recursos
Filtros combinados + persistência (sessionStorage)

Tema Dark/Light · Tooltip própria · Estado vazio

Tabela ordenável · aria-sort · prefers-reduced-motion

Zero CDN/API/biblioteca

Limitações
Filtragem é client-side (DAX não filtra modelo)

Depende do JSON Gold trazer baseInterativa completa

Slicers nativos só funcionam com ponte data-ld-slicer

Regras preservadas
OTIF = On Time e In Full no mesmo pedido · pendentes ficam na fato · lead time só em entregues · percentuais 0–100%.
