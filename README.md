# Selic em dezembro: manter, cortar ou elevar?

Painel interativo, em um único arquivo HTML, que organiza os dados disponíveis até 17/11/2026 para responder a uma pergunta: **o que a Selic deveria fazer na reunião do Copom de 8 e 9 de dezembro de 2026?**

> **Aviso:** projeto acadêmico, sem fins lucrativos (Data Science III, IDP). **Não é um produto oficial do Banco Central do Brasil.** A identidade visual (cores e tipografia) é inspirada no Manual da Marca do BCB. O simulador é aritmético e não é previsão.

## Como abrir

Não há instalação, build nem dependências. Basta abrir `painel_selic_copom_v9.html` em qualquer navegador moderno.

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
- **IPCA acumulado no ano** (jan–out/26) contra o mesmo período de 2025.

### Atividade
Gráficos de **desemprego**, **PIB trimestral** e **PIB esperado** (Focus). Nenhum número é digitado: o navegador lê as APIs do IBGE (SIDRA 6381 e 5932) e do BCB (Focus) ao abrir a aba.

### Decisão
- Três colunas com os argumentos **para manter**, **para cortar** e **para elevar**.
- **Simulador da decisão de 9 de dezembro**: escolha entre cortar 0,75 p.p. e elevar 0,75 p.p., passando por manter e controles para IPCA esperado de 2027 e Selic no fim de 2027. Mostra a Selic após a decisão, o juro real ex-post, o juro real ex-ante e o juro real no fim de 2027. É possível fixar um cenário para comparar.
- Tabela com **todas as opções lado a lado** e gráfico do juro real ex-post na história desde jan/19.
- **Indicadores frente à referência** e **histórico das decisões do Copom**, de 2019 a 2026, com filtro por cortes, manutenções e altas.

### Sobre o painel
Definição das métricas, limitações, bases para baixar, bases oficiais e nota sobre o uso de IA.

## Como as métricas são calculadas

| Métrica | Cálculo |
|---|---|
| IPCA 12 meses | inflação acumulada, composta a partir dos 12 IPCAs mensais |
| Teto e piso | meta do CMN ± 1,5 p.p. (teto 4,5% e piso 1,5% em 2026) |
| Juro real ex-post | (1 + Selic) ÷ (1 + IPCA 12m) − 1 |
| Juro real ex-ante | (1 + Selic) ÷ (1 + IPCA esperado para 2027) − 1, com a mediana do Focus ou o valor dos controles do simulador |
| Impacto por grupo (p.p.) | variação × peso do grupo; a soma dá o IPCA do mês |

A Selic de cada mês é a meta em vigor no último dia do mês. Nas decisões do Copom, o IPCA usado é o último divulgado até a reunião.

## Fontes de dados

| Dado | Fonte |
|---|---|
| IPCA mensal e grupos | IBGE, SIDRA tabela 1737 e publicação do IPCA de outubro/2026 · BCB, série 433 |
| Selic meta | BCB, série 432 (dados abertos) |
| Decisões e projeções do Copom | BCB, atas do Copom (282ª reunião) e histórico das taxas de juros |
| Expectativas de mercado | BCB, Relatório Focus (13/11/2026) |
| Metas de inflação | BCB, histórico das metas |
| Desemprego | IBGE, SIDRA tabela 6381 (PNAD Contínua trimestral) |
| PIB trimestral | IBGE, SIDRA tabela 5932 |

## Limitações

- O simulador é aritmético: não modela como a Selic afeta inflação, câmbio ou atividade.
- O juro real ex-post olha o passado. O ex-ante depende do Focus, que muda toda semana.
- Caso único (Brasil, uma decisão): não há comparação com outros bancos centrais.
- Dados até 17/11/2026.

## Estrutura técnica

- Um único arquivo HTML com CSS e JavaScript embutidos, sem framework nem biblioteca externa.
- Gráficos em **SVG escrito à mão** (função `chart()` para linhas e `bars()` para barras horizontais), com dica de valores ao passar o mouse.
- Abas em seções `<section class="page">`. Layout em CSS Grid, com uma coluna em telas abaixo de 1000 px.
- Tema claro e escuro.

## Histórico de versões

- **v7:** identidade visual inspirada no Manual da Marca do BCB, animações, interatividade e gráficos de desemprego, PIB e PIB esperado lidos das APIs.
- **v8:** layout espalhado pela tela, com gráficos e cartões lado a lado em vez de centralizados. Também:
  - faixa do IPCA em largura total no Panorama, com os três indicadores em linha;
  - rótulos de data do eixo mais espaçados e rótulo do IPCA sem sobreposição ao do teto;
  - barras de expectativas só com a linha da meta;
  - média do juro real descrita ao lado dos botões, fora do gráfico.
- **v9:** remoção dos blocos "Conferência dos números principais" e "Auditar com o Banco Central agora" da aba Sobre o painel, junto com o código da auditoria ao vivo. O título da página (aba do navegador) passou a ser "Painel Selic".

  Dados e cálculos não mudaram em relação à v7.

## Uso de IA

O Claude (Anthropic) localizou e leu as publicações do IBGE e do BCB, transcreveu os valores para o código e escreveu a estrutura do painel. Não gerou nem estimou nenhum dado. A verificação final e a responsabilidade pelos números são do autor.

## Licença

Defina a licença antes de publicar (por exemplo, MIT). Os dados pertencem ao IBGE e ao Banco Central do Brasil.
