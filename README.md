# DayZ Standalone [PT-BR] W.I.P.

## 1. Introdução

Neste repositório você vai aprender como criar, trocar de mapa, adicionar mods e mudar os itens iniciais em um servidor 'Standalone' no DayZ. Você só vai conseguir realizar esses passos com o DayZ original da Steam e com um sistema operacional do Windows 10 ou superior. Este guia não tem o intuito de ser um tutorial de como jogar DayZ.
 
Para criar o nosso servidor vamos precisar das seguintes ferramentas: Windows 10 ou superior, um editor de texto da sua preferência para configurar os arquivos do servidor, se você não conhece nenhum eu recomendo o [Notepad++](https://notepad-plus-plus.org/downloads/) ou [Visual Studio Code](https://code.visualstudio.com/Download), e, para finalizar, vamos precisar do aplicativo 'DayZ Server' que vamos instalar pela Steam.

## 2. Instalando o 'DayZ Server'

Siga as instruções abaixo para instalar o aplicativo 'DayZ Server'.

 1. Abra e faça o login na Steam.
 2. Vá até a aba Biblioteca.
 3. Clique na aba que vai estar escrito 'Jogos, localizada acima da sua lista de jogos. [Imagem](https://prnt.sc/AisqsDSwcNoy)
 4. Ative a alternativa 'Ferramentas'. [Imagem](https://prnt.sc/BnnGXbihF8ZC)
 5. Procure e instale o aplicativo 'DayZ Server'. [Imagem](https://prnt.sc/wRsCVFLRz33g)

## 3. Criando o Servidor Local

Primeiramente, localize onde você instalou o aplicativo 'DayZ Server'. Por padrão ele irá para ```C:\Program Files (x86)\Steam\steamapps\common\DayZServer```. Porém, se você escolheu algum lugar diferente ou estiver esquecido onde instalou, vá até a sua biblioteca da Steam, localize o aplicativo, clique com o botão direito nele, vá em propriedades e clique em navegar pelos arquivos locais. Deste jeito você consegue achar a pasta raiz sem muitas dificuldades.

Crie um novo arquivo de texto na pasta raiz do aplicativo. Renomeie o arquivo para start.bat (removendo o .txt). Clique com o botão direito e vá em editar, se você der dois cliques, ele irá rodar os comandos dentro dele, no caso ainda não há nenhum, com o editor de texto da sua escolha copie os seguintes comandos:

```
@echo off

:start
::Nome do Servidor (Este nome é apenas para o arquivo .bat, não será o nome que aparecerá no launcher)
set serverName=DayZ server

::Localização dos arquivos do servidor
set serverLocation="C:\Program Files (x86)\Steam\steamapps\common\DayZServer"

::Porta do servidor
set serverPort=2302

::Arquivo de configuração do servidor
set serverConfig=serverDZ.cfg

::Núcleos da CPU à ser utilizado (O valor tem que ser igual ou menor do que os núcleos disponíveis)
set serverCPU=2

::Defina o título para o terminal (NÃO EDITE)
title %serverName% batch

::Localização do DayZServer (NÃO EDITE)
cd "%serverLocation%"
echo (%time%) %serverName% started.

::Parâmetros de inicialização (edite no final: -config=|-port=|-profiles=|-doLogs|-adminLog|-netLog|-freezeCheck|-filePatching|-BEpath=|-cpuCount=)
start "DayZ Server" /min "DayZServer_x64.exe" -config=%serverConfig% -port=%serverPort% -cpuCount=%serverCPU% -dologs -adminlog -netlog -freezecheck

::Tempo em segundos para desligar o servidor (14400 = 4 horas)
timeout 14390
taskkill /im DayZServer_x64.exe /F

::Tempo em segundos de espera antes de entrar no servidor
timeout 10

::Comando para o servidor continuar em funcionamento (NÃO EDITE)
goto start 

```
