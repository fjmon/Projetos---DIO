[README.md](https://github.com/user-attachments/files/33283989/README.md)
# Porsche Sales Intelligence --- Dashboard Executivo

## 1. Visão geral

Este projeto apresenta um dashboard executivo de vendas da Porsche,
desenvolvido em HTML, CSS e JavaScript, com visual escuro (*dark mode*)
e gráficos interativos. A proposta foi reunir indicadores comerciais e
análises por produto, localização, ano-modelo e método de pagamento em
uma única tela.

A interface foi inspirada em painéis automotivos premium e na linguagem
visual minimalista indicada como referência. O dashboard é uma página
HTML independente; os dados da planilha estão incorporados no próprio
arquivo, enquanto a biblioteca Chart.js é carregada por CDN.

## 2. Perguntas de negócio escolhidas e justificativas

### 2.1. Quais modelos e anos-modelo concentram o maior volume de vendas?

**Por que foi escolhida:** permite identificar os modelos com maior
procura e os anos-modelo que aparecem com mais frequência na base. Isso
ajuda a entender o mix de produtos e a destacar os veículos de maior
volume.

**Como foi representada:** - Ranking de modelos mais vendidos, em barras
horizontais, que facilita comparar nomes de modelos e ordenar as
categorias. - Gráfico por ano-modelo, com volume de vendas e
faturamento. - Indicadores de destaque que mostram o modelo e o
ano-modelo líderes na seleção atual.

### 2.2. Como o volume e o faturamento se distribuem por cidade e estado?

**Por que foi escolhida:** a visão geográfica ajuda a comparar mercados,
identificar localidades com maior atividade e observar se uma cidade se
destaca em volume, faturamento ou ambos.

**Como foi representada:** - Gráfico de faturamento e volume por
cidade. - Tabela regional por estado com quantidade de registros,
faturamento, ticket médio e modelo líder.

A combinação de gráfico e tabela permite uma leitura rápida e, em
seguida, uma comparação mais detalhada.

### 2.3. Como as vendas se distribuem por faixa de preço e quais modelos se destacam?

**Por que foi escolhida:** as faixas de preço mostram em quais
intervalos se concentra a base analisada. Em conjunto com o ranking de
modelos e a análise regional, ajudam a contextualizar o perfil comercial
das vendas.

**Como foi representada:** - Gráfico de colunas por faixa de preço:
abaixo de US\$ 75 mil, US\$ 75--100 mil, US\$ 100--150 mil, US\$
150--200 mil e US\$ 200 mil ou mais. - Ranking de modelos. - Modelo
líder por estado na tabela regional.

As faixas são agrupamentos analíticos para facilitar a leitura, não
categorias oficiais da Porsche.

### 2.4. Qual é a relação entre preço/modelo e método de pagamento?

**Por que foi escolhida:** permite observar a participação dos métodos
de pagamento e cruzar essa informação com os filtros de modelo, ano e
localidade. É uma leitura exploratória do comportamento registrado na
base, não uma explicação causal sobre a escolha de pagamento.

**Como foi representada:** - Gráfico de rosca com a participação de cada
método no volume filtrado. - Filtros interativos para restringir a
análise por modelo, ano-modelo e cidade. - Indicador de método de
pagamento mais utilizado na seleção atual.

## 3. Indicadores e interações

O dashboard contém três KPIs principais:

-   **Faturamento total:** soma dos preços dos registros considerados na
    seleção.
-   **Volume de vendas:** quantidade de registros na seleção.
-   **Ticket médio:** faturamento total dividido pelo volume de
    registros.

No topo, há filtros de **modelo Porsche**, **ano-modelo**, **cidade** e
**método de pagamento**, cada um com a opção "Todos", além do botão
**Limpar filtros**. Ao alterar os filtros, os KPIs, os gráficos, a
tabela regional e os insights são recalculados em tempo real.

> **Nota de interpretação:** na implementação atual, o volume é contado
> como número de registros e o faturamento é calculado pela soma do
> campo de preço. O status da venda não é usado como filtro automático;
> portanto, registros com status como "Cancelled", "Pending" ou "In
> Transit" também podem entrar nos indicadores. Para medir apenas vendas
> concluídas, seria necessário definir uma regra de negócio explícita e
> filtrar os status correspondentes.

## 4. Prompt utilizado e evolução até a versão final

### Prompt inicial

O pedido inicial foi, em essência:

> Aja como especialista sênior em Front-end, BI e UI/UX. Crie um
> dashboard executivo em HTML, com visual sofisticado em tema escuro,
> inspirado no site oficial da BMW Brasil. Use a planilha com 100 vendas
> da Porsche, contendo modelo, cidade, estado, ano, preço e método de
> pagamento. Inclua filtros para modelo, ano-modelo, cidade e método de
> pagamento, com opção "Todos" e botão "Limpar filtros". Os filtros
> devem recalcular os KPIs e gráficos em tempo real. Inclua faturamento
> total, volume de vendas, ticket médio, modelos mais vendidos,
> distribuição por faixa de preço, vendas por cidade/estado e método de
> pagamento. Responda também às perguntas de negócio sobre concentração
> por modelo e ano, desempenho geográfico, faixas de preço e relação
> entre veículos e formas de pagamento.

### O que mudou até a versão final

1.  **Primeira versão:** foi criada uma estrutura visual executiva em
    HTML, com cartões de KPI, gráficos e filtros. Na primeira entrega,
    porém, os dados da planilha não haviam sido incorporados
    corretamente.
2.  **Correção solicitada:** a planilha foi enviada novamente e a versão
    seguinte passou a incorporar os 100 registros diretamente no HTML,
    em uma estrutura de dados JavaScript.
3.  **Versão com dados:** os gráficos e indicadores passaram a ser
    calculados a partir dos registros incorporados. Foram mantidos os
    filtros dinâmicos, a opção "Todos" e o botão de limpeza.
4.  **Refinamento analítico:** a versão final inclui também uma tabela
    regional por estado e blocos de insights calculados de acordo com a
    seleção atual, além dos gráficos de modelos, faixas de preço,
    pagamentos, cidades e ano-modelo.
5.  **Tratamento de moeda:** os preços foram exibidos em dólares
    americanos (USD), coerentemente com os valores e localidades
    presentes na base, sem conversão cambial.

O prompt evoluiu, portanto, de uma especificação principalmente visual e
funcional para uma instrução que também exigia verificar a incorporação
efetiva dos dados e recalcular todas as visualizações a partir deles.

## 5. Preparação e tratamento da base antes de enviar à IA

A base foi preparada manualmente antes de ser utilizada na geração do
dashboard. O tratamento realizado foi:

-   **Sanitização dos nomes das colunas:** os cabeçalhos foram
    padronizados para facilitar o uso no código.
-   **Conversão dos campos numéricos:** preço e ano-modelo foram
    convertidos para números, evitando que fossem interpretados como
    texto.
-   **Colagem como valores:** as fórmulas foram substituídas por seus
    valores calculados, para impedir que referências ou fórmulas
    quebradas fossem levadas à análise.
-   **Revisão da estrutura:** a planilha foi organizada para que os
    campos necessários à análise estivessem disponíveis como colunas de
    dados.

Esse preparo é importante porque a IA e o código de visualização
precisam receber campos consistentes para somar preços, contar
registros, ordenar anos e agrupar categorias. A sanitização de
cabeçalhos e a conversão numérica também reduzem ambiguidades na
interpretação dos dados.

**Limitação conhecida:** a coluna de data contém valores inválidos em
alguns registros, como `INVALID`. Como os gráficos finais não dependem
diretamente da data da venda, essa coluna não foi usada para construir
uma série temporal por data. O gráfico temporal apresentado é por
**ano-modelo**, que é diferente do ano em que a venda aconteceu.

## 6. Ferramentas utilizadas: ChatGPT, Canvas ou agente com skill?

O trabalho foi feito com **ChatGPT**, a partir das instruções em
linguagem natural e do arquivo Excel anexado. O resultado foi gerado
como um arquivo HTML com CSS e JavaScript, usando a biblioteca
**Chart.js** para os gráficos interativos.

-   **ChatGPT:** sim, foi utilizado para interpretar os requisitos,
    propor indicadores e visualizações e produzir o arquivo.
-   **HTML/CSS/JavaScript e Chart.js:** sim, compõem a implementação do
    dashboard.
-   **Agente com skill especializada:** não foi utilizado um agente
    separado com uma skill específica de BI ou front-end.
-   **Canvas do ChatGPT:** embora o pedido inicial mencionasse Canvas, a
    entrega final foi um arquivo HTML autônomo. Portanto, a forma mais
    precisa de descrever a solução é **dashboard HTML criado com auxílio
    do ChatGPT**, e não um relatório nativo do Power BI nem
    necessariamente um artefato construído dentro do Canvas.

A biblioteca Chart.js é carregada por CDN, então é necessária conexão
com a internet para que os gráficos sejam renderizados. Os dados, por
outro lado, estão embutidos no arquivo HTML.

## 7. Como executar

1.  Baixe o arquivo `porsche_executive_dashboard_com_dados.html`.
2.  Abra-o em um navegador moderno, como Google Chrome ou Microsoft
    Edge.
3.  Use os filtros no topo para explorar diferentes seleções.
4.  Clique em **Limpar filtros** para voltar à visão completa da base.

Não é necessário instalar o Power BI para visualizar esta versão HTML.

## 8. Limitações e possíveis melhorias futuras

-   Definir formalmente quais status representam uma venda concluída e
    disponibilizar um filtro de status.
-   Tratar ou documentar os valores inválidos da coluna de data.
-   Acrescentar filtros de estado e status, caso sejam relevantes para
    os usuários.
-   Incluir uma análise temporal por data da venda depois de corrigir os
    valores inválidos.
-   Acrescentar métricas de participação percentual e comparações entre
    períodos, se a base tiver datas confiáveis.
-   Validar os resultados dos KPIs com uma conferência independente da
    planilha.

## 9. Arquivo principal

`porsche_executive_dashboard_com_dados.html` --- dashboard executivo
interativo com os registros incorporados.
