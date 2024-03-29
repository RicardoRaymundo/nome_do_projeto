# Comando Flutter!

### Comando comuns:
|           Comando Flutter           |                                  Descrição                                  |
|-------------------------------------|-----------------------------------------------------------------------------|
| flutter create <diretório de saída> | Cria uma nova aplicação Flutter em um diretório específico                  |
| flutter run <opções>                | Execute o aplicativo Flutter em um dispositivo conectado ou em um emulador. |

Uso: flutter `<comando> <argumentos>`


### Opções globais:

| Comando Flutter      |                                                                     Descrição                                                                    |
|:---------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------|
| -h, --help           | Imprima essas informações gerai de uso do Flutter.                                                                                                                |
| -v, --verbose        | Imprime log detalhado, incluindo todos os comandos do shell executados. Se usado com --help, mostra opções ocultas.                                |
| -d, --device-id      | ID ou nome do dispositivo de destino (prefixos permitidos).                                                                                      |
| --version            | Imprime a versão do Flutter.                                                                                                                |
| --suppress-analytics | Suprime os relatórios analíticos quando este comando é executado.                                                                              |
| --bug-report         | Captura um arquivo de relatório de bug para enviar à equipe do Flutter. Contém caminhos locais, identificadores de dispositivo e trechos de log. |
| --packages           | Caminho para o seu arquivo ".packages".  (obrigatório, pois o diretório atual não contém um arquivo ".packages")                                 |


### Comandos disponíveis:

| Comando Flutter       |                                                           Descrição                                                          |
|:----------------------|:-----------------------------------------------------------------------------------------------------------------------------|
| analyze               | Analise o código Dart do projeto.                                                                                            |
| assemble              | Monte e crie recursos de Flutter                                                                                             |
| attach                | Anexe a um aplicativo em execução.                                                                                           |
| bash-completion       | Scripts de instalação de conclusão do shell da linha de comando.                                                             |
| [build](build.md)                 | Comandos de criação do Flutter.                                                                                              |
| [channel](channel.md) | Listar ou alternar os canais de Flutter.                                                                                     |
| clean                 | Exclua os diretórios build/ e .dart_tool/.                                                                                   |
| config                | Defina as configurações do Flutter.                                                                                          |
| create                | Crie um novo projeto Flutter.                                                                                                |
| devices               | Lista todos os dispositivos conectados.                                                                                      |
| doctor                | Mostrar informações sobre as ferramentas instaladas.                                                                         |
| drive                 | Executa os testes do Flutter Driver para o projeto atual.                                                                    |
| emulators             | Lista, inicia e cria emuladores.                                                                                             |
| format                | Formate um ou mais arquivos Dart.                                                                                            |
| generate              | Executar geradores de código.                                                                                                |
| help                  | Exibir informações de ajuda para o Flutter.                                                                                  |
| install               | Instale um aplicativo Flutter em um dispositivo conectado.                                                                   |
| logs                  | Mostrar saída de log para executar aplicativos Flutter.                                                                      |
| make-host-app-editble | Move aplicativos host de diretórios gerados para diretórios não gerados, para que possam ser editados pelos desenvolvedores. |
| precache              | Preenche o cache de artefatos binários da ferramenta Flutter.                                                                |
| pub                   | Comandos para gerenciar pacotes Flutter.                                                                                     |
| run                   | Executa o aplicativo Flutter em um dispositivo conectado.                                                                    |
| screenshot            | Tira uma captura de tela de um dispositivo conectado.                                                                        |
| test                  | Executa testes unitários Flutter para o projeto atual.                                                                       |
| upgrade               | Atualiza sua cópia do Flutter.                                                                                               |
| version               | Lista ou alternar as versões do Flutter.                                                                                    |

Execute `flutter <comando> -h` para mais informações sobre o comando

Execute `flutter help -v` para obter ajuda detalhada, incluindo opções menos usadas.

### Hot Reload 
O recurso Hot Reload do Flutter ajuda você a experimentar rápido e facilmente, criar UIs, adicionar recursos e corrigir bugs.
Para saber mais: [Hot Reload](https://flutter.dev/docs/development/tools/hot-reload)

[Difference between Hot Reload and Hot Restart](https://flutter-examples.com/difference-between-hot-reload-and-hot-restart-in-flutter-dart/)

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| r               | Cmd + \ |Hot Reload compila rapidamente o código recém-adicionado e envia o código para o Dart Virtual Machine. Depois de atualizar a máquina virtual, atualiza a interface do usuário do aplicativo com widgets.                                                                | r                                     |
| Shift + r               | Shift + Cmd + \ | Hot Restart destrói o valor dos States preservados e os re-definem para o default. Portanto, se você estiver usando States em seu aplicativo, após cada Hot Restart, o aplicativo é totalmente compilado e todos os States serão definidos para default. A árvore de widgets do aplicativo é completamente reconstruída.                                                                 | r                                     |

### Devices
| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| devices       || Liste todos os dispositivos conectados. [Set up your Android device](https://flutter.dev/docs/get-started/install/windows#set-up-your-android-device)  | flutter devices                       |

