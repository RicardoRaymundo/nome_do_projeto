[Flutter comandos](README.md)

1. [Crie uma nova aplicação web](#crie-uma-aplicação-web)
1. [Execute uma aplicação web](#execute-uma-aplicação-web)
1. [Compile uma aplicação web](#compile-uma-aplicação-web)

## Web
### Crie uma aplicação Web
Siga os passos para criar uma aplicação web. Para saber mais: [Building a web application with Flutter](https://flutter.dev/docs/get-started/web)
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| channel              |         | Altere o canal para dev.                                      | flutter channel dev    |


-------------

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| upgrade              |         | Atualize o Flutter SDK.                                      | flutter upgrade    |



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

### Compile uma aplicação web
Siga os passos para compilar uma aplicação web. Para saber mais: [Build](#build). 
[Preparing an web app for release](https://flutter.dev/docs/deployment/web) 
> Abra o terminal/prompt de comando.

| Comando         |Atalho   | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| cd              |         | Entre no diretório da aplicação.                                                                                                                          | cd `<diretório do projeto>`           |
| build             || Execute o comando de criação do Flutter.                                                                                                                          | flutter build web                           |
| cd             || Entre no diretório de compilação web.                                                                                                                          | `<diretório do projeto>`/build/web                           |

*Caso a pasta 'build' não esteja visível no Android Studio, delete a linha `<excludeFolder url="file://$MODULE_DIR$/build" />` do arquivo **nome_do_projeto.iml** na pasta raiz.