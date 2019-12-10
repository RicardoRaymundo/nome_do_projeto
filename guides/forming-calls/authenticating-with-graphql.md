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

- `query {`
    
    Porque queremos ler dados do servidor, não modificá-los, `query` é a operação raiz. (Se você não especificar uma operação, `query` será default.)
    
- `repository(owner:"octocat", name:"Hello-World") {`

    Para iniciar a consulta, queremos encontrar um [`repository`]() objeto. A validação do esquema indica que este objeto requer um `owner` e um name argumento.

- `issues(last:20, states:CLOSED) {`

    Para explicar todos os problemas no repositório, chamamos o `issues` objeto ( Poderíamos consultar um único `issue` em um `repository`, mas isso exigiria que soubéssemos o número do problema que queremos retornar e forneça como argumento.)

Alguns detalhes sobre o `issues` objeto:

    - Os [documentos]() dizem-nos este objeto tem o tipo `IssueConnection`.
    - A validação do esquema indica que este objeto requer um `last` ou `first` número de resultados como argumento, portanto fornecemos `20`.
    - Os [documentos]() também nos dizem que esse objeto aceita um `states` argumento, que é uma ` [IssueState]() ` enumeração que aceita OPENou CLOSEDvaloriza. Para encontrar apenas problemas fechados, atribuímos à stateschave o valor de CLOSED.

- `edges {`

Sabemos que issuesé uma conexão porque tem o IssueConnectiontipo Para recuperar dados sobre problemas individuais, precisamos acessar o nó via edges.

