# 1. Teste Qui-Quadrado

O teste Qui-Quadrado (ou *Chi-Squared*) mede a relação de dependência entre duas variáveis categóricas.

## 1.1. Variáveis Categóricas

Variáveis categóricas - também conhecidas como __variáveis qualitativas__ - são aquelas que possuem um número finito de categorias (grupos).

Em geral, é bastante comum observarmos seu uso no mercado de trabalho pela presença de variáveis não numéricas ou pelo interesse em agrupar variáveis numéricas em grupos.

# 2. Como o teste funciona

A ideia do teste é medir como os valores esperados se diferenciam dos valores observados. Para isso, um teste de hipótese é realizado.

## 2.1. O teste de hipótese

Para realizar o teste, duas hipóteses complementares são formuladas

$H_0:$ as duas variáveis são independentes

$H_1:$ as duas variáveis não são independentes

<br>

Assim como demais testes de hipótese, o cálculo do teste qui quadrado fornecerá um valor em sua distribuição. A partir deste valor, é possível calcular a probabilidade de observamos esse valor caso a hipótese nula ( $H_0$ ) seja verdadeira.

Por padrão, tanto dentro da academia quanto em aplicações no mercado de trabalho, quando a probabilidade de observarmos $H_0$ é inferior a 0,05, recusamos a hipótese e seguimos com sua complementar.

## 2.2. Tabela de Contingência

Para calcular o valor do teste, utilizamos uma tabela de contingência. A tabela de contingência combina os diferentes valores para cada variável analisada e retorna a ocorrência (contagem) desses valores no seu conjunto de dados.

| gender | Female | Male |
| --- | --- | --- |
| rank_cat |  |  |
| 0-100 | 37 | 63 |
| 101-200 | 41 | 59 |
| 201-300 | 49 | 51 |
| 301-400 | 61 | 39 |
| 401-500 | 77 | 23 |

<br>

Caso as variáveis analisadas sejam independentes, não deveríamos observar uma grande variação entre a proporção dos valores em cada coluna.

Em nosso exemplo, se não há diferença entre ser do gênero feminino ou masculino, a proporção entre pessoas do gênero feminino e do gênero masculino para cada intervalo de ranking deveria ser similar.

Dentro do pacote `pandas`, essa tabela pode ser criada com a função `crosstab`.

## 2.3. Distribuição Qui-Quadrado

A partir da tabela de contingência, podemos calcular o valor qui-quadrado.

$$
Qui-Quadrado = \displaystyle \frac{(observado - esperado)^2}{esperado}
$$

<br>

Para o cálculo do valor esperado, tem-se

Quantidade de pessoas com gênero = feminino: $37 + 41 + 49 + 61 + 77 = 265$

Quantidade de pessoas com gênero = masculino: $63 + 59 + 51 + 39 + 23 = 235$

Quantidade de categorias de rankings: $5$ 

<br>

Valor esperado de pessoas com gênero feminino por ranking: $\displaystyle \frac{265}{5} = 53$

Valor esperado de pessoas com gênero masculino por ranking: $\displaystyle \frac{235}{5} = 47$

<br>

| Variáveis | Valor observado | Valor esperado | Qui-Quadrado |
| --- | --- | --- | --- |
| Female, 0-100 | 37 | 53 | 4,830189 |
| Female, 101-200 | 41 | 53 | 2,716981 |
| Female, 201-300 | 49 | 53 | 0,301887 |
| Female, 301-400 | 61 | 53 | 1,207547 |
| Female, 401-500 | 77 | 53 | 10,86792 |
| Male, 0-100 | 63 | 47 | 5,446809 |
| Male, 101-200 | 59 | 47 | 3,06383 |
| Male, 201-300 | 51 | 47 | 0,340426 |
| Male, 301-400 | 39 | 47 | 1,361702 |
| Male, 401-500 | 23 | 47 | 12,25532 |

Ao somarmos o valor de Qui-Quadrado para todas as combinações de valores das duas variáveis, temos o valor 42,39. 

O valor obtido deve ser comparado com a tabela de distribuição de probabilidade. A título de curiosidade, com um grau de liberdade e um valor crítico definido em 0,05, o valor da distribuição será de 3,841. Como o valor obtido, 42,39, é superior ao valor da distribuição, negaríamos a hipótese nula.

Felizmente, você não precisará se preocupar com nada dito no parágrafo anterior caso não queira.

Ao utilizar os pacotes estatísticos de alguma linguagem de programação, você obterá o **p-valor** (ou *p-value*) e precisará apenas dele para tomar uma decisão quanto a negação (ou não) da hipótese nula. 

# 3. Usos do teste

O teste qui-quadrado é extremamente útil quando trabalhamos com dados categóricos, tanto dentro do contexto de análise quanto de ciência de dados.

## 3.1. Análise Exploratória

Ao utilizar o teste, é possível testar estatisticamente a relação entre grandes quantidades de variáveis com bastante velocidade. Isso te possibilita focar sua atenção nas relações significantes, agregando maior valor a sua análise e fortalecendo seu *storytelling*.

## 3.2. Seleção de Variáveis

A *feature selection* é uma parte importantíssima do desenvolvimento de qualquer modelo. Ao testar a relação entre diferentes variáveis categóricas antes do treino do modelo, é possível apenas utilizar as variáveis que possuem relação com seu *target*, possuindo efeitos positivos em suas métricas de acerto e reduzindo a variância de seus resultados.
