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
| -h, --help           | Imprima essas informações de uso.                                                                                                                |
| -v, --verbose        | Registro barulhento, incluindo todos os comandos do shell executados. Se usado com --help, mostra opções ocultas.                                |
| -d, --device-id      | ID ou nome do dispositivo de destino (prefixos permitidos).                                                                                      |
| --version            | Relata a versão desta ferramenta.                                                                                                                |
| --suppress-analytics | Suprima os relatórios analíticos quando este comando for executado.                                                                              |
| --bug-report         | Captura um arquivo de relatório de bug para enviar à equipe do Flutter. Contém caminhos locais, identificadores de dispositivo e trechos de log. |
| --packages           | Caminho para o seu arquivo ".packages".  (obrigatório, pois o diretório atual não contém um arquivo ".packages")                                 |


### Comandos disponíveis:

| Comando Flutter       |                                                           Descrição                                                          |
|:----------------------|:-----------------------------------------------------------------------------------------------------------------------------|
| analyze               | Analise o código Dart do projeto.                                                                                            |
| assemble              | Monte e crie recursos de Flutter                                                                                             |
| attach                | Anexe a um aplicativo em execução.                                                                                           |
| bash-completion       | Scripts de instalação de conclusão do shell da linha de comando.                                                             |
| build                 | Comandos de criação de Flutter.                                                                                              |
| channel               | Listar ou alternar os canais de Flutter.                                                                                     |
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
| run                   | Execute o aplicativo Flutter em um dispositivo conectado.                                                                    |
| screenshot            | Tire uma captura de tela de um dispositivo conectado.                                                                        |
| test                  | Execute testes unitários Flutter para o projeto atual.                                                                       |
| upgrade               | Atualize sua cópia do Flutter.                                                                                               |
| version               | Listar ou alternar as versões do Flutter.                                                                                    |

Execute `flutter help <comando>` para mais informações sobre o comando

Execute `flutter help -v` para obter ajuda detalhada, incluindo opções menos usadas.

### Crie app Mobile
#### 1. Crie um novo projeto

| Comando         | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| create          | Crie um novo projeto Flutter. [Write your first Flutter app, part 1](https://flutter.dev/docs/get-started/codelab)                                     | flutter create `<nome do projeto>`    |
| cd              | Entre no diretório do projeto                                                                                                                          | cd `<diretório do projeto>`           |
| devices         | Lista todos os dispositivos conectados. [Set up your Android device](https://flutter.dev/docs/get-started/install/windows#set-up-your-android-device)  | flutter devices                       |
| run             | Execute o aplicativo Flutter.                                                                                                                          | flutter run                           |
| -d, --device-id | Execute o aplicativo Flutter em um dispositivo conectado pelo ID ou nome do dispositivo de destino (prefixos permitidos).                              | flutter --device-id `<device id>` run |
| r               | Saiba mais sobre o [Hot Reload](https://flutter.dev/docs/development/tools/hot-reload)                                                                 | r                                     |

### Canais
