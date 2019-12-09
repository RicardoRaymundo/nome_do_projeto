# Formando chamadas com o GraphQL

a. [Autenticando com GraphQL]()

1. O terminal do GraphQL
1. Comunicação com o GraphQL
1. Sobre operações de consulta e mutação
1. Trabalhando com variáveis
1. Consulta de exemplo
1. Exemplo de mutação
1. Leitura adicional

## Autenticando com GraphQL
Para se comunicar com o servidor GraphQL, você precisará de um token OAuth com os escopos corretos.

Siga as etapas em " Criando um token de acesso pessoal para a linha de comando " para criar um token. Os escopos necessários dependem do tipo de dados que você está tentando solicitar. Por exemplo, selecione os escopos do usuário para solicitar dados do usuário. Se você precisar acessar as informações do repositório, selecione os escopos de Repositório apropriados .

Para corresponder ao comportamento do GraphQL Explorer , solicite os seguintes escopos:

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

## O terminal do GraphQL
A API REST v3 possui vários pontos de extremidade; a API do GraphQL v4 possui um único terminal:

    https://api.github.com/graphql
    
## Comunicação com o GraphQL
Como as operações do GraphQL consistem em JSON com várias linhas, o GitHub recomenda o uso do Explorer para fazer chamadas ao GraphQL. Você também pode usar cURL ou qualquer outra biblioteca que fala HTTP.

No REST, os verbos HTTP determinam a operação executada. No GraphQL, você fornecerá um corpo codificado em JSON, esteja executando uma consulta ou uma mutação; portanto, o verbo HTTP é `POST`. A exceção é uma consulta de introspecção , que é simples `GET` para o terminal. Para obter mais informações sobre GraphQL versus REST, consulte " Migrando do REST para o GraphQL ".

Para consultar o GraphQL usando cURL, faça uma `POST` solicitação com uma carga útil JSON. A carga útil deve conter uma sequência chamada `query`:

```
curl -H "Autorização: token do portador " -X POST -d "\
 {\
   \ "query \": \ "query {visualizador {login}} \" \
 } \
"https://api.github.com/graphql
```
    Nota : O valor da cadeia de caracteres "query"deve escapar dos caracteres de nova linha ou o esquema não o analisará corretamente. Para o POSTcorpo, use aspas duplas externas e aspas duplas internas que escaparam.

## Sobre operações de consulta e mutação
Os dois tipos de operações permitidas na API GraphQL do GitHub são consultas e mutações . Comparando o GraphQL ao REST, as consultas operam como GETsolicitações, enquanto as mutações operam como POST/ PATCH/ DELETE. O nome da mutação determina qual modificação é executada.

