[REFERENCIA](https://developer.github.com/v4/guides/migrating-from-rest/)

# Migrando do REST para o GraphQL
1. [Diferenças na lógica da API](#diferenças-na-lógica-da-api)
2. [Exemplo: obtendo os dados necessários e nada mais](#exemplo:-obtendo-os-dados-necessários-e-nada-mais)
3. [Exemplo: aninhando](#exemplo:-aninhando)
4. [Exemplo: digitação forte](#exemplo:-digitação-forte)

## Diferenças na lógica da API
A migração do REST para o GraphQL representa uma mudança significativa na lógica da API. As diferenças entre o REST como um estilo e o GraphQL como uma especificação tornam difícil - e muitas vezes indesejável - substituir as chamadas da API REST pelas consultas da API GraphQL de uma a uma. Incluímos exemplos específicos de migração abaixo.

Para migrar seu código da `API REST v3` para a API GraphQL v4:

- Revise as [especificações do GraphQL]()
- Analise o [esquema GraphQL]() do GitHub
- Considere como qualquer código existente que você interage atualmente com a API REST do GitHub v3
- Use [IDs de nó global]() para fazer referência a objetos entre versões da API

As vantagens significativas do GraphQL incluem:

- [Obtendo os dados necessários e nada mais]()
- [Campos aninhados]()
- [Digitação forte]()

Aqui estão exemplos de cada um.

## Exemplo: obtendo os dados necessários e nada mais
Uma única chamada da API REST v3 recupera uma lista dos membros da sua organização:

        curl -v https://api.github.com/orgs/:org/members

A carga útil do REST contém dados excessivos se seu objetivo é recuperar apenas nomes de membros e links para avatares. No entanto, uma consulta GraphQL retorna apenas o que você especificar:

[Executar no Explorer]()

```graphql
query {
    organization(login:"github") {
    members(first: 100) {
      edges {
        node {
          name
          avatarUrl
        }
      }
    }
  }
}
```

Considere outro exemplo: recuperando uma lista de solicitações pull e verificando se cada uma é mesclável. Uma chamada para a API REST v3 recupera uma lista de solicitações pull e suas [representações de resumo]():

        curl -v https://api.github.com/repos/:owner/:repo/pulls

Determinar se uma solicitação pull é mesclável requer recuperar cada solicitação pull individualmente para sua [representação detalhada]() (uma grande carga útil) e verificar se seu `mergeable` atributo é verdadeiro ou falso:

        curl -v https://api.github.com/repos/:owner/:repo/pulls/:number

Com o GraphQL, você pode recuperar apenas os atributos `number` e `mergeable` para cada solicitação pull:

[Executar no Explorer]()

```graphql
query {
    repository(owner:"octocat", name:"Hello-World") {
    pullRequests(last: 10) {
      edges {
        node {
          number
          mergeable
        }
      }
    }
  }
}
```

## Exemplo: aninhando
A consulta com campos aninhados permite substituir várias chamadas REST por menos consultas GraphQL. Por exemplo, a recuperação de uma solicitação pull com seus commit, comentários sem revisão e revisões usando a **API REST v3** requer quatro chamadas separadas:

    curl -v https://api.github.com/repos/:owner/:repo/pulls/:number
    curl -v https://api.github.com/repos/:owner/:repo/pulls/:number/commits
    curl -v https://api.github.com/repos/:owner/:repo/issues/:number/comments
    curl -v https://api.github.com/repos/:owner/:repo/pulls/:number/reviews

Usando a **API GraphQL v4** , é possível recuperar os dados com uma única consulta usando campos aninhados:

[Executar no Explorer]()

```graphql
{
  repository(owner: "octocat", name: "Hello-World") {
    pullRequest(number: 1) {
      commits(first: 10) {
        edges {
          node {
            commit {
              oid
              message
            }
          }
        }
      }
      comments(first: 10) {
        edges {
          node {
            body
            author {
              login
            }
          }
        }
      }
      reviews(first: 10) {
        edges {
          node {
            state
          }
        }
      }
    }
  }
}
```

Você também pode estender o poder dessa consulta [substituindo uma variável]() pelo número da solicitação de recebimento.

## Exemplo: digitação forte
Os esquemas do GraphQL são fortemente tipados, tornando a manipulação de dados mais segura.

Considere um exemplo de adição de um comentário a um problema ou solicitação pull usando uma [mutação]() GraphQL e especificando por engano um número inteiro em vez de uma sequência para o valor de [`clientMutationId`]() :

[Executar no Explorer]()

```graphql
mutation {
  addComment(input:{clientMutationId: 1234, subjectId: "MDA6SXNzdWUyMjcyMDA2MTT=", body: "Looks good to me!"}) {
    clientMutationId
    commentEdge {
      node {
        body
        repository {
          id
          name
          nameWithOwner
        }
        issue {
          number
        }
      }
    }
  }
}
```

A execução desta consulta retorna erros especificando os tipos esperados para a operação:

```graphql
{
  "data": null,
  "errors": [
    {
      "message": "Argument 'input' on Field 'addComment' has an invalid value. Expected type 'AddCommentInput!'.",
      "locations": [
        {
          "line": 3,
          "column": 3
        }
      ]
    },
    {
      "message": "Argument 'clientMutationId' on InputObject 'AddCommentInput' has an invalid value. Expected type 'String'.",
      "locations": [
        {
          "line": 3,
          "column": 20
        }
      ]
    }
  ]
}
```

O agrupamento `1234` entre aspas transforma o valor de um número inteiro em uma sequência, o tipo esperado:

[Executar no Explorer]()

```graphql
mutation {
  addComment(input:{clientMutationId: "1234", subjectId: "MDA6SXNzdWUyMjcyMDA2MTT=", body: "Looks good to me!"}) {
    clientMutationId
    commentEdge {
      node {
        body
        repository {
          id
          name
          nameWithOwner
        }
        issue {
          number
        }
      }
    }
  }
}
```

