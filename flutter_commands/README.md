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
| build                 | Comandos de criação do Flutter.                                                                                              |
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
| run                   | Executa o aplicativo Flutter em um dispositivo conectado.                                                                    |
| screenshot            | Tira uma captura de tela de um dispositivo conectado.                                                                        |
| test                  | Executa testes unitários Flutter para o projeto atual.                                                                       |
| upgrade               | Atualiza sua cópia do Flutter.                                                                                               |
| version               | Lista ou alternar as versões do Flutter.                                                                                    |

Execute `flutter help <comando>` para mais informações sobre o comando

Execute `flutter help -v` para obter ajuda detalhada, incluindo opções menos usadas.

### Build

Para saber mais: [Preparing an Android app for release](https://flutter.dev/docs/deployment/android), 
[Flutter's build modes](https://flutter.dev/docs/testing/build-modes)

| Comando       | Descrição                                                                                                                    |
|---------------|------------------------------------------------------------------------------------------------------------------------------|
| aar           | Cria um repositório contendo um arquivo AAR e POM. PESQUISAR AAR E POM                                                                          |
| aot           | Cria um snapshot compilado antecipadamente do código Dart do seu aplicativo. PESQUISAR AOT                                                |
| apk           | Cria um arquivo APK do Android a partir do seu aplicativo.                                                                   |
| appbundle     | Cria um arquivo Bundle de aplicativos Android a partir do seu aplicativo. PESQUISAR APP BUNDLE                                                    |
| bundle        | Cria o diretório de assets do Flutter no seu aplicativo.                                                                     |
| ios           | Cria um bundle de aplicativo iOS (somente host do Mac OS X).                                                                 |
| ios-framework | Cria um diretório .framework para um módulo Flutter e seus plugins para integração em projetos Xcode simples e existentes. |
| web           | Cria um pacote de aplicativos web.                                                                                      |

### Canais
O Flutter possui os seguintes [canais](https://github.com/flutter/flutter/wiki/Flutter-build-release-channels), em ordem crescente de estabilidade:

| Channels | Descrição                                                                                                                                                            |
|:--------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| master | A atual base da árvore, a mais recente construção. Geralmente funcional, embora às vezes quebremos acidentalmente as coisas.                    |
| dev    | A versão mais recente e totalmente testada. Geralmente funcional, mas consulte [Bad Builds](https://github.com/flutter/flutter/wiki/Bad-Builds) para obter uma lista de construções de desenvolvimento "ruins" conhecidas. |
| beta   | Todos os meses, escolhemos o "melhor" desenvolvedor do mês anterior e o promovemos para a versão beta. Essas versões foram testadas com os [codelabs](https://github.com/flutter/flutter/wiki/Codelabs).                 |
| stable | Quando acreditamos que temos uma construção particularmente boa, a promovemos para o canal estável.                                                                  |

Para trocar o canal:

| Comando         | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| channel         |  Liste os canais de Flutter.                                     | flutter channel    |
| channel         |  Troque os canais de Flutter.                                     | flutter channel `<channel>`   |

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


## Mobile
### Crie uma nova aplicação mobile
Siga os passos para criar uma aplicação mobile. Para saber mais: [Write your first Flutter app](https://flutter.dev/docs/get-started/codelab)
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| cd              |         | Entre no diretório onde deseja criar sua aplicação.                                      | cd `<diretório desejado>`    |
| create          |         | Crie uma nova aplicação Flutter.                                      | flutter create `<nome do projeto>`    |

### Crie uma nova aplicação mobile AndroidX
Siga os passos para criar uma aplicação mobile AndroidX. Para saber mais: [Migrando para AndroidX](https://flutter.dev/docs/development/androidx-migration) 
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| cd              |         | Entre no diretório onde deseja criar sua aplicação.                                      | cd `<diretório desejado>`    |
| create          |         | Crie uma nova aplicação Flutter com Android X.                                      | flutter create --androidx `<nome do projeto>`    |

### Execute uma aplicação mobile
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| cd              |         | Entre no diretório da aplicação                                                                                                                          | cd `<diretório do projeto>`           |
| run             || Execute o aplicativo Flutter no dispositivo default.                                                                                                                          | flutter run                           |
| --device-id | -d |Execute o aplicativo Flutter em um dispositivo conectado pelo ID ou nome do dispositivo de destino (prefixos permitidos).                              | flutter --device-id `<device id>` run |

### Compile uma aplicação mobile
Siga os passos para compilar uma aplicação mobile. Para saber mais sobre os tipos de compilação: [Build](#build) 
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| cd              |         | Entre no diretório da aplicação.                                                                                                                          | cd `<diretório do projeto>`           |
| build             || Execute o comando de criação do Flutter.                                                                                                                          | flutter build `<tipo de build>` --release                           |
| cd             || Entre no diretório de compilação Android.                                                                                                                          | build/app/outputs/apk/release                           |


## Web
### Crie uma aplicação Web
Siga os passos para criar uma aplicação web. Para saber mais: [Building a web application with Flutter](https://flutter.dev/docs/get-started/web)
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| channel              |         | Altere o canal para dev.                                      | flutter channel dev    |
| upgrade              |         | Atualize o Flutter SDK.                                      | flutter upgrade    |
| config              |         | Habilite o suporte para web. Para desabilitar, utilize `--no-enable-web`.          | flutter config --enable-web    |
| cd              |         | Entre no diretório onde deseja criar sua aplicação.                   | cd `<diretório desejado>`    |
| create          |         | Crie uma nova aplicação Flutter. Caso já tenha uma aplicação criada, execute `flutter create .`                                     | flutter create `<nome do projeto>`    |

### Execute uma aplicação web
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| cd              |         | Entre no diretório do projeto                                                                                                                          | cd `<diretório do projeto>`           |
| --device-id | -d | Execute o aplicativo Flutter em um dispositivo conectado pelo ID ou nome do dispositivo de destino (prefixos permitidos).                              | flutter -d chrome run |
