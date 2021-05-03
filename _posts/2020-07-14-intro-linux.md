---
layout: post
title:  "Introdução ao Linux (para iniciantes)"
date:   2020-07-14
comments: true
---

![Linux yaaaaaaay](https://media.giphy.com/media/3og0ICG4WxdKSRzE3K/giphy.gif)  

<br/>

Oi, gente!

Andei meio sumida daqui - de novo - por conta de texto de mestrado pra enviar pra banca (foi enviado na última sexta ihuuu), tela de *software* pra prototipar, casa e vida em meio a pandemia acontecendo, UFA! Mas as coisas estão um tantinho mais tranquilas e, pensando nas coisas que eu tinha pra falar - obrigada [Dandara](https://twitter.com/dandaramcsousa) por me fazer pensar nisso - e vim fazer um compilado de um minicurso de Introdução ao Linux que eu já dei pelo [Diretório Acadêmico Ada Lovelace](https://www.instagram.com/daal.ufrn/)), do [IMD](https://imd.ufrn.br/) um tempo atrás e resolvi criar um blogpost a partir dele. Nesse post então vou tratar um pouco do histório do Linux, explicar o que é, falar de distribuições e alguns comandos básicos :)

# O que é o Linux (um pouquinho de história)
Linux é, na verdade, um *kernel*, o núcleo do sistema operacional. O *kernel* Linux é, no caso, o componente principal de um sistema operacional Linux. O que ele faz é intermediar a comunicação entre o *hardware* e a unidade de processamento do dispositivo que ele roda, gerindo os recursos da melhor forma possível.

*Fun fact*: o *kernel Linux* é o **MAIOR** projeto *open source* do mundo, e está disponível [aqui](https://github.com/torvalds/linux). Seu nome vem da brincadeira Linus + Unix. O primeiro é o nome do criador do Linux, Linus Torvalds. E o segundo, Unix, é o nome de um sistema operacional, criado por vários engenheiros e pesquisadores. O projeto Unix era realizado por vários ógãos, como o Massachusets Institute of Technology (MIT), General Eletric (GE), Bell Labs e American Telephone and Telegraph (AT&T).

Tudo isso aconteceu na década de 60, e o Unix passou por várias modificações por parte dessas instituições, sendo elas de código fechado. Aí que entra o Minix - peça chave para a criação do Linux. O Minix é uma versão *open source* do Unix, criado originalmente para uso educacional, para quem quisesse estudar Unix de casa. Importante ressaltar que, apesar do Minix ser uma versão do Unix, não contém nenhum código da AT&T e por isso podia ser distribuído gratuitamente.

Aí que chegamos em **Linux = Linux + Unix**: Linus decidiu então desenvolver um sistema mais poderoso que o Minix. Em 1991, ele disponibilizou a versão do *kernel* na versão 0.02 e continuou trabalhando nele, até que em 1994 disponibilizou a versão 1.0.

Observação: no meio de tuuuuuuudo isso, ainda temos o projeto GNU. Essa iniciativa iniciou 1984, que também queria desenvolver um SO que fosse compatível com o padrão Unix. Na época que Linus Torvalds estava desenvolvendo o *kernel* do Linux, começou a usar programas do projeto GNU pra fazer o seu sistema operacional. Aí ele acabou deixando o seu *kernel* com a mesma licença. Por conta desse uso de variantes GNU junto do *kernel* Linux, este se tornou um sistema operacional.


# Caracterização

## O  Linux  está  sob  a  licença  GPL
A General Public License (Licença Pública Geral, livremente traduzido) é a licença para *software* idealizada por Richard Stallman, no final da década de 80. Originalmente essa Licença foi criada pro projeto GNU, acordado com as definições de *software* livre da [Free Software Foundation](https://www.fsf.org/pt-br).

A GPL está baseada em quatro liberdades, a saber:
* A liberdade de executar o programa, para qualquer propósito (liberdade nº 0)
* liberdade de estudar como o programa funciona e adaptá-lo às suas necessidades (liberdade nº 1). O acesso ao código-fonte é um pré-requisito para esta liberdade.
* A liberdade de redistribuir cópias de modo que você possa ajudar ao seu próximo (liberdade nº 2).
* A liberdade de aperfeiçoar o programa e liberar os seus aperfeiçoamentos, de modo que toda a comunidade beneficie deles (liberdade nº 3). O acesso ao código-fonte é um pré-requisito para esta liberdade.

Dessa forma, o Linux é livre  para  uso, tem o código-fonte  aberto, pode  ser  modificado e não  pode  ser  usado  para  produzir  programas fechados  com  fins  exclusivamente  comerciais.

## O  Linux  não  é  vulnerável  a  vírus (?)
![Quando me dizem que Linux tem vírus...](https://media.giphy.com/media/l0Hlw1wlzvxTvxiZG/giphy.gif)

Muita gente pensa que o Linux não é vulnerável a vírus... mas o que realmente acontece? No Linux, temos bem forte a separação  de  privilégios  entre  processos, além de um padrão  de  política  de  segurança  para  uso  de contas  privilegiadas, o que pode evitar muita coisa, como usuários acabarem fazendo besteira porque tem alguma permissão inadequada. No entanto, o  Linux  é  alvo  de  “*exploits*”. O que seriam esses *exploits*: um pedaço de *software* que se aporoveita de algum defeito, falha ou vulnerabilidade do sistema, com fim de causar um comportamento imprevisto no sistema. Eles se aproveitam de  falhas  em  sistemas  desatualizados, então utilizar distribuições  bem  mantidas  e  atualizadas resolvem  tal  problema :)

## Sistema de arquivos
  O sistema de arquivos é criado durante a formatação do disco, no processo de instalação do sistema operacional. Esse processo gera toda a estrutura para leitura e gravação de arquivos e diretórios pelo sistema operacional. Durante certo tempo foi mais utilizado o sistema de arquivos ext2 (Linux Native) no Linux. Atualmente, são mais usados sistemas de arquivos com recursos de *journaling* (ext3, ext4, reiserfs, xfs,...). E o que danado são sistemas de arquivos com *journaling*? São sistemas que registram de antemão numa área especial do disco, chamada *journal*, as alterações que realizará no disco. Dessa forma, possibilita que erros de gravação causados por queda de energia ou desligamento incorreto sejam mais facilmente solucionados e diagnosticados.


## Filesystem Hierarchy Standard (aka hierarquia padrão de sistema de arquivos)
As partições do disco são acessadas através de diretórios (pastas). Para que essas partições - os arquivos contidos nelas - sejam acessívels, é necessário que haja um processo de vinculação do sistema de arquivos a um diretório, cujo nome é denominado montagem. Dessa forma, os diretórios a partir dos quais as partições são acessadas são chamados de pontos de montagem.

No Linux, todo arquivo possui uma localização adequada conforme sua finalidade, padrão conhecido como ***Filesystem Hierarchy Standard (FHS)***. Deve-se observar que alguns dos diretórios devem, obrigatoriamente, permanecer na mesma partição do diretório raiz (/). Já os demais podem ser pontos de montagem para outras partições ou dispositivos.

![Hierarquia padrão do sistema de arquivos do Linux](https://img.vivaolinux.com.br/imagens/artigos/comunidade/Artigo_01.jpg)

# Distribuições Linux
![Distribuições Linux](https://miro.medium.com/max/596/1*75iMyS-b0IQvWiJAk1xMQA.png)
Existem **centenas** de distribuições Linux para escolher. Como *kernel é open source*, basicamente qualquer pessoa tem permissão para usar e contruir seu próprio sistema operacional, totalmente customizável. [Aqui](https://pt.wikipedia.org/wiki/Lista_de_distribui%C3%A7%C3%B5es_de_Linux) tem uma lista em Português com as distribuições Linux disponíveis, desde distros para iniciantes, deficientes visuais, crianças, uso geral etc. Apesar da lista grande, para uso geral, o Ubuntu, Fedora e Debian são bastante populares.

# Primeiro exemplo: o diretório /dev

Os dispositivos de *hardware* do computador são identificados por arquivos no diretório /dev. Nele a gente consegue identificar os discos no Linux.

Comando para listar o conteúdo do diretório `/dev`

    $ ls -l /dev

Nesse caso, vou exemplificar com uma saída que esse comando pode mostrar, sendo executado numa máquina.
```
$ ls -l /dev
/dev/sda1
```

Nesse caso, temos a identificação do disco ``` sda1 ```, sendo:
* `/dev` - diretório dos dispositivos
* `sd` - sigla que identifica tipo de disco
  - `sd` - SCSI
  - `hd` - disco IDE
* `a` - letra que identifica um determinado disco
  - `a` = primeiro, b = segundo…
  - `1` - número que identifica a partição no disco



# Comandos
![Vamos aprender comandos!](https://media.giphy.com/media/4Zgy9QqzWU8C3ugvCa/giphy.gif)

Com os comandos que vou explicar abaixo, você poderá, diretamente do terminal, realizar algumas atividades no seu sistema. Lembrando que essas ações também podem ser feitas no "Explorer" do seu sistema, mas é interessante conhecer essa forma de fazer no terminal.

Também é importante saber que os comandos tem uma sintaxe a ser seguida, a saber:

```
comando < opções < argumentos
```

E de tooooooodos, o comando mais importante pra saber é o **man**!
```
man comando-a-ser-pesquisado
```
O comando `man` (acrônimo de "manual"), traz um manual do comando que você passar como opção, sendo de grande valia pra saber mais sobre algum comando!

Agora vamos aos comandos?

## Comandos para manipulação de arquivos e diretórios

Comando `pwd`

```
$ pwd
```

Informa o nome do diretório corrente, mostrando o seu caminho desde a raiz (/). É o acrônimo de *"print working directory"*.

Comando `ls`

```
$ ls
```
Lista o conteúdo do diretório no qual você estiver, como pastas e arquivos. ele tem algumas opções bem úteis como `-l`, que lista o conteúdo do diretório mostrando as permissões que o usuário tem, quem é o dono do arquivo, entre outras informações, `-a`, que lista TODO o conteúdo do diretório, mesmo que por padrão alguns desses conteúdos estejam ocultos, etc.

Comando `cd`

```
$ cd caminho-do-diretório
```
Navega entre os diretórios. Usando o `cd`, dá pra entrar em diretórios anteriores ou subdiretórios do diretório qeu você se encontra.

Comando `mkdir`

```
$ mkdir nome-do-diretório-a-ser-criado
```
Cria novos diretórios. Importante lembrar que, para criar diretórios em alguns lugares específicos, como pastas na raiz do sistema (/), é necessário ter permissões de super usuário pra isso.

Comando `cp`

```
$ cp caminho-do-arquivo-pra-copiar caminho-que-o-arquivo-copiado-vai-ficar
```
Faz cópias arquivos e diretórios. Para fazer cópia de arquivo, você usa o comando como está no exemplo. Caso queira copiar um diretório, use o comando com a oção `-r`, que copia o diretório em questão com todo o conteúdo que estiver dentro dele.

Comando `mv`

```
$ mv caminho-do-arquivo-pra-mover caminho-que-o-arquivo-movido-vai-ficar
```
Move/renomeia arquivos ou diretórios.

Comando `rm`

```
$ rm nome-do-arquivo-pasta-a-deletar
```
Apaga arquivos de um  diretório ou o próprio diretório. No caso de se querer apagar um diretório e todo o seu conteúdo, se usa a opção `-r` para realizar essa ação.




## Comandos de filtragem

Comando `cat`

```
$ cat nome-do-arquivo
```
Exibe o conteúdo de um arquivo e faz concatenação diretamente on terminal.

Comando `wc`

```
$ wc nome-do-arquivo
```
Conta caracteres, palavras e linhas do arquivo passado e mostra no terminal.

Comando `sort`

```
$ sort nome-do-arquivo
```
Ordena o conteúdo de um arquivo e mostra o conteúdo ordenado no terminal. No caso de uma lista de palavras, por exemplo. Ele ordena em ordem alfabética. OBS: ele não modifica o arquivo, apenas ordena e mostra isso no terminal.

Comando `head`

```
$ head nome-do-arquivo
```
Exibe o início do arquivo. O padrão é mostrar as 10 primeiras linhas do arquivo.

Comando `tail`

```
$ tail nome-do-arquivo
```

Exibe o final do arquivo. O padrão é mostrar as 10 primeiras linhas do arquivo.


Comando `grep`

```
$ grep 'padrão-a-procurar' nome-do-arquivo
```

Procura arquivos por conteúdo. Ele busca por todas as palavras no arquivo passado que correspondam ao padrão colocado no comando.



## Mais uns comandinhos aqui

Nessa seção vou mostrar pra vocês alguns outros comandos, à medida que for vendo alguns interessantes para quem tá començando a se aventurar :D

Comando `touch`

```
$ touch nome-do-arquivo-a-ser-criado.extensão
```

Cria um novo arquivo. O `touch` é legal porque você pode passar a extensão do arquivo que quer criar também, mas isso é opcional. Quando a extensão não é passada, ele cria um arquivo de texto.


Comando `sudo/su`

```
$ sudo su
```

Troca para o super usuário do sistema, o usuário `root`. Tem alguns comandos que precisam de poderes a mais que um usuário comum não possui. Para isso, o `sudo su` vai mudar o seu *shell* (termina) para o *shell* do super usuário e, até que você use o comando `exit` você continua com os poderes de super usuário.

Comando `sudo`

```
$ sudo comando-a-ser-executado-como-super-usuario
```

Executa o comando passado com poderes de *root* (super usuário). Se você quer executar um comando só como super usuário, você pode usar o `sudo`.


**Só não esqueça.....**
![Com grandes poderes, vem grandes responsabilidades](https://i.gifer.com/5bme.gif)


<br/>
E esse foi o post de Introdução ao Linux! Espero que seja de valia para vocês! :D

<br/>
![Isso é tudo pessoal](https://media.giphy.com/media/l4pTjOu0NsrLApt0Q/giphy.gif)



**Referências**

[GNU General Public License](https://pt.wikipedia.org/wiki/GNU_General_Public_License#Conteúdo)

[História do Linux](https://brasilescola.uol.com.br/informatica/historia-do-linux.htm)
