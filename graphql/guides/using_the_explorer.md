|CONTEÚDOS                                                                                                                                      |
|-----------------------------------------------------------------------------------------------------------------------------------------------|
| [Visão global](README.md)                                                                                                                                   |   
| [Introdução ao GraphQL](introduction_to_graphql.md)                     |   
| [Formação de chamadas](forming-calls-with-graphql.md)    |   
| [Usando IDs de Nó Globais](using_global_node_ids.md)                    |   
| [Migrando do REST](migrating_from_rest_to_graphql.md)                   |   
| [Usando o Explorer](using_the_explorer.md)                              |   
| [Gerenciando contas corporativas](managing-enterprise-accounts.md)      |   
| [Limitações de recursos](graphql_resource_limitations.md)               |   

------------

[REFERENCIA](https://developer.github.com/v4/guides/using-the-explorer/)

# Usando o Explorer
1. [Sobre o Explorer](#sobre-o-explorer)
2. [Usando o GraphiQL](#usando-o-graphiql)
3. [Acessando os documentos da barra lateral](#acessando-os-documentos-da-barra-lateral)
4. [Usando o painel de variáveis](#usando-o-painel-de-variáveis)
5. [Solicitando suporte](#solicitando-suporte)
6. [Resolução de erros](#resolução-de-erros)

## Sobre o Explorer
[O GraphQL Explorer]() é uma instância do [GraphiQL](), que é um "IDE gráfico do GraphQL interativo no navegador".

> Nota : O GitHub desativou as mutações no Explorer, mas você pode usá-las em sua própria instância do GraphiQL.

Executar no Explorer
Acima de algumas amostras de consulta do GraphQL, você pode ver um link que diz "Executar no Explorer". Clique no link e você irá para a janela Explorer com o exemplo de consulta já preenchido. Você será solicitado a autorizar o aplicativo, se ainda não o tiver.

[Executar no Explorer]()

```graphql
query {
  viewer {
    login
    name
  }
}
```

Você deve ver uma resposta como a seguinte:

```graphql
{
  "data": {
    "viewer": {
      "login": "octocat",
      "name": "The Octocat"
    }
  }
}
```

## Usando o GraphiQL
Para usar o aplicativo GraphiQL, faça o download e instale-o em [https://github.com/skevy/graphiql-app]().

### Configurando o GraphiQL
1. Obtenha um [token OAuth]().
1. Inicie o GraphiQL.
1. No canto superior direito do GraphiQL, clique em **Editar cabeçalhos HTTP**.
1. No campo **Chave**, insira `Authorization`. No campo **Valor**, insira `Bearer <token>` onde `<token>` está o seu token OAuth gerado.
1. Clique na marca de seleção à direita do token para salvá-lo.
1. Para retornar ao editor, clique fora do modal **Editar Cabeçalhos HTTP**.
1. No campo **Ponto de extremidade** do **GraphQL**, insira [https://api.github.com/graphql]() .
1. No menu suspenso **Método**, selecione **POST**.

> Nota : Para obter mais informações sobre o motivo `POST` do método, consulte "[Comunicação com o GraphQL]()".

Você pode testar seu acesso consultando-se:

```graphql
query {
  viewer {
    login
  }
}
```

Se tudo funcionou corretamente, isso exibirá seu login. Você está pronto para começar a fazer consultas.

## Acessando os documentos da barra lateral

Todos os tipos em um esquema GraphQL incluem um `description` campo compilado na documentação. O painel **Documentos** dobráveis, no lado direito da página do Explorer, permite navegar na documentação sobre o sistema de tipos. Os documentos são atualizados automaticamente e eliminam os campos obsoletos.

> A barra lateral do **Documentos** contém o mesmo conteúdo que é gerado automaticamente a partir do esquema em "[Referência]()", embora seja formatado de maneira diferente em alguns locais.

## Usando o painel de variáveis

Alguns exemplos de chamadas incluem [variáveis]() escritas assim:

[Executar no Explorer]()

```graphql
query($number_of_repos:Int!){
  viewer {
    name
     repositories(last: $number_of_repos) {
       nodes {
         name
       }
     }
   }
}
variables {
   "number_of_repos": 3
}
```

Este é o formato correto para enviar a chamada por meio de um cURL `POST`(desde que você [escape de novas linhas]()).

Se você deseja executar a chamada no Explorer, insira o `query` segmento no painel principal e as variáveis ​​no painel **Variáveis ​​de Consulta** abaixo dele. Omita a palavra `variables` do Explorer:

```graphql
{
   "number_of_repos": 3
}
```

## Solicitando suporte

Para perguntas, relatórios de bugs e discussões sobre aplicativos GitHub, aplicativos OAuth e desenvolvimento de API, explore o [Fórum de suporte e desenvolvimento da API]() do [GitHub]() . O fórum é moderado e mantido pela equipe do GitHub, mas as perguntas postadas no fórum não garantem a resposta da equipe do GitHub.

Considere entrar em contato com o [suporte do GitHub]() diretamente usando o formulário de contato para:

- resposta garantida da equipe do GitHub
- solicitações de suporte que envolvam dados confidenciais ou preocupações particulares
- solicitações de recursos
- feedback sobre os produtos GitHub

## Resolução de erros
Como o GraphQL é [introspectivo](), o Explorer suporta:

- Tipeaheads inteligentes cientes do esquema atual
- O erro de validação é visualizado enquanto você digita

Se você inserir uma consulta que não está bem formada ou não passa na [validação do esquema](), um pop-up avisa sobre um erro. Se você executar a consulta, o erro retornará no painel de resposta.

Uma resposta do GraphQL contém várias chaves: um `data` hash e uma `errors` matriz.

```json
{
  "data": null,
  "errors": [
    {
      "message": "Objects must have selections (field 'nodes' returns Repository but has no selections)",
      "locations": [
        {
          "line": 5,
          "column": 8
        }
      ]
    }
  ]
}
```

É possível que você tenha um erro inesperado que não esteja relacionado ao esquema. Se isso acontecer, a mensagem incluirá um código de referência que você pode usar ao relatar o problema:

```json
{
  "data": null,
  "errors": [
    {
      "message": "Something went wrong while executing your query. This is most likely a GitHub bug. Please include \"7571:3FF6:552G94B:69F45B7:5913BBEQ\" when reporting this issue."
    }
  ]
}
```

> Nota: O GitHub recomenda a verificação de erros antes de usar dados em um ambiente de produção. No GraphQL, a falha não é total: partes das consultas do GraphQL podem ter êxito, enquanto outras falham.

