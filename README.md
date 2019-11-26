# **Manual de criação de aplicações Flutter (Mobile/Web)**

Manual de criação de aplicações Flutter para mobile e web 


## Conteúdo
1. [Instalar](#instalar)
1. [Passo à passo](#passo-à-passo)
    * [Aplicação Mobile](#aplicação-mobile) 
    * [Aplicação Mobile(AndroidX)](#Aplicação-Mobile(AndroidX))
    * [Aplicação Web]
1. [Aprender](#aprender)
1. [Agradecimentos](#Agradecimentos)
1. [Licença](#licença)

## Instalar
[Instale o Flutter](https://flutter.dev/docs/get-started/install)


## Passo à Passo
> Abra o terminal/prompt de comando para realizar o passo à passo

### Aplicação Mobile
#### 1. Crie um novo projeto
[Flutter - Write your first Flutter app, part 1](https://flutter.dev/docs/get-started/codelab)

Selecione uma pasta pelo terminal/prompt e execute
```
flutter create nome_do_projeto
```

#### 2.  Selecione o projeto

```
cd nome_do_projeto
```


#### 3.  Verifique se há dispositivos disponíveis

```
flutter devices
```
 
> Procure por:  "Set up your Android device" [neste link](https://kobiton.com/topics/develop-deploy-and-test-flutter-apps/)

#### 4.  Execute o app

```
flutter run
```

#### 5.  Execute o "Hot Reload"
`r`
> Saiba mais sobre o [Hot Reload](https://flutter.dev/docs/development/tools/hot-reload)

### Aplicação Mobile(AndroidX)
#### 1. Crie um novo projeto
Crie o projeto com AndroidX, a versão melhorada da Support Library
```
flutter create --androidx -t tipo_do_projeto path_do_projeto

Exemplo:
flutter create --androidx -t app /Users/macbookpro/AndroidStudioProjects/nome_do_projeto
```
> Saiba mais sobre [Migrando para AndroidX](https://flutter.dev/docs/development/androidx-migration) 

#### 2.  Selecione o projeto

```
cd nome_do_projeto
```


#### 3.  Verifique se há dispositivos disponíveis

```
flutter devices
```
 
> Procure por:  "Set up your Android device" [neste link](https://kobiton.com/topics/develop-deploy-and-test-flutter-apps/)

#### 4.  Execute o app

```
flutter run
```

#### 5.  Execute o "Hot Reload"
`r`
> Saiba mais sobre o [Hot Reload](https://flutter.dev/docs/development/tools/hot-reload)

### Aplicação Web
[flutter.dev/docs/get-started/web](https://flutter.dev/docs/get-started/web)
#### 1.  Altere o channel para dev

```
flutter channel dev
```

> Saiba mais sobre 
[Flutter build release channels](https://github.com/flutter/flutter/wiki/Flutter-build-release-channels)
, e [Trocando os canáis do Flutter](https://flutter.dev/docs/development/tools/sdk/upgrading#switching-flutter-channels)
#### 2.  Atualize o Flutter SDK

```
flutter upgrade
```


#### 3.  Habilite o suporte para web

```
flutter config --enable-web
```

e para desabilitar

```
flutter config --no-enable-web
```


#### 4.  Verifique se há o Chrome como dispositivo disponível

```
flutter devices
```


#### 5. Habilite o suporte para web em um projeto já criado
Selecione o projeto
```
cd nome_do_projeto
```

Agora execute o comando
```
flutter create .
```



## Aprender

[Comandos Dart, Pub e Flutter](https://dartcode.org/docs/commands)


[flutter.dev/docs/get-started/test-drive](https://flutter.dev/docs/get-started/test-drive?tab=terminal#vscode)

[https://flutter.dev/docs/get-started/codelab](https://flutter.dev/docs/get-started/codelab)


## Licença

MIT License

Copyright (c) 2019 Ricardo Raymundo

É concedida permissão, gratuitamente, a qualquer pessoa que obtenha uma cópia deste software e dos arquivos de documentação associados (o "Software"), para negociar o Software sem restrições, incluindo, sem limitação, os direitos de uso, cópia, modificação e fusão , publicar, distribuir, sublicenciar e / ou vender cópias do Software, e permitir que as pessoas a quem o Software é fornecido o façam, sujeitas às seguintes condições:

O aviso de copyright acima e este aviso de permissão devem ser incluídos em todas as cópias ou partes substanciais do Software.

O SOFTWARE É FORNECIDO "NO ESTADO EM QUE SE ENCONTRA", SEM NENHUM TIPO DE GARANTIA, EXPRESSA OU IMPLÍCITA, INCLUINDO, MAS NÃO SE LIMITANDO ÀS GARANTIAS DE COMERCIALIZAÇÃO, ADEQUAÇÃO A UM FIM ESPECÍFICO E NÃO VIOLAÇÃO. EM NENHUMA CIRCUNSTÂNCIA, OS AUTORES OU PROPRIETÁRIOS DE DIREITOS DE AUTOR PODERÃO SER RESPONSABILIZADOS POR QUAISQUER REIVINDICAÇÕES, DANOS OU OUTRAS RESPONSABILIDADES, QUER EM ACÇÃO DE CONTRATO, DELITO OU DE OUTRA FORMA, DECORRENTES DE, OU EM CONEXÃO COM O SOFTWARE OU O USO OU OUTRAS NEGOCIAÇÕES NO PROGRAMAS.