node {

Aqui, recuperamos o nó no final da borda. Os IssueConnectiondocumentos indicam que o nó no final do IssueConnectiontipo é um Issueobjeto.

Agora que sabemos que estamos recuperando um Issueobjeto, podemos examinar os documentos e especificar os campos que queremos retornar:

title
url
labels(first:5) {
  edges {
    node {
      name
    }
  }
}
Aqui nós especificar os title, urle labelscampos do Issueobjeto.

O labelscampo tem o tipo LabelConnection. Assim como o issuesobjeto, por labelsser uma conexão, devemos percorrer suas bordas para um nó conectado: o labelobjeto. No nó, podemos especificar os labelcampos do objeto que queremos retornar, neste caso name,.

Você pode perceber que a execução dessa consulta no Hello-Worldrepositório público do Octocat não retornará muitos rótulos. Tente executá-lo em um de seus próprios repositórios que usa rótulos e você provavelmente verá uma diferença.

Exemplo de mutação
As mutações geralmente exigem informações que você só pode descobrir executando uma consulta primeiro. Este exemplo mostra duas operações:

Uma consulta para obter um ID de problema.
Uma mutação para adicionar uma reação emoji ao problema.
Executar no Explorer

query FindIssueID {
  repository(owner:"octocat", name:"Hello-World") {
    issue(number:349) {
      id
    }
  }
}

mutation AddReactionToIssue {
  addReaction(input:{subjectId:"MDU6SXNzdWUyMzEzOTE1NTE=",content:HOORAY}) {
    reaction {
      content
    }
    subject {
      id
    }
  }
}
Embora você possa incluir uma consulta e uma mutação na mesma janela do Explorer, se você der nomes ( FindIssueIDe AddReactionToIssueneste exemplo), as operações serão executadas como chamadas separadas para o terminal do GraphQL. Não é possível realizar uma consulta ao mesmo tempo que uma mutação ou vice-versa.

Vamos percorrer o exemplo. A tarefa parece simples: adicione uma reação emoji a um problema.

Então, como sabemos começar com uma consulta? Ainda não.

Como queremos modificar os dados no servidor (anexar um emoji a um problema), começamos pesquisando no esquema uma mutação útil. Os documentos de referência mostram a addReactionmutação, com esta descrição: Adds a reaction to a subject.Perfeito!

Os documentos para a mutação listam três campos de entrada:

clientMutationId( String)
subjectId( ID!)
content( ReactionContent!)
Os !s indicam isso subjectIde contentsão campos obrigatórios. Um requisito contentfaz sentido: queremos adicionar uma reação, portanto, precisamos especificar qual emoji usar.

Mas por que é subjectIdnecessário? É porque subjectIdé a única maneira de identificar qual problema em qual repositório reagir.

É por isso que começamos este exemplo com uma consulta: para obter o ID.

Vamos examinar a linha de consulta por linha:

query FindIssueID {

Aqui, estamos realizando uma consulta e o nomeamos FindIssueID. Observe que nomear uma consulta é opcional; damos um nome aqui para que possamos incluí-lo na mesma janela do Explorer que a mutação.

repository(owner:"octocat", name:"Hello-World") {

Especificamos o repositório consultando o repositoryobjeto e passando ownere nameargumentos.

issue(number:349) {

Especificamos o problema ao qual reagir consultando o issueobjeto e passando um numberargumento.

id

É aqui que recuperamos o idde https://github.com/octocat/Hello-World/issues/349para passar como o subjectId.

Quando executamos a consulta, obtemos o id:MDU6SXNzdWUyMzEzOTE1NTE=

Nota : O idretorno na consulta é o valor que passaremos subjectIDna mutação. Nem a documentação nem a introspecção de esquema indicarão esse relacionamento; você precisará entender os conceitos por trás dos nomes para descobrir isso.

Com o ID conhecido, podemos prosseguir com a mutação:

mutation AddReactionToIssue {

Aqui estamos realizando uma mutação, e o nomeamos AddReactionToIssue. Como nas consultas, nomear uma mutação é opcional; fornecemos um nome aqui para que possamos incluí-lo na mesma janela do Explorer que a consulta.

addReaction(input:{subjectId:"MDU6SXNzdWUyMzEzOTE1NTE=",content:HOORAY}) {

Vamos examinar esta linha:

addReaction é o nome da mutação.
inputé a chave de argumento necessária. Isso sempre será inputpara uma mutação.
{subjectId:"MDU6SXNzdWUyMzEzOTE1NTE=",content:HOORAY}é o valor do argumento necessário. Este sempre será um objeto de entrada (portanto, as chaves) composto de campos de entrada ( subjectIde contentneste caso) para uma mutação.
Como sabemos qual valor usar para o conteúdo? Os addReactiondocumentos nos dizem que o contentcampo tem o tipo ReactionContent, que é um enum, porque apenas certas reações emoji são suportadas nos problemas do GitHub. Estes são os valores permitidos para reações (observe que alguns valores diferem dos nomes de emoji correspondentes):

conteúdo	emoji
+1	: +1:
-1	: -1:
laugh	:sorrir:
confused	:confuso:
heart	:coração:
hooray	: tada:
rocket	:foguete:
eyes	: olhos:
O restante da chamada é composto pelo objeto de carga útil. É aqui que especificamos os dados que queremos que o servidor retorne após a mutação. Essas linhas vêm dos addReactiondocumentos , cujos três campos de retorno possíveis:

clientMutationId( String)
reaction( Reaction!)
subject( Reactable!)
Neste exemplo, retornamos os dois campos obrigatórios ( reactione subject), ambos com subcampos necessários (respectivamente contente id).

Quando executamos a mutação, esta é a resposta:

{
  "data": {
    "addReaction": {
      "reaction": {
        "content": "HOORAY"
      },
      "subject": {
        "id": "MDU6SXNzdWUyMTc5NTQ0OTc="
      }
    }
  }
}
É isso aí! Confira sua reação ao problema , passando o mouse sobre : tada:para encontrar seu nome de usuário.

Uma observação final: quando você passa vários campos em um objeto de entrada, a sintaxe pode ficar pesada. Mover os campos para uma variável pode ajudar. Veja como você pode reescrever a mutação original usando uma variável:

Executar no Explorer

mutation($myVar:AddReactionInput!) {
  addReaction(input:$myVar) {
    reaction {
      content
    }
    subject {
      id
    }
  }
}
variables {
  "myVar": {
    "subjectId":"MDU6SXNzdWUyMTc5NTQ0OTc=",
    "content":"HOORAY"
  }
}
Você pode perceber que o contentvalor do campo no exemplo anterior (onde é usado diretamente na mutação) não possui aspas HOORAY, mas possui aspas quando usado na variável. Há uma razão para isso:

Quando você usa contentdiretamente na mutação, o esquema espera que o valor seja do tipo ReactionContent, que é uma enumeração , não uma sequência. A validação do esquema gerará um erro se você adicionar aspas ao redor do valor da enumeração, pois as aspas são reservadas para cadeias de caracteres.
Quando você usa contentem uma variável, a seção de variáveis ​​deve ser JSON válida, portanto, as aspas são necessárias. A validação do esquema interpreta corretamente o ReactionContenttipo quando a variável é passada para a mutação durante a execução.
Para obter mais informações sobre a diferença entre enumerações e strings, consulte a especificação oficial do GraphQL .

Leitura adicional
Há um monte mais você pode fazer quando formando as chamadas GraphQL. Aqui estão alguns lugares para procurar a seguir:

Paginação
Fragmentos
Fragmentos em linha
Diretivas
    