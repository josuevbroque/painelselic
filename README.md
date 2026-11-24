# Selic em dezembro: manter, cortar ou elevar?

Painel interativo, em um único arquivo HTML, para **um(a) diretor(a) do Banco Central com voto no Copom** decidir o que fazer com a Selic na reunião de **8 e 9 de dezembro de 2026**. Reúne os dados disponíveis até **17/11/2026**.

> **Aviso:** projeto acadêmico, sem fins lucrativos (Data Science III, IDP). **Não é um produto oficial do Banco Central do Brasil.** A identidade visual (cores e tipografia) é inspirada no Manual da Marca do BCB. O simulador é aritmético e não é previsão.

## Como abrir

Não há instalação, build nem dependências. Basta abrir `index.html` em qualquer navegador moderno.

- A aba **Atividade** consulta as APIs do IBGE e do BCB quando é aberta, então precisa de internet. Sem conexão, mostra a última cópia salva no navegador, se houver.
- As fontes (Google Fonts) também são carregadas da internet. Sem elas, o painel usa fontes do sistema.

## O que tem em cada aba

### Panorama
- Faixa de destaque com o **IPCA em 12 meses** (4,63% em out/26) e sua posição em relação ao piso (1,5%), à meta (3,0%) e ao teto (4,5%).
- Três indicadores: **Selic meta**, **juro real ex-post** e **IPCA esperado para 2027** (Focus).
- **Seletor de período** (botões e controle deslizante) que redefine os dois gráficos ao lado.
- Gráfico do **IPCA em 12 meses com a banda da meta** e gráfico da **Selic meta e do juro real ex-post**, com a média do período indicada.

### Pressões
- **O que moveu o IPCA de outubro, por grupo**, em impacto no índice (p.p.) ou em variação do grupo (%).
- **IPCA esperado pelo mercado** (Focus, 13/11) para 2026, 2027 e 2028.
- **IPCA projetado pelo Copom** (reunião de 4/11, cenário de referência) para 2026, 2027 e 2º tri/2028.

### Atividade
Gráficos de **desemprego**, **PIB trimestral** e **PIB esperado** (Focus). Nenhum número é digitado: o navegador lê as APIs do IBGE (SIDRA 6381 e 5932) e do BCB (Focus) ao abrir a aba. O PIB pode ser visto contra o mesmo trimestre do ano anterior ou contra o trimestre anterior, com ajuste sazonal.

### Decisão
- Três colunas com os argumentos **para manter**, **para cortar** e **para elevar**.
- **Simulador da decisão de 9 de dezembro**: escolha entre cortar 0,75 p.p. e elevar 0,75 p.p., passando por manter, com controles para o IPCA esperado de 2027 e a Selic no fim de 2027. Mostra a Selic após a decisão, o juro real ex-post, o juro real ex-ante e o juro real no fim de 2027. É possível fixar um cenário para comparar.
- Tabela com **todas as opções lado a lado** e gráfico do juro real ex-post na história desde jan/19.
- **Indicadores frente à referência** e **histórico das decisões do Copom**, de 2019 a 2026, com filtro por cortes, manutenções e altas e detalhe ao clicar em uma reunião.

### Sobre o painel
Definição das métricas, limitações, conferência dos números, bases para baixar, bases oficiais e nota sobre o uso de IA.

## Como as métricas são calculadas

| Métrica | Cálculo |
|---|---|
| IPCA 12 meses | inflação acumulada, composta a partir dos 12 IPCAs mensais |
| Teto e piso | meta do CMN ± 1,5 p.p. (teto 4,5% e piso 1,5% em 2026) |
| Juro real ex-post | (1 + Selic) ÷ (1 + IPCA 12m) − 1 |
| Juro real ex-ante | (1 + Selic) ÷ (1 + IPCA esperado para 2027) − 1, com a mediana do Focus ou o valor dos controles do simulador |
| Impacto por grupo (p.p.) | variação × peso do grupo; a soma dá o IPCA do mês |
| Selic meta | taxa básica de juros fixada pelo Copom, em % ao ano; é a variável da decisão |
| Projeção do Copom | IPCA acumulado em quatro trimestres no cenário de referência da ata (2026, 2027 e 2º tri/2028, o horizonte relevante) |
| Focus | mediana das projeções do mercado, coletadas pelo Banco Central |
| Desemprego | taxa de desocupação da PNAD Contínua, em trimestre móvel |
| PIB | variação do volume do PIB trimestral (IBGE) |
| PIB esperado | mediana do Focus para a variação do PIB no ano |

O IPCA 12m é **calculado**, não copiado: como os mensais são arredondados, o resultado pode diferir em 0,01 p.p. do 12m publicado pelo IBGE (fev/20: 4,00% vs. 4,01%; dez/22: 5,78% vs. 5,79%).

