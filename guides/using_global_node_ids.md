[REFERENCIA](https://developer.github.com/v4/guides/using-global-node-ids/)

# Usando IDs de Nó Globais
1. [Colocando IDs de Nó Global em Uso](#colocando-ids-de-nó-global-em-uso)
2. [Usando IDs de Nó Global em Migrações](#usando-ids-de-nó-global-em-migrações)

Você pode acessar a maioria dos objetos no GitHub (usuários, problemas, solicitações pull, etc.) usando a API REST v3 ou a API GraphQL v4. Com uma [atualização recente]() , é possível encontrar o ID do nó global de muitos objetos na API REST e usá-los nas operações do GraphQL.

> Nota: No REST, o campo ID do nó global é nomeado `node_id`. No GraphQL, é um `id` campo na `node` interface. Para uma atualização sobre o que "nó" significa no GraphQL, consulte " [Introdução ao GraphQL]() ".

## Colocando IDs de Nó Global em Uso
Você pode seguir três etapas para usar os IDs de nó global de maneira eficaz:

- Chame um terminal REST que retorne o objeto `node_id`.
- Encontre o tipo de objeto no GraphQL.
- Use o ID e o tipo para fazer uma pesquisa direta no nó no GraphQL.

Vamos dar um exemplo.

### 1. Chame um terminal REST que retorne o ID do nó de um objeto
Se você [solicitar o usuário autenticado]():

        curl -i -u nome de usuário: token https://api.github.com/user

você receberá uma resposta que inclui o `node_id` usuário autenticado:

```
Status: 200 OK
```
```graphql
{
  "login": "octocat",
  "id": 1,
  "avatar_url": "https://github.com/images/error/octocat_happy.gif",
  "gravatar_id": "",
  "url": "https://api.github.com/users/octocat",
  "html_url": "https://github.com/octocat",
  "followers_url": "https://api.github.com/users/octocat/followers",
  "following_url": "https://api.github.com/users/octocat/following{/other_user}",
  "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
  "organizations_url": "https://api.github.com/users/octocat/orgs",
  "repos_url": "https://api.github.com/users/octocat/repos",
  "events_url": "https://api.github.com/users/octocat/events{/privacy}",
  "received_events_url": "https://api.github.com/users/octocat/received_events",
  "type": "User",
  "site_admin": false,
  "name": "monalisa octocat",
  "company": "GitHub",
  "blog": "https://github.com/blog",
  "location": "San Francisco",
  "email": "octocat@github.com",
  "hireable": false,
  "bio": "There once was...",
  "public_repos": 2,
  "public_gists": 1,
  "followers": 20,
  "following": 0,
  "created_at": "2008-01-14T04:33:35Z",
  "updated_at": "2008-01-14T04:33:35Z",
  "private_gists": 81,
  "total_private_repos": 100,
  "owned_private_repos": 100,
  "disk_usage": 10000,
  "collaborators": 8,
  "two_factor_authentication": true,
  "plan": {
    "name": "Medium",
    "space": 400,
    "private_repos": 20,
    "collaborators": 0
  },
  "node_id": "MDQ6VXNlcjU4MzIzMQ=="
}
```

### 2. Encontre o tipo de objeto no GraphQL
Neste exemplo, o `node_id` valor é `MDQ6VXNlcjU4MzIzMQ==`. Você pode usar esse valor para consultar o mesmo objeto no GraphQL.

Você precisará conhecer primeiro o tipo do objeto . Você pode verificar o tipo com uma simples consulta GraphQL:

[Executar no Explorer]()

```graphql
query {
  node(id:"MDQ6VXNlcjU4MzIzMQ==") {
     __typename
  }
}
```

Esse tipo de consulta - ou seja, encontrar o nó por ID - é conhecido como "pesquisa direta do nó".

Quando você executa essa consulta, verá que `__typename` sim [`User`]() .

### 3. Faça uma consulta direta ao nó no GraphQL
Depois de confirmar o tipo, você pode usar um [fragmento embutido]() para acessar o objeto por seu ID e retornar dados adicionais. Neste exemplo, definimos os campos `User` que gostaríamos de consultar:

[Executar no Explorer]()

```graphql
query {
  node(id:"MDQ6VXNlcjU4MzIzMQ==") {
   ... on User {
      name
      login
    }
  }
}
```

## Esse tipo de consulta é a abordagem padrão para procurar um objeto por seu ID de nó global.

Usando IDs de Nó Global em Migrações
Ao criar integrações que usam a API REST v3 ou a API GraphQL v4, é uma boa prática manter o ID do nó global para que você possa facilmente referenciar objetos nas versões da API. Para obter mais informações sobre como lidar com a transição entre o REST e o GraphQL, consulte " [Migrando do REST para o GraphQL]() ".

