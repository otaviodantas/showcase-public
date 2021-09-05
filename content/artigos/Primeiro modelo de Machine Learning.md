+++
categories = ["Development"]
date = "2020-03-25"
description = "Como fazer seu primeiro modelo de Machine Learning"
featured = "Python"
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Como fazer seu primeiro modelo de Machine Learning"
slug = ""
type = "post"
tags = ["Python", "Machine Learning"]
+++

<p style='text-align: justify;'>
Exemplo simples de como implementar uma base de dados comum, em um modelo de Machine Learning que determinará se ele é um vinho do tipo Branco ou Tinto usando o JupyterLab.
</p>

![Untitled](https://miro.medium.com/max/1400/1*SmQEaANmMNiSgj5i7WSi1Q.jpeg)
<p align = "center">
Fonte: Studio Ingrid Picanyol(BeHance).
</p>

<p style='text-align: justify;'>
Para começar vamos instalar nosso ambiente de programação, o JupyterLab. O Jupyter é uma iniciativa cem por cento open source, que visa o suporte para o estudo e desenvolvimento de ciência de dados com suporte para várias linguagens. Se você usar o pip, poderá instalá-lo com:
</p>

``` Bash
pip install jupyterlab
```

Além do ambiente de programação, também precisaremos baixar duas ferramentas que vão nos auxiliar na hora de criar os modelos, que são elas:

- [Anaconda](https://www.anaconda.com/distribution/)

- [Scikit-Learn](https://scikit-learn.org/stable/install.html)

### **Base de dados**

Com tudo instalado, vamos baixar a base de dados disponível no Kaggle para poder usar no nosso modelo:
https://www.kaggle.com/dell4010/wine-dataset

### **Iniciando o Jupyter**

Agora basta inicializar o Jupyter na pasta no local onde você quer iniciar o projeto.

``` bash
Desktop\ot-vio\code\Python\test
```

### **Mão na massa, ou no vinho!**

Com o ambiente de programação aberto, vamos começar a programar. Na primeira célula importaremos as bibliotecas e funções necessárias.

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.ensemble import ExtraTreesClassifier
```


- ***train_test_split:** é uma* função usada para dividir o conjunto total de dados em dois outros conjuntos o de treino e o teste.
- ***ExtraTreesClassifier:*** é um método de aprendizado de conjunto baseado em árvore de decisão, a diferença desse método para o RandomForest é a foma de aprendizado sem o excesso, ou seja, ela propõe ao modelo a aleatoriedade de determinadas decisões.

``` Python
file = pd.read_csv('wine_dataset.csv')
```

- ***pd.read_csv:*** Nesta parte simplesmente importamos o dataset que vamos utilizar.

![https://cdn-images-1.medium.com/max/1250/1*Wb8p7XMBLBIpBfVH5wWfYQ.png](https://cdn-images-1.medium.com/max/1250/1*Wb8p7XMBLBIpBfVH5wWfYQ.png)
<p align = "center"> Figura 1 </p>

<p style='text-align: justify;'>
Note que na Figura 1 na última coluna da tabela, encontramos os tipos do vinho em “red” e “white”, o nosso modelo não conseguirá prosseguir se não transpassarmos coluna de str para int. Isso faz parte de um processo muito importante para qualquer tipo de modelo, o tratamento de dados está intrinsecamente ligado ao sucesso do seu modelo.
</p>

```python
file['style'] = file['style'].replace('red', 0)
file['style'] = file['style'].replace('white', 1)
```

As funções acima demonstram como podemos transformar a coluna *style.*

``` python
target = file['style']
predictive = file.drop('style', axis = 1)
```
<p style='text-align: justify;'>
Nessa parte do código temos a separação das varáveis preditoras e das variáveis resultado. As variáveis alvo, ou resultado, são aquelas que buscamos no experimento, logo, a variável *target* recebe toda a coluna <b> style(Figura 2).</b>
</p>

<p align = "center"> 
 <img src="https://cdn-images-1.medium.com/max/1250/1*j_W_grl-w4JXX4ETEFK6Lg.png">Figura 2 
</p>

Já a variável *predictive* recebe as demais colunas do dataset(Figura 3), esse tipo de variável é composta por dados que podem mudar o resultado das variáveis alvo.

<p align = "center">
    <img src="https://cdn-images-1.medium.com/max/1250/1*TGkC6MJDtR0dOfoq50yoKQ.png"> Figura 3 
</p>

``` python
predictive_train, predictive_test, target_train, target_test = train_test_split(predictive, target, test_size = 0.3)
```
<p style='text-align: justify;'>
Existem etapas para percorrer no processo de criação de um modelo de Machine Learning, duas dessas etapas são: etapa de treino e etapa de teste. Na etapa de treino os dados são requisitados para que o modelo possa entender a diferença do vinho tinto para o vinho branco. Já na etapa de teste outro dataset é entregue ao modelo, diferente do dataset que é usado na etapa de treino, para isso usamos o *train_test_split,* ele irá preparar os dados para o treino e teste.
</p>

<p style='text-align: justify;'>
Podemos ver claramente como o conjunto é dividido. A função separou uma porção maior para a etapa de treino (Figura 4, a esquerda), e uma porção equivalente a um terço do total, para a etapa de de teste (Figura 5, a direita).
</p>


<p align = "center"> 
    <img src="https://cdn-images-1.medium.com/max/1250/1*0BPb5sg984GLztWq0OqQjw.png">
    Figura 4
</p>

<p align = "center"> 
    <img src="https://cdn-images-1.medium.com/max/938/1*MUvqoOiYkKNqOpWPQTPChQ.png"> Figura 5
</p>

### **Criando o modelo**

Pode parecer engraçado, mas criaremos o modelo em apenas uma linha de código.

```python
model = ExtraTreesClassifier(n_estimators = 100)
```


Nessa linha basicamente chamamos o modelo que importamos lá em cima e passamos um parâmetro para ela.

- *n_estimators:* número de árvores usadas para processar o conjunto de dados, por padrão ele é =10.

```python
model.fit(predictive_train, target_train)
```

Por meio da função *fit do scikit-learn* implementamos os estimadores.

![https://cdn-images-1.medium.com/max/1250/1*fr9iuTYkEA5V7g8L6iOXPQ.png](https://cdn-images-1.medium.com/max/1250/1*fr9iuTYkEA5V7g8L6iOXPQ.png)

<p align = "center"> Figura 6</p>

<p style='text-align: justify;'>
Se tudo correr bem até aqui esse será o resultado da depuração da célula anterior (Figura 6), a partir desse ponto o seu modelo está treinado.
</p>

### **Hora do teste**

<p style='text-align: justify;'>
Lembra quando separamos os dados em conjunto de treino e teste, pois então, está na hora de usar o conjunto de teste para saber se realmente o modelo tem um resultado esperado, ou seja, se ele vai conseguir determinar qual vinho é cada um.
</p>

<p style='text-align: justify;'>
Para isso usaremos a função *score,* ela irá fornecer ao modelo nossos dados de teste, e por consequência a variável *result* receberá o veredito.
</p>

```python
result = model.score(predictive_test, target_test)
```

<p style='text-align: justify;'>
Para que possamos ver o resultado do teste, basta utilizar a célula seguinte para imprimir:
</p>

<p align = "center">
    <img src="https://cdn-images-1.medium.com/max/1250/1*pmgYyuBp6xM4OztBWs9S8Q.png">
</p>

<p align = "center"> Figura 7</p>

<p style='text-align: justify;'>
Pronto! O seu modelo está finalizado e com uma taxa de assertividade alta, isso quer dizer que se inserido qualquer outro dado diferente do que foi usado no dataset de treino e teste, provavelmente ele terá 99,8% de certeza no resultado.
</p>

---

<p style='text-align: justify;'>
O artigo contém várias assuntos pertinentes na área de ciência de dados, vou deixar alguns link com conteúdos mais aprofundados sobre os tópicos.
</p>

# **Referências:**

- [https://youtu.be/DNegkxwQJuY](https://youtu.be/DNegkxwQJuY)
- [https://medium.com/@contactsunny/how-to-split-your-dataset-to-train-and-test-datasets-using-scikit-learn-e7cf6eb5e0d](https://medium.com/@contactsunny/how-to-split-your-dataset-to-train-and-test-datasets-using-scikit-learn-e7cf6eb5e0d)
- [https://medium.com/@namanbhandari/extratreesclassifier-8e7fc0502c7](https://medium.com/@namanbhandari/extratreesclassifier-8e7fc0502c7)
- [https://scikit-learn.org/stable/modules/model_evaluation.html](https://scikit-learn.org/stable/modules/model_evaluation.html)