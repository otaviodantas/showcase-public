+++
categories = ["Development"]
date = "2020-07-06"
description = "Web Scraping na página da OLX"
featured = "Python"
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "Web Scraping na página da OLX"
slug = ""
type = "post"
tags = ["Python", "BeautifulSoup"]
+++

![https://miro.medium.com/max/1094/1*75AH4zD0r5CNtO_Zpf_epg.jpeg](https://miro.medium.com/max/1094/1*75AH4zD0r5CNtO_Zpf_epg.jpeg)

## **Mas oque é isso?**

O método de web scraping consiste em obter dados de uma página web, navegando pelo seu código HTML e capturando os dados que interessam, para posteriormente usa-los em outras aplicações.

Um exemplo da utilização dessa ferramenta pode ser vista quando vamos até um site de vendas de algum produto, e queremos prever o preço desse produto daqui a alguns dias ou meses. Para isso, aplicamos o web scraping para obter os dados dos preços que estão sendo mostrados no site.

No meu caso, vou utilizar o site da OLX para aplicar a técnica.

## **Por onde começar?**

Antes de tudo precisamos ir até a página e visualizar quais dados nos interessa.

- Preço do produto
- Descrição
- Localização
- Nº de páginas

> Para que os dados continuassem os iguais, mesmo que eu atualize a página, tive que ordena-los por cidade, e menor preço, dessa forma obteria os mesmos números sempre que acesse aquela URL.

![https://miro.medium.com/max/47/1*9aRv_5wekpetKWdver2qRQ.png?q=20](https://miro.medium.com/max/1094/1*9aRv_5wekpetKWdver2qRQ.png?q=20)

## **Identificação no HTML**

Como já localizamos os dados visualmente, agora basta ir no código fonte HTML e identificar onde eles estão.

A esquerda, o card onde está localizado a maioria das informações. A direita é o primeiro item da lista, ou seja, o primeiro produto.

![https://miro.medium.com/max/1059/1*YMCMHTHQAIY805JjA8-peQ.png](https://miro.medium.com/max/1059/1*YMCMHTHQAIY805JjA8-peQ.png)

![https://miro.medium.com/max/1055/1*ErrbMWwGlO31pv5ag6XbKg.png](https://miro.medium.com/max/1055/1*ErrbMWwGlO31pv5ag6XbKg.png)

Quando fazemos o scraping em um site comercial, os itens que são apresentados estão dentro de uma lista de itens, que por sua vez possuem a mesma estrutura dos demais. Tendo isso em mente, o ideal é identificar as informações no primeiro item e em seguida replicar para o restante.

Para que o nosso código entenda onde estão localizados as informações, precisamos passar os identificadores do código HTML, ou seja, suas classes.

``` .env
CONTAINER_PAGES_FIRST = 'col2 sc-15vff5z-5 fFdJjk'
CONTAINER_PAGES_SEC = 'sc-jTzLTM sc-ksYbfQ uUqze'
CONTAINER_PAGES_THIRD = 'sc-1mi5vq6-0 gfpAwo'

CONTAINER_MAIN_CARDS_FIRST = 'sc-1fcmfeb-0 WQhDk'
CONTAINER_MAIN_CARDS_SEC   = 'fnmrjs-1 ddDPXY'
```

## **Módulos**

Os módulos são estruturados da seguinte forma:

> simple_scraping.py

Ele pode ser executado como uma forma muito mais simples de web scraping, ele não te retorna dados, porém são poucas linhas de comando que podem ser utilizadas para entender melhor o funcionamento das bibliotecas.

> err_handling.py

Módulo principal, quando executado interage com os demais módulos e retorna um tabela com todos os dados obtidos

> all_def.py

Módulo separado com as funções que foram utilizadas, separadas por suas funcionalidades, por exemplo, buscar o texto, a imagem, gerar a tabela etc.

> my_options.py

Neste módulo eu incorporei todas as informações estáticas em forma de varáveis, para que eu pudesse apenas importar e usa-las de forma comum.

## **Dificuldades**

Apesar de obter bastante dados, não consegui coletar por completo as informações, se prestarem atenção, o número de produtos ultrapassa os 150 mil. Quando tentei implementar a lógica para capturar todos os produtos foi me retornado um erro pelo tamanho de páginas que eu precisaria acessar.

## **Link**

[github.com](https://github.com/otaviodantas/web-scraping-python)