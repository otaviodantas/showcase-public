+++
categories = ["Development"]
date = "2020-08-14"
description = "O básico do Docker"
featured = "Python"
featuredalt = ""
featuredpath = ""
linktitle = ""
title = "O básico do Docker"
slug = ""
type = "post"
tags = ["Python", "Docker"]
+++


## **Contextualizando**

<p style='text-align: justify;'>
Durante a minha graduação eu sempre ouvi, e continuo ouvindo, sobre o Docker, e como ele é isso e aquilo. Esse assunto sempre me deixou com uma pulga atrás da orelha, então desta vez eu decidi estudar um pouco mais sobre como surgiu a tecnologia e como ela impactou todo o ecossistema de desenvolvimento.
</p>

## **A história do Docker.**

<p style='text-align: justify;'>
Para contar a história do Docker antes é preciso entender como as coisas funcionavam antes dele. De uma forma superficial as empresas que proviam os servidores e disponibilizavam máquinas e serviços para as estabilidade das aplicações de outras empresas faziam tudo isso, na grande maioria, com máquinas físicas. As máquinas eram providas com capacidade estática, ou seja, as empresas compravam aquelas máquinas pensando sempre acima da média diária de movimento, para que, em alguma ocasião especial, o sistema não sofresse por uma sobrecarga de acessos.
</p>

<p style='text-align: justify;'>
Por exemplo, uma máquina que comportava o banco de dados da aplicação, era provida com uma capacidade de suportar 10 vezes o fluxo diário de query, pensando que, em dia muito movimentado, o banco suportaria os acessos “sem abrir o bico”. Mas para pra pensar na capacidade diária que o sistema “desperdiçava” somente em uma das máquinas.
</p>

<p style='text-align: justify;'>
Isso afetava diretamente o bolso da empresa que comprava as máquinas, pois, quanto maior a sua capacidade, maior os gastos com energia e manutenção, lembrando que as máquinas ficavam em seu maior tempo ociosas.
</p>

<p align = "center">
        <img src="https://miro.medium.com/max/1063/1*kLHQkOWV4WJj1JFXUn4KBg.jpeg">Fonte: Autor
</p>

<p style='text-align: justify;'>
Porém com o desenvolvimento do Hypervisor e todas as inovações que ele trazia junto de si, os hosts começaram a implementar as máquinas virtuais como forma de lidar com a capacidade ociosa das máquinas físicas.
</p>

<p align = "center">
        <img src="https://miro.medium.com/max/458/1*GLNUNfrh6JmF0RSLfLLy9A.jpeg">
</p>

<p style='text-align: justify;'>
O Hypervisor compartilha virtualmente os recursos da máquina física, podendo então, distribuir o hardware “parrudo” que anteriormente era usado somente em uma máquina física, para N máquinas virtuais, causando um impacto gigantesco no ramo de servidores pelo mundo todo.
</p>

<p style='text-align: justify;'>
Mas como nem tudo são flores, depois de um tempo os servidores começaram a sentir o peso de ter um sistema operacional rodando em cada máquina virtual.
</p>

<p style='text-align: justify;'>
Como qualquer sistema operacional eles ocupam uma parcela mínima de memória RAM e espaço no disco, além de pacotes que não são uteis para a aplicação a qual a máquina está destinada.
</p>

<p style='text-align: justify;'>
No final das contas ambas as tecnologias tinham o mesmo problema, possuíam capacidade e ferramentas além do que era necessário para a aplicação. <b>E é ai que o Docker entra!</b>
</p>

<p style='text-align: justify;'>
O conceito de Docker abrange muito mais que só o deploy , é um ecossitema de ferramentas que possibilitam ao desenvolvedor uma rápidez na hora de implementar a infraestrutura da sua aplicação.
</p>

<p align = "center">
        <img src="https://miro.medium.com/max/458/1*FmE1KNXeE07pxaGvA2hVEQ.jpeg">Fonte: autor
</p>

