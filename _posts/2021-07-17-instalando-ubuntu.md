---
layout: post
title:  "Intalando o Ubuntu 20.04.2.0 LTS - passo a passo"
date:   2021-07-17
comments: true
---

![Tux dançando](https://sempreupdate.com.br/wp-content/uploads/2019/10/tux-linux-gif.gif)  

<br/>

Oi, gente!

Logo mais às 13:30 de hoje, 17 de Julho de 2021, estarei dando um tutorial na [Python Nordeste](https://2020.pythonnordeste.org/) de introdução ao Linux!

Esse post nasce, então, como um registro de algo que adicionei no curso original que já ministrei outras vezes em eventos do [Diretório Acadêmico Ada Lovelace](https://twitter.com/daal_ufrn) (DAAL) do IMD. Como é um curso de introdução, para entender mais sobre a estrutura do sistema de arquivos do Linux, comandos etc, pensei em agregar a esse conteúdo como instalar o Ubuntu (distribuição Linux que escolhi) e mostrar nesse passo a passo que não tem tantos mistérios assim, risos.

Vamos começar?

## Softwares que usaremos
A ideia é simularmos a instalação do Ubuntu 20.04 como ela seria se fosse uma máquina real. Para isso, usaremos o software de virtualização Virtual Box [(aqui tu consegue acessar o site oficial do Virtual Box e fazer o download pra instalar na sua máquina)](https://www.virtualbox.org/). O VirtualBox é um software de código aberto, gratuito e multiplataforma que permite criar, gerenciar e executar máquinas virtuais (VMs) – computadores cujos componentes de hardware (como memória RAM e armazenamento) são emulados pelo computador hospedeiro, o computador que executa o programa. O VirtualBox roda em sistemas operacionais como Windows, Mac OS X, Linux e Solaris.

Além do Virtual Box, também precisaremos baixar a ISO do Ubuntu. E o que danado é uma ISO? O popular ISO é um formato de gravação para CDs e DVDs muito utilizado para softwares e sistemas operacionais, como o Windows. A sigla ISO significa Organização Internacional de Padronização (International Organization for Standardization, em inglês). Esse tipo de gravação permite manter os padrões originais com cópia em uma “imagem” perfeita. 

Lembra quando muito tempo atrás a gente precisava ter um CD ou DVD pra instalar um sistema operacional no nosso computador? Hoje podemos pegar um arquivo .ISO e colocar em uma mídia (como pen drive ou cartao SD) e usar para instalar o sistema operacional. Massa, né?

O arquivo ISO que vamos usar do Ubuntu 20.04.2.0 LTS pode ser baixado [aqui](https://ubuntu.com/download/desktop). Vamos usar essa versão LTS (long-term support) pois ela traz suporte de longo prazo - cinco anos, até abril de 2025, de segurança gratuita e atualizações de manutenção garantidas.

## Com o Virtual Box instalado e a ISO baixada, vamos lá!

Vamos por passos, ok?


### Criando uma Máquina Virtual no Virtual Box


![Criando VM](/assets/img/posts/criando-vm.gif)


No assistente:

* Clicar no botão "Novo"
* Nomeiar a VM e seleciona o tipo de Sistema Operacional e sua versão. No nosso caso, seleciona Linux e Ubuntu (32 ou 64 bits vai depender da sua máquina real  (hospedeira). 
Definir a quantidade de memória (RAM) a ser alocada para a máquina virtual
* Criar um disco rígido virtual a ser utilizado como disco de boot da máquina virtual (criaremos um novo, mas pode-se utilizar um disco virtual que já exista ou iniciar sem)
* Selecionar disco de tamanho dinamicamente alocado (à medida que vamos criando arquivo e instalando softwares, o disco vai aumentando de tamanho na máquina hospedeira)
* Definir tamanho máximo do disco virtual (20GB no nosso caso)

### Após a criação da máquina virtual, vamos configurar a ISO para instalar o sistema

![Configurando a VM antes de instalar o SO](/assets/img/posts/config-init.gif)


* Clicar em "Configurações" < Armazenamento
* Clicar em "Vazio" na Controladora IDE e selecionar o arquivo ISO correspondente ao SO que vamos instalar.
* Clicar em OK

### Vamos iniciar a máquina e fazer a instalação!

Primeira coisa que aparece é a tela de idioma, vamos lá!

![Selecionando idioma](/assets/img/posts/idioma.gif)

* Selecionar o idioma desejado
* Clicar em "instalar Ubuntu"


![Sem atualizações](/assets/img/posts/atualiza.gif)

* Clicar em "Instalação normal"
* Desativar "Baixar atualizações automáticas" (isso pode fazer a instalação demorar, no caso de a máquina hospedeira estar conectada à internet, pois ao invés de pegar os arquivos da ISO, baixa do repositório na internet) > Próximo

![Opções avançadas](/assets/img/posts/opavancada.gif)

* Clicar em opções avançadas (iremos criar uma tabela de particionamento, o que ajuda a ter mais autonomia no gerenciamento de disco)

#### ~ PARÊNTESE ~
Manipular de discos ou partições são muito comum, especialmente quando se desejar ter espaços mais reservados para arquivos específicos, ou quando se quer ter mais de um  sistema instalado na máquina.

Uma partição é um subconjunto de tamanho fixo de uma unidade de disco que é tratada como uma unidade pelo sistema operacional, indicando onde começa e onde termina uma região do disco rígido. Em relação aos tipos, temos partições primárias, estendidas e lógicas.

Partições primárias são partições que contém um sistema de arquivos. Normalmente, partições de sistemas operacionais. Já as partições estendidas são partições primárias especiais, que no lugar de receber um sistema de arquivos, contém outras partições lógicas.
Finalmente, as partições lógicas são aquelas partições que são criadas dentro das partições estendidas, e também recebem sistemas de arquivos.

Uma tabela de partição é uma tabela mantida no disco pelo sistema operacional que descreve as partições daquele disco, mantendo o "layout" das partições no disco.

#### ~ FECHA PARÊNTESE ~

![Criando tabela de partições](/assets/img/posts/part-tab.gif)

* Clicar em "Nova tabela de partição"
* Criar nova tabela de partições vazia
* Clicar em "Espaço livre" e depois no "+" (ou clicar duas vezes em "Espaço livre)
* Criar partição "/" do tipo primária, com 10GB, usar sistema de arquivos ext4 e ponto de montagem em "/"
* Clicar em "Espaço livre" e depois no "+" (ou clicar duas vezes em "Espaço livre)
* Criar partição "/" do tipo lógica, com 2GB, usar área de troca swap
* Clicar em "Espaço livre" e depois no "+" (ou clicar duas vezes em "Espaço livre)
* Criar partição "/" do tipo lógica, com 8GB, usar sistema de arquivos ext4 e ponto de montagem em "/home"
* Escrever mudanças nos discos

![Fuso e informações de usuário](/assets/img/posts/fuso-user.gif)

* Indicar onde você está (selecionar fuso horário)
* Fornecer informações do usuário (nome de usuário e senha - tem que ser senha forte)
* Finalizar instalação :)

Agora é só aguardar que em alguns minutos que o Ubuntu será instalado :)


Todo o passo a passo visual completo pode ser encontrado nesses vídeos:

[Configuração para criação de uma VM Ubuntu no Virtual Box](https://youtu.be/szqS5PFrEE0)

[Instalação do Ubuntu 20.04 LTS no Virtual Box](https://youtu.be/lalQERGYa48)


Espero que seja útil!

![Minha assinatura](/assets/img/signature.gif)