A Selic de cada mês é a meta em vigor no último dia do mês. Nas decisões do Copom, o IPCA usado é o último divulgado até a reunião (exceção: 09/12/2020, pois o IPCA de nov/20 foi divulgado em 08/12/2020).

## Fontes de dados

Dados até **17/11/2026**. Fontes acessadas e conferidas em **25/11/2026**.

| Dado | Fonte |
|---|---|
| IPCA mensal e grupos | [IBGE, SIDRA 1737](https://sidra.ibge.gov.br/tabela/1737) · [IPCA e INPC de outubro/2026 (PDF)](https://biblioteca.ibge.gov.br/visualizacao/periodicos/236/inpc_ipca_2026_out.pdf) · [BCB, série 433 (JSON)](https://api.bcb.gov.br/dados/serie/bcdata.sgs.433/dados?formato=json&dataInicial=01/01/2018&dataFinal=17/11/2026) |
| Selic meta | [BCB, dados abertos, série 432](https://dadosabertos.bcb.gov.br/dataset/432-taxa-de-juros---meta-selic-definida-pelo-copom) · [JSON](https://api.bcb.gov.br/dados/serie/bcdata.sgs.432/dados?formato=json&dataInicial=01/01/2019&dataFinal=17/11/2026) |
| Decisões do Copom | [BCB, histórico das taxas de juros](https://www.bcb.gov.br/controleinflacao/historicotaxasjuros) |
| Projeções e votação | [BCB, ata da 282ª reunião (PDF)](https://www.bcb.gov.br/content/copom/atascopom/Copom282-not20261104282.pdf) |
| Expectativas de mercado | [BCB, Focus de 13/11/2026 (PDF)](https://www.bcb.gov.br/content/focus/focus/R20261113.pdf) · [Relatório Focus](https://www.bcb.gov.br/publicacoes/focus) |
| Metas de inflação | [BCB, histórico das metas](https://www.bcb.gov.br/controleinflacao/historicometas) |
| Desemprego | [IBGE, SIDRA 6381](https://sidra.ibge.gov.br/tabela/6381) · [release de 30/10/2026](https://agenciadenoticias.ibge.gov.br/agencia-sala-de-imprensa/2013-agencia-de-noticias/releases/48409-30-10-release) · [PNAD Contínua trimestral](https://www.ibge.gov.br/estatisticas/sociais/trabalho/9173-pesquisa-nacional-por-amostra-de-domicilios-continua-trimestral.html?lang=pt-BR) |
| PIB trimestral | [IBGE, SIDRA 5932](https://sidra.ibge.gov.br/tabela/5932) · [release de 01/09/2026](https://agenciadenoticias.ibge.gov.br/agencia-sala-de-imprensa/2013-agencia-de-noticias/releases/47902-pib-cresce-0-5-no-segundo-trimestre-de-2026) |

Conferência: os 106 valores mensais do IPCA foram comparados um a um com a série 433; as 63 decisões do Copom (datas e metas) com a série 432 e com a tabela de histórico de taxas de juros do BCB; Focus, grupos do IPCA, desemprego e PIB com os PDFs e releases acima.

## Limitações

- O simulador é aritmético: não modela como a Selic afeta inflação, câmbio ou atividade, e não é previsão.
- O juro real ex-post olha o passado. O ex-ante depende do Focus, que muda toda semana.
- Caso único (Brasil, uma decisão): não há comparação com outros bancos centrais.
- Os gráficos da aba Atividade dependem das APIs do IBGE e do BCB no momento em que a aba abre.
- Dados até 17/11/2026.

## Estrutura técnica

- Um único arquivo HTML com CSS e JavaScript embutidos, sem framework nem biblioteca externa.
- Gráficos em **SVG escrito à mão** (`chart()` para linhas, `bars()` para barras horizontais), com dica de valores ao passar o mouse.
- Abas em seções independentes; layout em CSS Grid, que colapsa para uma coluna em telas estreitas.
- **Tema claro e escuro.**
- As séries embutidas podem ser exportadas em CSV pela aba "Sobre o painel".

## Uso de IA

Assistentes de IA foram usados em duas etapas. O Claude (Anthropic) localizou e leu as publicações do IBGE e do BCB, transcreveu os valores para o código, montou a estrutura e escreveu o código, incluindo a identidade visual inspirada no Manual da Marca do BCB, as animações, a interatividade e os gráficos de desemprego, PIB e PIB esperado, que leem as APIs oficiais no navegador e não trazem número digitado. Nenhum dado foi gerado ou estimado por IA.

A conferência dos números contra as fontes primárias foi feita em 25/11/2026 com assistência do Qwen, em várias rodadas, e o autor revisou os resultados. A responsabilidade final pelos dados é do autor.