<p style='text-align: justify;'>
O Docker é nativo no Linux, tornando sua operação mais fluída, pois não precisa de uma virtualização como no Windows. Para rodar, o Docker no Windows uma micromáquina virtual que é executada em cima do Hyper-V, mesma tecnologia do Hypervisor, que pode ser encontrado em alguns modelos do Windows, um exemplo de micromáquina é a Alpine Linux. Outra forma de executar o Docker no Windows é o usando o subsistema [WSL2](https://docs.microsoft.com/pt-br/windows/wsl/wsl2-index), que precisa ser instalado.
</p>

<p style='text-align: justify;'>
A Docker Engine é capaz de criar, entregar e rodar containers com uma rapidez monstruosa, isso faz dele uma proposta muito melhor que os seus antecessores.
</p>

<p style='text-align: justify;'>
No final das contas, o que o Docker propõe é que uma aplicação possa ser provida de forma segura e isolada, ou seja, cada parte da aplicação possui um container para tal. Cada container por sua vez possui somente o necessário para que aquela aplicação seja operada, e se por algum acaso a demanda por bibliotecas ou ferramentas dentro do container for solicitada, você não terá problema em implementar.
</p>

## **Por onde começar?**

<p style='text-align: justify;'>
Como eu disse anteriormente, o Hyper-V só é encontrado em alguns modelos de Windows como o Professional, Education e Enterprise, então se você não for usuário de algum desses você não poderá brincar com a nossa baleiazinha, brincadeira, tem outra possibilidade de usar o Docker mesmo não sendo usuário desses modelos, e se chama Docker Toolbox. O Docker Toolbox vem com o Oracle Virtual Box, que tem a função de emular o Alphine Linux.
</p>

[Docker Toolbox](https://docs.docker.com/toolbox/)

[Docker Install](https://docs.docker.com/desktop/windows/)

<p style='text-align: justify;'>
Na hora de executar, o Docker for Windows pode ser utilizado via prompt nativo do windows, porém o Docker Toolbox possui um prompt especial para o uso, o Docker Quickstart Terminal.
</p>

## **Preliminares**

<p style='text-align: justify;'>
Antes de começar a organizar tudo em contêineres, precisamos falar de algo que iremos ouvir muito enquanto usuários do Docker, as <b>IMAGENS</b>.
</p>

<p style='text-align: justify;'>
Nos nossos exemplos passados falamos sobre a aplicação que fica “dentro” do contêiner, passaremos a chamar essa estrutura de imagens, pois são elas que dão vida ao nosso amigo frio e metálico. Sendo mais especifico, quando precisamos subir um container contendo o Mysql, por exemplo, precisaremos ir até o repositório principal de imagens do docker, o docker hub, e buscar pela imagem oficial do banco de dados.
</p>

<p align = "center">
        <img src="https://miro.medium.com/max/1094/1*tgUYNHm1I5jodmX76DKfyg.png">Fonte: autor
</p>

> Você pode encontrar outras imagens que possuem o nome mysql, como por exemplo zert/mysql, marifz/mysql-oficial, porém essas imagens NÃO são oficiais, fica nítido que a imagem oficial contem a certificação docker logo em baixo.

<p style='text-align: justify;'>
As imagens oficiais são a estruturas padrões que podemos utilizar para criar as nossas próprias imagens, com comandos e rotinas personalizadas, e é o que vamos fazer nesse artigo.
</b>

## **O projeto**

<p style='text-align: justify;'>
A principio pensei de subir somente um container para uma demonstração mais casual, porém, estou com um outro projeto que envolve a API do twitter e NLP.
</b>

<p style='text-align: justify;'>
Pensando nisso, vou subir um container com a aplicação bruta, o código, e outra com o banco. O intuito geral é captar tweets relacionados a determinado assunto em um banco de dados relacional.
</b>

<p align = "center">
        <img src="https://miro.medium.com/max/458/1*82AtGK6qdg3uNJrYQkR-Bw.jpeg">Fonte: autor
</p>

## **Repositório**

> Estou usando o Docker Toolbox, então todas os comandos serão no Docker Quickstart Terminal.

Com o terminal aberto, vamos até a pasta que contêm a nossa aplicação. No meu caso a distribuição ficou dessa forma:

``` Bash
C:.
│
├───code
│       auth.py
│       database.py
│       main.py
│       organize.py
│       remove_trash.py
│       stream.py
│
├───db
│       create-database.sql
│
└───dockerfiles
        db.Dockerfile
        twitter-api.Dockerfile
```

A pasta **code** contêm os módulos python, na pasta **db** o arquivo .sql para a criação do banco, e os arquivos para as criações das nossas imagens estão na pasta **dockerfiles**. Os aquivos com a extensão .Dockerfile é responsável por conter as instruções para a criação da nossa imagem.

## **1º Etapa: Criar a imagem Mysql.**

Os comandos no Docker são muito simples e intuitivos, para começar então vamos verificar a versão que estamos trabalhando:

``` Bash
$ docker --version
Docker version 18.03.0-ce
```

Para criar a nossa imagem vamos precisar do arquivo db.Dockerfile, mencionado na parte anterior.

``` Bash
FROM mysql:5.7COPY ./db/create-database.sql /docker-entrypoint-initdb.d/ENV MYSQL_ROOT_PASSWORD=RootPasswordENV MYSQL_DATABASE=twitterdbENV MYSQL_USER=MainUserENV MYSQL_PASSWORD=MainPassword
```

- O **FROM** representa a nossa imagem base, ou seja, vamos utilizar a imagem original myql, o dois pontos denota a versão, que no meu caso é a 5.7.
- **COPY** literalmente copia o aquivo que é mencionado no primeiro parâmetro que está localizado no host, para o segundo parâmetro, dentro do contêiner. COPY <origem> <destino>
- **ENV** são variáveis de ambiente, são coisas que precisam ser passadas para o funcionamento do meu contêiner mysql.

vamos até o prompt dar o comando para criar a imagem.

``` Bash
docker build -t otaviodantas/mysql -f ./dockerfiles/db.Dockerfile .
```

- **build** é o comando para criar a imagem no docker.
- **t** flag usada para nomear a imagem, como boa prática o ideal é que coloque o usuário que mantem essa imagem/ a imagem oficial.
- **f** flag com o caminho até o dockerfile

<p align = "center">
        <img src="https://miro.medium.com/max/1094/1*2rYQYg76sfjoe2r5dLUdPQ.png">Fonte: autor
</p>

<p style='text-align: justify;'>
Repare que ele segue cada etapa assim como está no arquivo, ele primeiro faz o download da imagem base e em seguida ele vai executar as outras instruções que vem a seguir, em camadas.
</p>

<p align = "center">
        <img src="https://miro.medium.com/max/1000/1*bF-kV6oAFrI9vSGP6MDBGQ.png">Fonte: autor
</p>

<p style='text-align: justify;'>
As camadas são a estrutura da imagem, quando precisarmos modificar a mesma não custará o mesmo tempo que custou da primeira vez, tornando esse processo muito rápido. Dando um docker images, vamos conseguir visualizar todas as imagens salvas localmente.
</p>

``` Bash
docker images
```

![https://miro.medium.com/max/1094/1*FZ7DjfMHtqlOEthMS9BfvA.png](https://miro.medium.com/max/1094/1*FZ7DjfMHtqlOEthMS9BfvA.png)

## **2º Etapa: Subir o contêiner.**

Com a nossa imagem pronta, basta subirmos o contêiner com o comando:

``` Bash
docker run otaviodantas/mysql
```

O processo de inicialização está sendo feito e aparecerá em forma de log no terminal. Se você preferir não vê-los, o comando precisará da flag **-d** e ficará dessa forma:

``` Bash
docker run -d otaviodantas/mysql
```

Para verificar se o contêiner está ativo basta dar um **docker ps**.

![https://miro.medium.com/max/1094/1*cGbxmmz_-BpWtMqQoSpxvA.png](https://miro.medium.com/max/1094/1*cGbxmmz_-BpWtMqQoSpxvA.png)

## **3º Etapa: Criar a imagem Python.**

<p style='text-align: justify;'>
Assim como criamos a nossa imagem Mysql, nesta etapa vamos construir a imagem que terá o papel de coletar os twittes e trata-los para salvar no banco que já está rodando.
</p>
Vamos dar uma olhada no DockerFile dessa imagem:

``` docker
FROM python:3.6.4LABEL maintainer="Otávio Mendonça"
COPY code/. /scr/COPY requirements.txt /scr/RUN pip install -r /scr/requirements.txtWORKDIR /scr
```

- O **FROM** determina qual imagem base estamos usando para construir a nossa imagem pessoal, nessa caso usamos o python na versão 3.6.4. Essa versão estava rodando no meu VScode durante toda a fase de construção da aplicação na minha máquina.
- **LABEL** pode ser utilizado como rótulos, definindo informações para o sistema. Nesse caso usei a variável *mantainer* para gravar o meu nome como “mantedor” dessa imagem.
- **COPY** cria uma cópia de arquivo da máquina host para dentro do contêiner. Ele está passando todos os códigos da aplicação para a a pasta scr/.
- **RUN** vai executar o comando que estiver designado. No nosso caso, ele vai, por meio do gerenciador de pacotes pip, instalar todas as bibliotecas e dependências que estão especificadas no arquivo requirements.txt

``` Bash
tweepy==3.8nltk==3.5unidecode==1.1.1mysql-connector-python==8.0.21
```

- **WORKDIR** seta um diretório para servir como local de trabalho, ou seja, todos os comandos serão rodados nesse diretório especifico.

## **4º Etapa: Subindo contêiner Python.**

Para colocar a nossa aplicação rodando, vamos dar o comando:

``` Bash
docker create otaviodantas/init
```

Subimos o contêiner mysql apenas com o comando

***run***

, porém, tive problemas na hora de subir o ambiente em Python com o mesmo comando. Para isso primeiro criei a aplicação com o comando

***create***

e depois o levantei com o comando

***start***

Agora se dermos um ***docker ps -a*** veremos que o nosso contêiner está vivo porém não está ativo

``` Bash
$ docker ps -a
CONTAINER ID   IMAGE               STATUS
1f85f1c17610   otaviodantas/init   Created
```

O comando responsável por iniciar é o ***start**.*

``` Bash
docker start <CONTAINER ID>
```

## **5º Etapa: Executando o script dentro do contêiner.**

<p style='text-align: justify;'>
Como não consegui executar o comando logo na sua criação, vou precisar entrar no contêiner para rodar o script pelo terminal. Para isso vou usar o comando:
</p>

``` Bash
docker exec -it <CONTAINER ID> bash
```

- **exec** serve para executar qualquer coisa que venha depois dele.
- **it** determina que a execução seja interativa.
- **bash** é o interpretador de comandos.

Teremos algo como isso:

``` Bash
root@1f85f1c17610:/scr#
```

<p style='text-align: justify;'>
A partir daqui todos os comandos que dermos serão executados diretamente no dentro do contêiner.
Para que eu execute o script principal, nomeado como main.py, basta:
</p>

``` Bash
python main.py
```

O programa irá rodar normalmente e teremos a saída no próprio terminal dessa forma:

![https://miro.medium.com/max/905/1*EqD9cFmG5_BGcq3nDnXdXw.png](https://miro.medium.com/max/905/1*EqD9cFmG5_BGcq3nDnXdXw.png)

## **6º Etapa: Verificando no Banco de dados.**

Vou usar os mesmo princípios usados na seção acima para entrar no contêiner do banco.

``` Bash
$ docker exec -it <CONTAINER ID> bash
root@<CONTAINER ID>:/## mysql -u root -p
Enter password:
```

<p style='text-align: justify;'>
A senha do banco foi especificada dentro do arquivo DockerFile, <b>RootPassword.</b>
Dentro da estrutura SQL, vou até a tabela onde estão salvos os meu dados e seleciono toda a tabela, o resultado:

![https://miro.medium.com/max/1094/1*z_beiy2LYSmmqmgxOlQBrA.png](https://miro.medium.com/max/1094/1*z_beiy2LYSmmqmgxOlQBrA.png)

``` Bash
7866 rows in set (0.01 sec)
```

## **Dificuldades encontradas.**

![https://miro.medium.com/max/1094/0*4Us_zfWpzheiSJfL.jpg](https://miro.medium.com/max/1094/0*4Us_zfWpzheiSJfL.jpg)

<p style='text-align: justify;'>
O projeto principal contava com o docker compose, porém, quando o contêiner do banco era iniciado, ele travava os logs e impedia que o restante do processo continuasse. Passei muito tempo parado nesse bug e por fim optei por criar as imagens na mão e roda’-las da mesma forma. Se alguém já passou por um problema semelhante, por favor entrar em contato kkk.
</p>

<p style='text-align: justify;'>
Outro problema foi o comando run, com a imagem Python, o processo simplesmente não prosseguia, ficava perpetuamente parado abaixo da linha de comando.
</p>

## **Ideias futuras**

- Usar o Docker Compose para inciar os dois contêineres simultaneamente.
- Hospedar a aplicação em uma máquina de Free Tier na AWS(EC2).

## **Conclusão**

<p style='text-align: justify;'>
Durante todo o processo de construção do ambiente, o Docker se mostrou uma ferramenta extremamente prática e com uma linha de aprendizado exponencial, você consegue colocar a sua aplicação caseira sem muitas complicações no ar.
</p>