+++
categories = ["Development"]
date = "2020-10-15"
description = "Gerador de Dataset para Processamento de Linguagem Natural (PLN)"
featured = "Python"
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Gerador de Dataset para Processamento de Linguagem Natural (PLN)"
slug = ""
type = "post"
tags = ["Python", "Machine Learning", "NLP"]
+++

![https://miro.medium.com/max/1094/1*UMwqWHEYVmkezmRaqyCh1g.png](https://miro.medium.com/max/1094/1*UMwqWHEYVmkezmRaqyCh1g.png)

<p align = "center">
    fonte: <a href="https://icons8.com/illustrations">icons8 </a>
</p>

## **Introdução**

<p style='text-align: justify;'>
Este artigo vai mostrar como foi o processo de desenvolvimento e o resultado de um programa em python, com o intuito de gerar um dataset simples, com um conjunto de frases extraídas do Twitter, por meio da API disponibilizada pelo próprio Twitter. No projeto foi usado conceitos básicos de Python e algumas bibliotecas como: Tweepy e NLTK.
</p>

## **Problemática**

<p style='text-align: justify;'>
Eu tenho um grande apreço pelo campo de Machine Learning, e por conta disso, iniciei meus estudos na área por um ramo com grande notoriedade atualmente, o NLP (Natural Lenguange Process). O projeto em maior escala, busca analisar tweets de um respectivo assunto e retorna quais são as emoções que se destacam em relação ao tema.
</p>

<p style='text-align: justify;'>
Desta forma então, tive a ideia de fazer o meu próprio dataset, baseado em assuntos específicos que poderiam ser escolhidos por meio de um parâmetro. No meio do processo, fui desvendando algumas outras tecnologias que poderiam me auxilia na infra estrutura do projeto, entra elas está o Docker, e por conta disso acabei gastando um pouco mais de tempo para entender como a tecnologia funcionava, e documentar tudo isso em um artigo.( Link do Artigo ).
Neste artigo irei me atentar somente ao script usado para captar os tweets e aloca-los em um arquivo CSV.
</p>

## **Twitter-API**

<p style='text-align: justify;'>
A API do Twitter tem um papel importante no projeto. Para ter acesso a ela, é preciso fazer uma requisição de conta para desenvolvedor, não demora muito, e as features que ela entrega são de uma infinidade de aplicações.
Você pode se inscrever como desenvolvedor por esse link:
</p>

[developer.twitter.com](https://developer.twitter.com/en)

Esse tutorial cobre todo o processo de inscrição:

## **Modulos**
<p style='text-align: justify;'>
O programa é constituido por 6 módulos, e um arquivo .ENV. A primeira imagem abaixo, mostra como o programa é executado. Por mais separados que as funções estejam, o módulo Stream é responsável por chamar os processos que limpam os dados e salvam em um arquivo CSV, tornando o fluxo de software em cascata.
Na minha visão, ainda é confuso, porém vou fazer alguns ajustes e fazer algo parecido como a secunda imagem.
</p>

![https://miro.medium.com/max/1094/1*JMgE9nhRaXrsrRMaAUCg6w.png](https://miro.medium.com/max/1094/1*JMgE9nhRaXrsrRMaAUCg6w.png)

![https://miro.medium.com/max/1094/1*XPSPooiPov10u6BokQhMpA.png](https://miro.medium.com/max/1094/1*XPSPooiPov10u6BokQhMpA.png)

**[main.py](http://main.py/)**

> É responsável por comandar todos os outros módulos.

**call_stream.py**

> Unicamente invocado para fazer as chamadas de ativação da stream.

**[stream.py](http://stream.py/)**

> O módulo é ativado e tem uma função call back que retorna todo tweet que chega na pesquisa.

**[auth.py](http://auth.py/)**

> Unicamente para autenticar as chaves da API.

**aux_mod.py**

> São funções que auxiliam módulos maiores, retornam listas de pontuação, stopwords e strings tokenizadas.

**twitter_data_cleaner.py**

> Esse módulo remove todas as informações que não são utilizados para a analise:

- remove_stopwords
- remove_user
- remove_URL
- remove_emoji
- remove_hashtag
- remove_punct

**config.env**

> As chaves de acesso da API do twitter e a palavra chave a ser pesquisada, podem ser acessadas por meio desse arquivo.

## **I/O**

**Input**

<p style='text-align: justify;'>
No arquivo config.env é possível editar a palavra que quer basear seu dataset em WORDKEY.
As outras variáveis são chaves que são disponibilizadas pela API do Twitter, e são necessárias no processo de autenticação.
</p>

```
WORDKEY=CONSUMER_KEY=CONSUMER_SECRET_KEY=ACESS_TOKEN= ACESS_SECRET_TOKEN=
```

**Output**

<p style='text-align: justify;'>
O arquivo cria um arquivo CSV e popula o arquivo com os tweets que vão chegando, até que sofra uma interrupção do teclado (Ctrl+C).
</p>

## **Conclusão**

<p style='text-align: justify;'>
Tudo está muito cru, e a ideia justamente é disponibilizar o repositório para que outras pessoas possam dar opiniões sobre quais características podem ter mais relevância nas técnicas usadas em PLN, como por exemplo a localização do usuário ou o horário de publicação do tweet.
</p>

<p style='text-align: justify;'>
Até sendo mais criterioso, mudanças podem ser sugeridas na parte de Arquitetura de Software e Clean Code. O projeto pode ser uma grande base de dados para quem está começando na área.
</p>

## **Link do repositório**

[github.com](https://github.com/otaviodantas/NLP-generator-dataset)