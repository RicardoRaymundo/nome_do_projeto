# **Criando app Flutter**

Manual de criação de apps mobile e web para Flutter


## Conteúdo

1. [Passo à passo](#passo-à-passo)
1. [Aprender](#aprender)
1. [Agradecimentos](#Agradecimentos)
1. [Contribuir](#contribuir)
1. [Licença](#licença)

## Passo-à-Passo

### Mobile
#### 1. Crie um novo projeto

```
flutter create nome_do_projeto
```



**Recomendado** - Crie o projeto com AndroidX, a versão melhorada da Support Library


```
flutter create --androidx -t <project-type> <new-project-path>
```

#### 2.  Selecione o projeto

```
cd nome_do_projeto
```


#### 3.  Verificar se há dispositivos disponíveis

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

### Web
#### 1.  Alterar o channel para dev ou master

```
flutter channel dev
```
ou
```
flutter channel master
```


#### 2.  Atualizar o Flutter SDK

```
flutter upgrade
```


#### 3.  Habilitar o suporte para web

```
flutter config --enable-web
```


#### 4.  Verificar se há o Chrome como dispositivo disponível

```
flutter devices
```


#### 5. Habilitar o suporte para web em um projeto já criado

```
cd projeto_sem_web
```

```
flutter create .
```



## Aprender


[https://flutter.dev/docs/get-started/install](https://flutter.dev/docs/get-started/install)


[Comandos Dart, Pub e Flutter](https://dartcode.org/docs/commands/#flutter-new-project)


[flutter.dev/docs/get-started/test-drive](https://flutter.dev/docs/get-started/test-drive?tab=terminal#vscode)

[https://flutter.dev/docs/get-started/web](https://flutter.dev/docs/get-started/web)

[https://flutter.dev/docs/get-started/codelab](https://flutter.dev/docs/get-started/codelab)


## Contribuir

Contribuições são sempre muito bem vindas! Não precisam ser somente através de desenvolvimento de código, qualquer ajuda com ideias, sugestões, melhorias na documentação e doações são sempre muito apreciadas!

Participe da comunidade [Projeto que Vale](http://www.projetoquevale.com.br/) e colabore da forma que achar melhor.


## Licença

MIT License

Copyright (c) 2019 Ricardo Raymundo

É concedida permissão, gratuitamente, a qualquer pessoa que obtenha uma cópia deste software e dos arquivos de documentação associados (o "Software"), para negociar o Software sem restrições, incluindo, sem limitação, os direitos de uso, cópia, modificação e fusão , publicar, distribuir, sublicenciar e / ou vender cópias do Software, e permitir que as pessoas a quem o Software é fornecido o façam, sujeitas às seguintes condições:

O aviso de copyright acima e este aviso de permissão devem ser incluídos em todas as cópias ou partes substanciais do Software.

O SOFTWARE É FORNECIDO "NO ESTADO EM QUE SE ENCONTRA", SEM NENHUM TIPO DE GARANTIA, EXPRESSA OU IMPLÍCITA, INCLUINDO, MAS NÃO SE LIMITANDO ÀS GARANTIAS DE COMERCIALIZAÇÃO, ADEQUAÇÃO A UM FIM ESPECÍFICO E NÃO VIOLAÇÃO. EM NENHUMA CIRCUNSTÂNCIA, OS AUTORES OU PROPRIETÁRIOS DE DIREITOS DE AUTOR PODERÃO SER RESPONSABILIZADOS POR QUAISQUER REIVINDICAÇÕES, DANOS OU OUTRAS RESPONSABILIDADES, QUER EM ACÇÃO DE CONTRATO, DELITO OU DE OUTRA FORMA, DECORRENTES DE, OU EM CONEXÃO COM O SOFTWARE OU O USO OU OUTRAS NEGOCIAÇÕES NO PROGRAMAS.
