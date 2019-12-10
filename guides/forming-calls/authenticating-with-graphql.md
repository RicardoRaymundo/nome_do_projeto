# Formando chamadas com o GraphQL

[REFERENCIA](https://developer.github.com/v4/guides/forming-calls)

<!--TODO:: corrigir as traduções literais dos nomes de métodos -->

1. [Autenticando com GraphQL](#autenticando-com-graphql)
1. [O endpoint do GraphQL](#o-endpoint-do-graphql)
1. [Comunicação com o GraphQL](#comunicação-com-o-graphql)
1. [Sobre operações de consulta e mutação](#sobre-operações-de-consulta-e-mutação)
1. [Trabalhando com variáveis](#trabalhando-com-variáveis)
1. [Exemplo de query](#exemplo-de-query)
1. Exemplo de mutação
1. Leitura adicional

## Autenticando com GraphQL
Para se comunicar com o servidor GraphQL, você precisará de um token OAuth com os escopos corretos.

Siga as etapas em "[Criando um token de acesso pessoal para a linha de comando](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)" para criar um token. Os escopos necessários dependem do tipo de dados que você está tentando solicitar. Por exemplo, selecione os escopos do usuário para solicitar dados do usuário. Se você precisar acessar as informações do repositório, selecione os escopos de Repositório apropriados .

Para corresponder ao comportamento do [GraphQL Explorer](https://developer.github.com/v4/guides/using-the-explorer) , solicite os seguintes escopos:

    user
    public_repo
    repo
    repo_deployment
    repo:status
    read:repo_hook
    read:org
    read:public_key
    read:gpg_key
    
A API notifica se um recurso requer um escopo específico.

## O endpoint do GraphQL
A API REST v3 possui vários endpoints; a API do GraphQL v4 possui um único endpoint:

    https://api.github.com/graphql
    
O endpoint permanece constante, independentemente da operação que você executa.
    
## Comunicação com o GraphQL
Como as operações do GraphQL consistem em JSON com várias linhas, o GitHub recomenda o uso do [Explorer](https://developer.github.com/v4/guides/using-the-explorer) para fazer chamadas ao GraphQL. Você também pode usar cURL ou qualquer outra biblioteca que fala HTTP.

No REST, os [HTTP verbs](https://developer.github.com/v3/#http-verbs) determinam a operação executada. No GraphQL, você fornecerá um corpo codificado em JSON, esteja executando uma consulta ou uma mutação; portanto, o verbo HTTP é `POST`. A exceção é uma [introspection query](https://developer.github.com/v4/guides/intro-to-graphql#discovering-the-graphql-api), que é simples `GET` para o endpoint. Para obter mais informações sobre GraphQL versus REST, consulte " [Migrando do REST para o GraphQL](https://developer.github.com/v4/guides/migrating-from-rest) ".

Para consultar o GraphQL usando cURL, faça uma solicitação `POST` com uma carga útil JSON. A carga útil deve conter uma sequência chamada `query`:

```
curl -H "Authorization: bearer token" -X POST -d " \
 { \
   \"query\": \"query { viewer { login }}\" \
 } \
" https://api.github.com/graphql
```
> Nota : O valor String de "query" deve escapar dos caracteres de nova linha ou o esquema não o analisará corretamente. Para o corpo do POST, use aspas duplas externas e aspas duplas internas que escaparam.

## Sobre operações de consulta e mutação
Os dois tipos de operações permitidas na API GraphQL do GitHub são consultas e mutações. Comparando o GraphQL ao REST, as consultas operam como solicitações GET, enquanto as mutações operam como `POST`/ `PATCH`/ `DELETE`. O [nome da mutação](https://developer.github.com/v4/mutation/) determina qual modificação é executada.

Para obter informações sobre limitação de taxa, consulte "[Limitações de recursos do GraphQL](https://developer.github.com/v4/guides/resource-limitations/)".

Consultas e mutações compartilham formas semelhantes, com algumas diferenças importantes.

### Sobre consultas
As consultas do GraphQL retornam apenas os dados que você especificar. Para formar uma consulta, você deve especificar [campos nos campos](https://developer.github.com/v4/guides/intro-to-graphql#field) (também conhecidos como subcampos aninhados ) até retornar apenas [escalares](https://developer.github.com/v4/scalar/) .

As consultas são estruturadas da seguinte maneira:
```
query {
    objetos JSON para retornar
}
```

Para um exemplo do mundo real, consulte "[Consulta de exemplo](https://developer.github.com/v4/guides/forming-calls/#example-query)".

### Sobre mutações
Para formar uma mutação, você deve especificar três coisas:

1. Nome da mutação. O tipo de modificação que você deseja executar.
1. Objeto de entrada. Os dados que você deseja enviar para o servidor, compostos por campos de entrada. Passe como argumento para o nome da mutação.
1. Objeto de carga útil. Os dados que você deseja retornar do servidor, compostos por campos de retorno. Passe como o corpo do nome da mutação.

Mutações são estruturadas da seguinte maneira:

```
mutation {
  mutationName(input: {MutationNameInput!}) {
    MutationNamePayload
}
```

O objeto de entrada neste exemplo é `MutationNameInput` e o objeto de carga útil é `MutationNamePayload`.

Na referência de [mutações](https://developer.github.com/v4/mutation/), os campos de entrada listados são o que você passa como objeto de entrada. Os campos de retorno listados são o que você passa como objeto de carga útil.

Para um exemplo do mundo real, consulte "[Exemplo de mutação](https://developer.github.com/v4/guides/forming-calls/#example-mutation)".

## Trabalhando com variáveis
As [variáveis](https://graphql.github.io/learn/queries/#variables) podem tornar as consultas mais dinâmicas e poderosas, além de reduzir a complexidade ao passar objetos de entrada de mutação.

> Nota : Se você estiver usando o Explorer, certifique-se de inserir variáveis no [painel Variáveis Query](https://developer.github.com/v4/guides/using-the-explorer/#using-the-variable-pane) separado e não inclua a palavra `variables` antes do objeto JSON.

Aqui está um exemplo de consulta com uma única variável:

[Executar no Explorer](https://developer.github.com/v4/explorer/?variables=%20%7B%0A%20%20%20%22number_of_repos%22%3A%203%0A%7D&query=query%28%24number_of_repos%3AInt%21%29%20%7B%0A%20%20viewer%20%7B%0A%20%20%20%20name%0A%20%20%20%20%20repositories%28last%3A%20%24number_of_repos%29%20%7B%0A%20%20%20%20%20%20%20nodes%20%7B%0A%20%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%7D%0A%20%20%20%7D%0A%7D%0A)

```graphql
query($number_of_repos:Int!) {
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

Existem três etapas para usar variáveis:

1. Defina a variável fora da operação em um objeto `variables`:

    ```graphql
    variables {
       "number_of_repos": 3
    }
    ```
    O objeto deve ser JSON válido. Este exemplo mostra um tipo de variável simples `Int`, mas é possível definir tipos de variáveis ​​mais complexos, como objetos de entrada. Você também pode definir várias variáveis ​​aqui.

2. Passe a variável para a operação como argumento:

    ```graphql
    query($number_of_repos:Int!){
    ```
    
    O argumento é um par de valores-chave, em que a chave é o nome que começa com `$`(por exemplo, `$number_of_repos`) e o valor é o tipo (por exemplo, `Int`). Adicione a `!` para indicar se o tipo é necessário. Se você definiu várias variáveis, inclua-as aqui como vários argumentos.
    
3. Use a variável dentro da operação:
    ```
    repositories(last: $number_of_repos) {
    ```

    Neste exemplo, substituímos a variável pelo número de repositórios a serem recuperados. Especificamos um tipo na etapa 2 porque o GraphQL impõe uma forte tipagem.

Esse processo torna o argumento da consulta dinâmico. Agora podemos simplesmente alterar o valor no objeto `variables` e manter o restante da consulta igual.

O uso de variáveis ​​como argumentos permite atualizar dinamicamente os valores no objeto `variables` sem alterar a consulta.

## Exemplo de query

Vamos percorrer uma consulta mais complexa e colocar essas informações em contexto.

A consulta a seguir pesquisa o repositório `octocat/Hello-World`, localiza os 20 issues fechados mais recentes e retorna o título, o URL e os 5 primeiros rótulos de cada problema:

[Executar no Explorer](https://developer.github.com/v4/explorer/?variables=%7B%7D&query=query%20%7B%0A%20%20repository%28owner%3A%22octocat%22%2C%20name%3A%22Hello-World%22%29%20%7B%0A%20%20%20%20issues%28last%3A20%2C%20states%3ACLOSED%29%20%7B%0A%20%20%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20%20%20title%0A%20%20%20%20%20%20%20%20%20%20url%0A%20%20%20%20%20%20%20%20%20%20labels%28first%3A5%29%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20edges%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20node%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D)

```graphql
query {
  repository(owner:"octocat", name:"Hello-World") {
    issues(last:20, states:CLOSED) {
      edges {
        node {
          title
          url
          labels(first:5) {
            edges {
              node {
                name
              }
            }
          }
        }
      }
    }
  }
}
```

Olhando a composição linha por linha:

    * `query {`
        
        Porque queremos ler dados do servidor, não modificá-los, `query` é a operação raiz. (Se você não especificar uma operação, `query` será default.)
        