# EEL891 - 2020.02 - Relatório do Trabalho 1
Classificação - sistema de apoio à decisão p/ aprovação de crédito


Aluno: Bruno Dantas de Paiva


## Organização do Repositório

Nesse repositório todo o código desenvolvido se encontra no [jupyter](https://github.com/DantasB/Introduction-To-Machine-Learning/blob/main/First_Exercise/Trabalho_2_EEL891.ipynb). Este foi utilizado para submeter o dado ao [Kaggle](https://www.kaggle.com/c/eel891-202101-trabalho-1/).

## Tratamento do dataset

Para entender melhor o dataset e quais colunas deveriam ser consideradas para o modelo foi utilizada a biblioteca missingno para verificar se este dataframe possuia alguma coluna possuindo valores nulos e nenhuma dessas possuiam dados nulos, facilitando o processamento.

Além disso, algumas das colunas não possuiam informações bem claras ao verificar o tipo de dados utilizando o método dtypes da biblioteca pandas. Para verificar melhor, observei os parâmetros contidos nessas colunas e a contagem de cada um desses e foram observados que algum grupo de colunas seria necessário utilizar métodos de encoding como binarização e one-hot-encoding.
 
### Pré-processamento

Para realizar essa binarização foi utilizada a classe ``LabelBinarizer()`` da biblioteca sklearn. 
Já para a realização do One-Hot_encoding foi utilizada a função ``get_dummies()``.


### Matriz de correlação

Para definir quais as colunas deveriam de ser removidas foi utilizada a matriz de correlação a fim de medir a relação dessas colunas do dataset com relação à coluna objetivo. Deste modo foram removidas algumas colunas que possuiam um valor muito próximo de 0. Tendo assim a seguinte referência de colunas:

**1. Colunas removidas:**

```
'Id',
'diferenciais',
'tipo_vendedor',
'churrasqueira',
'quadra',
's_jogos',
's_ginastica',
'area_extra'
```

**2. Colunas binarizadas:**

```
'tipo_vendedor'
```

**3. Colunas codificadas (*One-hot Encoding*):**

```
'tipo',
'bairro'
```

**4. Colunas normalizadas:**

```
'bairro'
```

### Tratamento de Valores Nulos

Ademais, para este dataset, existiam um grupo de valores Nulos e além disso, um grupo restrito de parâmetros que possuiam valores como strings vazias em vez de nulo. Portanto, para fazer um tratamento mais preciso, essas colunas que tinham strings vazias, foram setadas como nulas.

Para os valores Nulos efetivamente foram preenchidos com os valores da mediana de cada coluna que os continham de forma aleatória, tanto para o dado de teste quanto para o dado de treino.

### Análise de Outliers

Para realizar a análise dos outliers, foram traçados dois gráficos utilizando a média da distância euclidiana, deste modo seria possível definir com base nos índices de dados do dataframe, deste modo foi possível observar que tinha uma grande variação da distância em alguns pontos do dataframe. Deste modo, com o auxílio de uma função criada foi possível remover esses dados.

## Análise do Dataset

Com a biblioteca `Pandas`, os dados dos conjuntos de treinamento e teste são importados no formato de DataFrame e depois valores alocados em arrays. No caso do conjunto de treinamento os valores são separados em dois arrays (um para as variáveis independentes e outro para a variável dependente).

Dentre os métodos disponíveis, foram utilizados o Gradient Boosting e Cat Boosting por serem os melhores métodos de classificação (geralmente). Para cada uma das metodologias, foram variados os seus hiperparâmetros a fim de obter um melhor resultado de acurácia (metodologia de medida utilizada por esse trabalho no kaggle).

Após a aplicação de todos os classificadores acima, aquele de melhor resultado foi o Cat Boosting, cujo resultado para o dado de treino foi de 0.6088. Contudo, com este modelo, no Kaggle o resultado foi mais baixo que o obtido pelo Gradient Boosting, sendo este utilizado para a submissão.

Para fazer a submissão dos dados foi utilizado este classificador para predizer os valores do conjunto de teste obtido do próprio kaggle e foi exportado para um csv resultado que será enviado ao kaggle.


## Resultados

O modelo encontrou uma Acurácia de 0.58560 no Kaggle utilizando o modelo de gradient boosting.