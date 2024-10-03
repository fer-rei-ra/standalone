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

### Arquivo "start.bat"

Crie um novo arquivo de texto na pasta raiz do aplicativo. Renomeie o arquivo para start.bat (removendo o .txt). Clique com o botão direito e vá em editar (se você der dois cliques, ele irá rodar os comandos dentro dele, no caso ainda não há nenhum), com o editor de texto da sua escolha, copie os seguintes comandos:

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

### Arquivo "serverDZ.cfg"

Dentro da pasta raiz do aplicativo existe um arquivo chamado "serverDZ.cfg", clique para editar o arquivo com o editor de texto de sua escolha e, usando como base os comandos que estão presentes abaixo, edite de acordo com as suas preferências.


```
hostname = "EXAMPLE NAME";			// Nome do servidor
password = "";				        // Senha para entrar no servidor
passwordAdmin = "";				// Senha para entrar como Administrador

enableWhitelist = 0;				// Habilita ou Desabilita whitelist (1 = Habilitado, 0 = Desabilitado)
disableBanlist = false;				// Desativa o uso do ban.txt (Padrão = false)
disablePrioritylist = false;			// Desativa o uso do priority.txt (Padrão = false)

maxPlayers = 60;				// Número máximo de jogadores

verifySignatures = 2;				//  Verifica os arquivos .pbos em relação aos arquivos .bisign (Apenas o 2 é suportado)

forceSameBuild = 1;				// Quando ativado, o servidor permitirá a conexão somente de clientes com a mesma versão do .exe do servidor (1 = Habilitado, 0 = Desabilitado)

disableVoN = 0;					// Habilita ou Desabilita o Voice over Network, ou seja, comunicação por voz (1 = Habilitado, 0 = Desabilitado)
vonCodecQuality = 20;				// Qualidade do codec de voz baseado na rede, quanto maior, melhor (Valores de 0 à 20)

disable3rdPerson = 0;				// Habilita ou Desabilita a visualização em terceira pessoa para os jogadores (1 = Habilitado, 0 = Desabilitado)
disableCrosshair = 0;				// Habilita ou Desabilita a crosshair, ou seja, a mira (1 = Habilitado, 0 = Desabilitado)

serverTime = "SystemTime";			// Horário em que o jogo irá começar. "SystemTime" significa o horário local do computador.
						// Outra possibilidade é definir a hora como qualquer valor no formato "YYYY/MM/DD/HH/MM". Exemplo: "2015/4/8/17/23".

serverTimeAcceleration = 1;			// Accelerated Time - The numerical value being a multiplier (0.1-64).
						// Thus, in case it is set to 24, time would move 24 times faster than normal. An entire day would pass in one hour.

serverNightTimeAcceleration = 1;		// Accelerated Nigh Time - The numerical value being a multiplier (0.1-64) and also multiplied by serverTimeAcceleration value.
						// Thus, in case it is set to 4 and serverTimeAcceleration is set to 2, night time would move 8 times faster than normal.
						// An entire night would pass in 3 hours.

serverTimePersistent = 0;			// Persistent Time (value 0-1) - The actual server time is saved to storage, so when active, the next server start will use the saved time value.

guaranteedUpdates = 1;				// Communication protocol used with game server (use only number 1)

loginQueueConcurrentPlayers = 5;		// The number of players concurrently processed during the login process.
						// Should prevent massive performance drop during connection when a lot of people are connecting at the same time.

loginQueueMaxPlayers = 500;			// The maximum number of players that can wait in login queue

instanceId = 1;					// DayZ server instance id, to identify the number of instances per box and their storage folders with persistence files

storageAutoFix = 1;				// Checks if the persistence files are corrupted and replaces corrupted ones with empty ones (value 0-1)

class Missions
{
	class DayZ
	{
		template = "dayzOffline.chernarusplus";	// Mission to load on server startup. <MissionName>.<TerrainName>
	};
};

```
