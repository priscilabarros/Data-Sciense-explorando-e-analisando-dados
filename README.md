# Data-Sciense-explorando-e-analisando-dados
Como analisar uma base de dados


## *Preparação do ambiente:*
* Colaboratory: https://colab.research.google.com/drive/1ih47GTjBWveck-FBRsghVzRRMkMuMyXX#scrollTo=I8RRLZwf5zdi

* é uma ferramenta para usar notebooks na nuvem, esta ferramenta é associada à uma conta gmail.

* O notebook criado executa os códigos desejados em uma máquina virtual dedicada a sua conta.

* Restaurar seu notebook:
faça o upload do arquivo .csv e executar as opções "Runtime" e "Restart and run all..."

* Existe um site https://grouplens.org/datasets/movielens/ chamado Movielens que  
disponibiliza avaliações de filmes. Pode ser usado como base de dados para testes.

* CSV - significa (Comma Separator Value) extensão de arquivos muito utilizados para salvar informações a ser trabalhadas para extrair dados. Possui uma extrutura bem simples, somente as informações das colunas separadas por virgulas.

## *Iniciando um projeto:*

* Pandas - biblioteca do python com um módulo que lê arquivos csv. Muito utilizada paratrabalhar com dados.

* Importar a biblioteca pandas usa-se o comando:

´´´
import pandas as pd

´´´
* Para ler um arquivo csv usa-se o comando:

´´´
pd.read_csv("ratings.csv")

´´´
* Para ler um endereço usa-se o comando:
´´´
dados = pd.read_csv("https://raw.githubusercontent.com/alura-cursos/data-science-analise-exploratoria/main/Aula_0/ml-latest-small/ratings.csv")

dados
´´´

* Para que o Jupiter encontre o arquivo que deseja ler, o arquivo deve estar no mesmmo diretório da onde estiver sendo rodado ou deve ser descrito o path de onde o arquivo se encontra.

* Para subir um arquivo no Jupiter o usuário deve clicar no menu lateral, escolher a seção Files, depois fazer o upload do arquivo.

* atribuir as linhas e resultados de dados de um arquivo csv a uma variável com o intuito de não mostrar visualmente o resultado total de linhas do arquivo e facilitar o manejo de dados:

´´´
notas = pd.read_csv("ratings.csv")

´´´ 

* Mostrar as 5 primeiras linhas de um arquivo csv:

```
notas.head()

```

* Mostrar o formato da tabela 

```
notas.shape

```
* Alterar nome de Colunas:
```
notas.columns = ["usuarioId","filmeId","nota","momento"]
``` 
* Valores de uma coluna:
``` 
notas["nota"]
``` 
* Saber quais são os valores unicos dentre uma coluna

``` 
notas['nota'].unique()
``` 

* Media das notas em uma coluna
``` 
notas['nota'].mean()
``` 



* Plotar - imprimir na tela visualmente

``` 
notas.nota.plot() 

``` 

* histograma - distribuição dos valores em um gráfico
``` 
notas.nota.plot(kind='hist')
``` 

* imprimir a mediana:
``` 
print(notas['nota'].mean())

print(notas['nota'].median())

or 
media = notas["nota"].mean()
mediana = notas["nota"].median()
print(f"Media é {media}")
print(f"Mediana é {mediana}")

``` 

* Describe - dá diversas medidas de descrição de forma automatica
``` 
notas.nota.describe()

``` 

* Seaborn - biblioteca de visualizações do panda
``` 
import seaborn as sns
``` 

* Boxplot - mostra visualmente as informações do describe
``` 
sns.boxplot(notas.nota)
``` 

* Query - para cruzar informações entre colunas é necessário fazer uma query. Por exemplo saber a nota de um determinado filme:
``` 
notas.query("filmeId==1").nota
notas.query("filmeId==1").nota.mean()
``` 

* Comentários - podem ser feitos nos notebooks virtuais também. Para adicionar um comentário é necessário escolher a opção TEXT.. No botão Move cell up o comentário é movido para cima e no Move cell down é movido para baixo.

* Agrupar os valores por uma coluna:
``` 
notas.groupby("filmeId")

``` 
Serádevolvido um objeto data frame do groupby do pandas que possibilita ser usado para alguma outra função, por exemplo tirar a média desse grupo:
``` 
notas.groupby("filmeId").mean()

``` 
Na visualização do groupby foi mostrado também a média de outras colunas. Para extração somente da coluna nota podemos fazer o seguinte:
``` 
notas.groupby("filmeId").mean()["nota"]

ou 

notas.groupby("filmeId").mean().nota

``` 

OBS: Para facilitar o retorno do agrupamento de uma coluna pode ser posto o resultado esperado em uma variavel aux, ex:
``` 
medias_por_filme = notas.groupby("filmeId").mean().nota
``` 

* Histograma da media de uma coluna - 
```
 medias_por_filme.plot(kind='hist')

``` 

## *Outra biblioteca gráfica: Seaborn*

