+++
categories = ["Development"]
date = "2020-11-15"
description = "A arte de Iterar, em Python"
featured = "Python"
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "A arte de Iterar, em Python."
slug = ""
type = "post"
tags = ["Python"]
+++


![https://miro.medium.com/max/1094/1*C-L6TRWn2iRL5Z3C7KOz0g.png](https://miro.medium.com/max/1094/1*C-L6TRWn2iRL5Z3C7KOz0g.png)

<p align = "center">
    Illustration by Natasha Remarchuk from <a href="https://icons8.com/illustrations">icons8 </a>
</p>

<p style='text-align: justify;'>
Quanto mais mergulhamos em alguma linguagem, começamos a busca por entender o por que que as coisas funcionam dessa ou daquela forma. Hoje trouxe um conceito que se ouve falar bem no inicio da programação, mas que passa despercebido até nos depararmos com o nome dele associado a um erro.
</p>

``` bash
TypeError: list object is not an iterator
```

## **Conceito**

<p style='text-align: justify;'>
Formalmente falando, iteradores são atributos de classe que o tornam “percorriveis”, ou seja, é possível acessar cada parte da coleção de forma singular. De um forma prática, quando implementamos uma lista em Python ele já é por natureza iterável.
</p>

``` python
number_list = [1, 2, 3, 4, 5, 6]
for number in number_list:
     print(number)
```

A saída para esse script é:

``` bash
1
2
3
4
5
6
[Finished in 0.52s]
```

<p style='text-align: justify;'>
O Python sabe que o <b>number_list</b> é uma lista, por default ele pode ser acessado parte por parte no laço FOR.

<p style='text-align: justify;'>
Esse comportamento da lista se da pelo atributo que está implementado por baixo dos panos: <b>iter</b>( ) ou chamado de <b>dunder iter.</b>

> Nota: O conceito de dunder advém da ideia de double underscore, que nada mais é do que os dois “underlines” posicionados antes e depois do nome do atributo. Isso é muito comum no mundo python para relacionar sobre qual atributos queremos falar, como por exemplo: __str__( ) ← dunder str, __index__() ← dunder index, __float__( ) ← dunder float, e por ai vai.

## **O FOR em outra linguagem**

<p style='text-align: justify;'>
Nas linguagem mais recentes, o FOR melhorado é usado à algum tempo, entretanto nas linguagens como o C por exemplo, o FOR é implementado com um contador, amigavelmente quase sempre chamado de “i”, e que é responsável por manter o estado de operação daquele laço, como visto no exemplo a baixo:
</p>

``` python
for (i=0, i == range, i++){
  printf("%d", i);
}
```

<p style='text-align: justify;'>
A variável “i” está implícita em Python, ou seja, não precisamos esquentar a cabeça quando vamos iterar sobre alguma coleção, pois internamente, o Python já fornece isso pra gente prontinho. Porém, internamente, podemos comparar a variável “i” com a função next( ) ou dunder next (__next__) que é responsável por fazer o gerenciamento de estado em um loop.
</p>

<p style='text-align: justify;'>
Vamos tentar implementar como seria então um laço FOR usando as funções que são usadas internamente durante uma chamada:
</p>

```python
lista = [1, 2, 3, 4, 5]
iter_list = iter(lista)
print(next(iter_list))
print(next(iter_list))
print(next(iter_list))
print(next(iter_list))
print(next(iter_list))
```
<p style='text-align: justify;'>
Repare como eu percorro a lista de cinco números usando a função next( ), que pega como parâmetro um objeto iterador. E a saída disse código é este:
</p>

``` bash
1
2
3
4
5
[Finished in 0.383s]
```
<p style='text-align: justify;'>
Tem a mesma saída que obtivemos usando o laço for no tópico anterior. É feito um adendo ao fato de quando não houver mais iterador para iterar, a função next( ) irá gerar uma exceção chamada StopIteration, e é com ele que o loop identifica que a coleção chegou ao final.
</p>

``` python
iter_list = iter(lista)
try:
     print(next(iter_list))
     print(next(iter_list))
     print(next(iter_list))
     print(next(iter_list))
     print(next(iter_list))
     print(next(iter_list))
except: #StopIteration
     print("lista chegou ao fim")
```

Output:

``` bash
1
2
3
4
5
lista chegou ao fim
[Finished in 0.367s]
```

## **1, 2, 3 testando.**

<p style='text-align: justify;'>
A implementação de algo é que nos faz entender de fato o que está sendo falado, por conta disto então, vamos criar uma classe, e fazer alguns testes em torno dela.
</p>

``` python
class iter_list_number:
    def __init__(self, max: int) -> None:
        self.end_number = max
        self.start_number = 5

if __name__ == '__main__':
    n_list = iter_list_number(10)
    for number in n_list:
        print(number)
```

<p style='text-align: justify;'>
Criamos uma classe bem simples, a intenção é apenas receber um número e quando quisermos iteralo, faremos isso a partir do número 5, exemplo: iter_list_number(10) → a saída esperada é 5, 6, 7, 8, 9, 10. Porém o log de erro que recebemos foi esse:
</p>

``` bash
File ".\test.py", line 8, in <module>
    for number in n_list:
TypeError: 'iter_list_name' object is not iterable
```

<p style='text-align: justify;'>
Como dito anteriormente, quando não implementamos o dunder iter é impossível iterar sobre o objeto da classe. Sabendo disso, vamos implementar este método para ver se realmente funciona.
</p>

``` python
class iter_list_number:
    def __init__(self, max: int) -> None:
        self.end_number = max
        self.start_number = 5    
        
    def __iter__(self):
        return self    
    
    def __next__(self) -> int:
        x = self.start_number
        if x > self.end_number:
            raise StopIteration
        else:
            self.start_number += 1
        
        return x

if __name__ == '__main__':    
    foo = iter_list_number(10)
    for bar in foo:
        print(bar)
```

Logo, a saída será:

``` bash
5
6
7
8
9
10
[Finished in 0.358s]
```
<p style='text-align: justify;'>
É importante frisar que é importante ter uma condição de parada, assim como na linguagem C, usamos o número de entrada dado pelo usuário para ser a condição de parada (self.end_number) e vamos incrementando sobre o número pré-definido self.start_number.
</p>

<p style='text-align: justify;'>
É possível fazer outra implementação que possuí outras características, desta vez usando uma classe que recebe umas lista de cores em seu construtor e com o método <b>add_item</b> podemos adicionar outras cores à lista.

``` python
from typing import List

class colors_colletion:
    def __init__(self, colors: List[str]) -> None:
        self.list_colors = colors
        self.flag_count: int = 0    
    
    def add_item(self, colors: str) -> None:
        self.list_colors.append(colors)    
    
    def __iter__(self):
        return self    
    
    def __next__(self) -> str:
        flag_stop = len(self.list_colors) #stop condition
        flag_count = self.flag_count       
        if flag_count >= flag_stop:
            raise StopIteration        
        else:
            self.flag_count += 1
        
        return self.list_colors[flag_count]
        
if __name__ == '__main__':
    list_colors = colors_colletion(['blue', 'red', 'brown'])
    list_colors.add_item('green')
    for color in list_colors:
        print(color)
```
<p style='text-align: justify;'>
A função dunder next é semelhante ao exemplo anterior, porém, agora usamos o tamanho da lista como condição de parada, assim que a <b>flag_count</b> chegar ao tamanho máximo ele apresentará o StopIteration e o loop acabará.

## **Conclusão**

<p style='text-align: justify;'>
Os iteradores em Python, apresentam uma construção elegante, com a sua aplicabilidade variada. Vale ressaltar que os iteradores possuem grande base no padrão de projeto Iterator, o que pode se tornar tópico de um outro artigo.
</b>

## **Referências**

Esses dois links me ajudaram a entender alguns pontos:


[refactoring.guru](https://refactoring.guru/pt-br/design-patterns/iterator)

[www.geeksforgeeks.org](https://www.geeksforgeeks.org/python-__iter__-__next__-converting-object-iterator/)
