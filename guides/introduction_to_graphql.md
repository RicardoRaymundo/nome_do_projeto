## GraphQL API v4

[REFERENCIA](https://developer.github.com/v4/guides/intro-to-graphql/)

# Introduction to GraphQL
1. Terminologia do GraphQL
2. Descobrindo a API GraphQL

## Terminologia do GraphQL
A API GitHub GraphQL v4 representa uma mudança arquitetônica e conceitual da API REST GitHub v3. Você provavelmente encontrará alguma nova terminologia nos [documentos de referência]() da API do GraphQL v4 .

### Schema
Um esquema define um sistema de tipos da API GraphQL. Ele descreve o conjunto completo de dados possíveis (objetos, campos, relacionamentos, tudo) que um cliente pode acessar. As chamadas do cliente são [validadas]() e [executadas]() no esquema. Um cliente pode encontrar informações sobre o esquema por [introspecção]() . Um esquema reside no servidor da API GraphQL. Para obter mais informações, consulte "[Descobrindo a API do GraphQL]()".

### Campo
Um campo é uma unidade de dados que você pode recuperar de um objeto. Como dizem os [documentos oficiais do GraphQL](): "A linguagem de consulta do GraphQL é basicamente sobre a seleção de campos nos objetos".

A [especificação oficial]() também diz sobre os campos:

> Todas as operações do GraphQL devem especificar suas seleções nos campos que retornam valores escalares para garantir uma resposta de forma inequívoca.

Isso significa que, se você tentar retornar um campo que não é escalar, a validação do esquema gerará um erro. Você deve adicionar subcampos aninhados até que todos os campos retornem escalares.

### Argumento
Um argumento é um conjunto de pares de valores-chave anexados a um campo específico. Alguns campos requerem um argumento. [Mutações]() requerem um objeto de entrada como argumento.

### Implementação
Um esquema do GraphQL pode usar o termo implementa para definir como um objeto é herdado de uma [interface]().

Aqui está um exemplo artificial de um esquema que define interface `X` e objeto `Y`:

```graphql
interface X {
  some_field: String!
  other_field: String!
}

type Y implements X {
  some_field: String!
  other_field: String!
  new_field: String!
}
```

Isso significa que o objeto `Y` requer os mesmos campos / argumentos / tipos de retorno que a interface `X`, enquanto adiciona novos campos específicos ao objeto `Y`. (Os `!` meios que o campo é obrigatório.)

Nos documentos de referência, você encontrará que:

- Cada [objeto]() lista as interfaces das quais herda em **Implementações**.

- Cada [interface]() lista os objetos que herdam dele em **Implementações**.

### Conexão
As conexões permitem consultar objetos relacionados como parte da mesma chamada. Com as conexões, você pode usar uma única chamada GraphQL na qual precisaria usar várias chamadas para uma API REST. Para obter mais informações, consulte " [Migrando do REST para o GraphQL]() ".

É útil imaginar um gráfico: pontos conectados por linhas. Os pontos são nós, as linhas são arestas. Uma conexão define um relacionamento entre nós.

### Beira
Arestas representam conexões entre nós. Ao consultar uma conexão, você percorre as bordas para chegar aos nós. Todo `edges` campo tem um `node` campo e um `cursor` campo. Os cursores são usados ​​para `paginação`.

### Nó
Nó é um termo genérico para um objeto. Você pode procurar diretamente um nó ou acessar nós relacionados por meio de uma conexão. Se você especificar um `node` que não retorne um [escalar]() , deverá incluir subcampos até que todos os campos retornem escalares. Para obter informações sobre como acessar IDs de nó por meio da API REST v3 e usá-los em consultas GraphQL, consulte " [Usando IDs de Nó Global]() ".

## Descobrindo a API GraphQL
O GraphQL é [introspectivo]() . Isso significa que você pode consultar um esquema do GraphQL para obter detalhes sobre si mesmo.

- Consulta `__schema` para listar todos os tipos definidos no esquema e obter detalhes sobre cada um:

[Executar no Explorer]()

```graphql
query {
  __schema {
    types {
      name
      kind
      description
      fields {
        name
      }
    }
  }
}
```

- Consulta `__type` para obter detalhes sobre qualquer tipo:

[Executar no Explorer]()

```graphql
query {
  __type(name: "Repository") {
    name
    kind
    description
    fields {
      name
    }
  }
}
```

- Você também pode executar uma *consulta de introspecção* do esquema por meio de uma GETsolicitação:

        curl -H "Autorização: token do portador " https://api.github.com/graphql

    Os resultados estão em JSON, portanto, recomendamos imprimi-los para facilitar a leitura e a pesquisa. Você pode usar uma ferramenta de linha de comando como [jq]() ou canalizar os resultados `python -m json.tool` para esse fim.

    Como alternativa, você pode passar o `idl` tipo de mídia para retornar os resultados no formato IDL, que é uma versão condensada do esquema:

        curl -H "Autorização: token do portador " -H "Aceite: application / vnd.github.v4.idl" \
        https://api.github.com/graphql
> Nota : A consulta de introspecção é provavelmente a única `GET` solicitação que você executará no GraphQL. Se você está passando um corpo, o método de solicitação do GraphQL é `POST`, seja uma consulta ou uma mutação.

Para obter mais informações sobre como executar consultas, consulte " [Formando chamadas com o GraphQL]() ".