* Como utilizar o Seaborn: 
``` 
sns.boxplot(media_por_filme)

``` 

* Gráfico de Histograma no seaborn:
``` 
sns.displot(medias_por_filme)
``` 

* Descrição das medias de uma coluna:
``` 
medias_por_filme.describe()

``` 

## *Biblioteca matematica:*

* Matplotlib - é uma biblioteca de baixo nível matemática utilizada pelo pandas/seaborn. Costuma-se importar essa biblioteca como plt

* importando a biblioteca matplotlib:
``` 
import matplotlib.pyplot as plt
``` 

* histograma da matplotlib
``` 
plt.hist(medias_por_filme)
``` 

* Titulo do histograma na matplotlib:
``` 
plt.title("Histograma das medias dos filmes")

* Eixo do box plot: Você pode alterar o eixo do boxplot através do comando
``` 
sns.boxplot(y=medias_por_filme)
``` 

* Mudando tamanho do grafico atraves do comando:
``` 
import matplot.pyplot as plt

plt.figure(figsize=(5,8))
``` 


## *Distribuição de médias:*
* usando o box plot do seeborn: Vamos utilizar o sns
``` 
sns.boxplot(medias_por_filme)
``` 

* controlando o numéro de colunas para aparecer no gráfico:
``` 
sns.displot(medias_por_filme, bins=10)
``` 

## *Separando Categorias:*

* categoria nominal:
``` 
tmdb.original_language.unique()
``` 
* mostrar uma coluna: 
``` 
tmdb["original_language"]
``` 

## *Exemplo de leitura de um arquivo e a listagem de uma categoria:*

* Faça o upload do arquivo csv no notebook:
 
arquivo: tmdb_5000_movies.csv

* Faça o import da biblioteca pandas:
``` 
import pandas as pd
``` 

* Adicione a leitura do arquivo a uma variavel
``` 
tmdb = pd.read_csv("tmdb_5000_movies.csv")
``` 

* Liste uma categoria nominal do arquivo csv:
``` 
tmdb.original_language.unique()
```

## *Exemplo de Categorias de dados:*
* Categoria nominal: a mostragem dos dados não precisa ser de acordo com uma ordem. Não utiliza uma classificação de acordo com uma regra, no caso da categoria nominal os valores não são ordenaveis como: ordem alfabética, ordem crescente, ordem decrescente.. exemplo de categoria nominal: listagem de idiomas de filmes, nomes de pessoas ...


* Categoria por ordem: é organizada por uma classificação de acordo com uma regra, por exemplo: ordem alfabética, ordem crescente, ordem decrescente.. a mostragem dos dados deverá ser de acordo com uma ordem.
EX: 
tmdb = pd.read_csv("tmdb_5000_movies.csv")
tmdb["original_language"]

* Categoria quantitativa: é uma categoria onde o valor dos dados contabilizara um valor total. Exemplo: o número de votos em uma pessoa. Cada pessoa terá um número inteiro de votos por exemplo 1, 2, 3, 4, e não 3.5 
EX: 
tmdb = pd.read_csv("tmdb_5000_movies.csv")
tmdb["original_language"].value_counts()

OBS: o to_frame() transforma uma serie em uma coluna bem organizada e padronizada.
EX: tmdb["original_language"].value_counts().to_frame()

OBS: o reset_index() adiciona um indice a uma coluna. 
EX: tmdb["original_language"].value_counts().to_frame().reset_index()

* Categoria quantitativa continua: reune valores que podem variar de x a y no entanto contabilizara os valores entre os intervalos menores de x a y por exemplo: a categoria budget de um filme. O orçamento pode ser de 0 a 500 reais mas os centavos também podem variar. 

  
## *Adicionar uma seção com titulo em destaque no notebook:*
* Vá em +Code e escreva o título. Mas para se obter mais destaque com o tamanho das letras e para que essa seção seja colapsada com as celulas de execução que ficam posterior a esse título, deve-se adicionar "#" ao inicio do Título.

## *Visualiar as categorias:*
* Para comparar categorias usamos plots de categoria, por exemplo no seaborn tem muitos plots de comparação de categoria. Um exemplo no seaborn é o gráfico de barras. 
EX: 
contagem_de_lingua = tmdb["original_language"].value_counts().to_frame().reset_index()
contagem_de_lingua.columns = ["original_labguage","total"]
contagem_de_lingua.head()
sns.barplot(data = contagem_de_lingua)

* Criar uma matriz de 2 eixos. Por exemplo no eixo X ficará cada uma das linguas e no eixo Y o total de itens dessa lingua.
EX: 
contagem_de_lingua = tmdb["original_language"].value_counts().to_frame().reset_index()
contagem_de_lingua.columns = ["original_language","total"]
contagem_de_lingua.head()
sns.barplot(x = "original_language", y = "total" , data = contagem_de_lingua )

OBS: para descrever um x e um y é necessário ter um data frame.

Continuar: Aula 02 - iniciar leitura. 01:19







