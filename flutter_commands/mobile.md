[Flutter comandos](README.md)

1. [Crie uma nova aplicação mobile](#Crie-uma-nova-aplicação-mobile)
1. Crie uma nova aplicação mobile AndroidX
1. Execute uma aplicação mobile
1. Compile uma aplicação mobile

2. [Crie uma nova aplicação mobile](#Crie-uma-nova-aplicação-mobile)
2. Crie uma nova aplicação mobile AndroidX
2. Execute uma aplicação mobile
2. Compile uma aplicação mobile


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
Siga os passos para compilar uma aplicação mobile. Para saber mais: [Build](#build), 
[Preparing an Android app for release](https://flutter.dev/docs/deployment/android), 
[Flutter's build modes](https://flutter.dev/docs/testing/build-modes)
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| cd              |         | Entre no diretório da aplicação.                                                                                                                          | cd `<diretório do projeto>`           |
| build             || Execute o comando de criação do Flutter.                                                                                                                          | flutter build `<tipo de build>` --release                           |
| cd             || Entre no diretório de compilação Android.                                                                                                                          | `<diretório do projeto>`/build/app/outputs/apk/release                           |

*Caso a pasta 'build' não esteja visível no Android Studio, delete a linha `<excludeFolder url="file://$MODULE_DIR$/build" />` do arquivo **nome_do_projeto.iml** na pasta raiz.
