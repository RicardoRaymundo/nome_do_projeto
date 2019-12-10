[REFERENCIA](https://developer.github.com/v4/guides/managing-enterprise-accounts/)

# Gerenciando contas corporativas
1. [Sobre o gerenciamento de contas corporativas com o GraphQL](#sobre-o-gerenciamento-de-contas-corporativas-com-o-graphql)
1. [Introdução ao uso do GraphQL para contas corporativas](#introdução-ao-uso-do-graphql-para-contas-corporativas)
1. [Uma consulta de exemplo usando a API de contas corporativas](#uma-consulta-de-exemplo-usando-a-api-de-contas-corporativas)
1. [Consultar cada organização separadamente](#consultar-cada-organização-separadamente)
1. [Campos e tipos de GraphQL para a API de contas corporativas](#campos-e-tipos-de-graphql-para-a-api-de-contas-corporativas)

## Sobre o gerenciamento de contas corporativas com o GraphQL

Para ajudar a monitorar e fazer alterações em suas organizações e manter a conformidade, você pode usar a API de Contas Corporativas e a API de Log de Auditoria, disponíveis apenas como APIs do GraphQL.

Os pontos de extremidade da conta corporativa funcionam no GitHub Enterprise Cloud e no GitHub Enterprise Server.

O GraphQL permite solicitar e retornar apenas os dados que você especificar. Por exemplo, você pode criar uma consulta GraphQL, ou solicitar informações, para ver todos os novos membros da organização adicionados à sua organização. Ou você pode fazer uma mutação ou alteração para convidar um administrador para sua conta corporativa.

Com a API do log de auditoria, você pode monitorar quando alguém:

- Acessa as configurações da sua organização ou repositório.
- Muda as permissões.
- Adiciona ou remove usuários em uma organização, repositório ou equipe.
- Promove usuários para administrar.
- Altera as permissões de um aplicativo GitHub.

A API de log de auditoria permite manter cópias de seus dados de log de auditoria. Para consultas feitas com a API de log de auditoria, a resposta do GraphQL pode incluir dados de até 90 a 120 dias. Para obter uma lista dos campos disponíveis com a API do Log de auditoria, consulte a " [interface AuditEntry]() ".

Com a API de contas corporativas, você pode:

- Liste e revise todas as organizações e repositórios que pertencem à sua conta corporativa.
- Alterar as configurações da conta corporativa.
- Defina políticas para configurações na sua conta corporativa e em suas organizações.
- Convide administradores para sua conta corporativa.
- Crie novas organizações em sua conta corporativa.

Para obter uma lista dos campos disponíveis na API de contas corporativas, consulte "[Campos e tipos de GraphQL para a API da conta corporativa]()".

## Introdução ao uso do GraphQL para contas corporativas

Siga estas etapas para começar a usar o GraphQL para gerenciar suas contas corporativas:

- Autenticando com um token de acesso pessoal
- Escolhendo um cliente GraphQL ou usando o GraphQL Explorer
- Configurando o Insomnia para usar a API GraphQL

Para alguns exemplos de consultas, consulte " [Um exemplo de consulta usando a API de Contas Corporativas]()".

### 1. Autentique com seu token de acesso pessoal  
    
  1. Para se autenticar com o GraphQL, você precisa gerar um PAT (token de acesso pessoal) a partir das configurações do desenvolvedor. Para obter mais informações, consulte " Criando um token de acesso pessoal para a linha de comando " na documentação de Ajuda do GitHub.
  
  2. Conceda permissões de administrador e controle total ao seu token de acesso pessoal para áreas do GHES que você deseja acessar. Para obter permissão total para repositórios privados, organizações, equipes, dados do usuário e acesso a dados corporativos de faturamento e perfil, recomendamos que você selecione estes escopos para seu token de acesso pessoal:
    - `repo`
    - `admin:org`
    - `user`
    - `admin:enterprise`
    Os escopos específicos da conta corporativa são:
    - `admin:enterprise:` Dá controle total às empresas (inclui `manage_billing:enterprise` e `read:enterprise`)
    - `manage_billing:enterprise:` Leia e grave dados de cobrança da empresa.
    - `read:enterprise:` Leia os dados do perfil da empresa.
  
  3. Copie seu token de acesso pessoal e mantenha-o em um local seguro até adicioná-lo ao seu cliente GraphQL.

### 2. Escolha um cliente GraphQL

Recomendamos que você use o GraphiQL ou outro cliente independente do GraphQL que permita configurar o URL base.

Você também pode considerar usar estes clientes GraphQL:

- [Insônia]()
- [GraphiQL]()
- [Carteiro]()

Os próximos passos usarão o Insomnia.

3. Configurando o Insomnia para usar a API do GitHub GraphQL com contas corporativas

    1. Adicione o URL e o `POST` método base ao seu cliente GraphQL. Ao usar o GraphQL para solicitar informações (consultas), alterar informações (mutações) ou transferir dados usando a API do GitHub, o método HTTP padrão é `POST` e o URL base segue esta sintaxe:

        - Para sua instância corporativa: https://<HOST>/api/graphql
        - Para o GitHub Enterprise Cloud: https://api.github.com/graphql
    2. Para autenticar, abra o menu de opções de autenticação e selecione **Token do portador**. Em seguida, adicione seu token de acesso pessoal que você copiou anteriormente.


    3. Incluir informações do cabeçalho.

        - Adicione `Content-Type` como cabeçalho e `application/json` como valor.

Agora você está pronto para começar a fazer consultas.

## Uma consulta de exemplo usando a API de contas corporativas

Esta consulta do GraphQL solicita o número total de `public` repositórios em cada uma das organizações do seu dispositivo usando a API de contas corporativas. Para personalizar essa consulta, substitua `<enterprise-account-name>` pela lesma da instância da sua empresa.

```
query publicRepositoriesByOrganization($slug: String!) {
  enterprise(slug: $slug) {
    ...enterpriseFragment
  }
}

fragment enterpriseFragment on Enterprise {
  ... on Enterprise{
    name
    organizations(first: 100){
      nodes{
        name
        ... on Organization{
          name
          repositories(privacy: PUBLIC){
            totalCount
          }
        }
      }
    }
  }
}
# Passing our Enterprise Account as a variable
variables {
  "slug": "<enterprise-account-name>"
}
```

O próximo exemplo de consulta do GraphQL mostra como é difícil recuperar o número de `public` repositórios em cada organização sem usar a API da conta corporativa. Observe que a API GraphQL Enterprise Accounts simplificou essa tarefa para empresas, pois você só precisa personalizar uma única variável. Para personalizar esta consulta, substitua `<name-of-organization-one>` e `<name-of-organization-one>` etc. pelos nomes da organização em sua instância.

```
# Each organization is queried separately
{
  organizationOneAlias: organization(login: "nameOfOrganizationOne") {
    # How to use a fragment
    ...repositories
  }
  organizationTwoAlias: organization(login: "nameOfOrganizationTwo") {
    ...repositories
  }
  # organizationThreeAlias ... and so on up-to lets say 100
}

## How to define a fragment
fragment repositories on Organization {
  name
  repositories(privacy: PUBLIC){
    totalCount
  }
}
```

## Consultar cada organização separadamente

```
query publicRepositoriesByOrganization {
  organizationOneAlias: organization(login: "<name-of-organization-one>") {
    # How to use a fragment
    ...repositories
  }
  organizationTwoAlias: organization(login: "<name-of-organization-two>") {
    ...repositories
  }
  # organizationThreeAlias ... and so on up-to lets say 100
}
# How to define a fragment
fragment repositories on Organization {
  name
  repositories(privacy: PUBLIC){
    totalCount
  }
}
```

Esta consulta do GraphQL solicita as últimas 5 entradas de log para uma organização corporativa. Para personalizar esta consulta, substitua <org-name>e <user-name>.

```
{
  organization(login: "<org-name>") {
    auditLog(last: 5, query: "actor:<user-name>") {
      edges {
        node {
          ... on AuditEntry {
# Get Audit Log Entry by 'Action'
            action
            actorLogin
            createdAt
# User 'Action' was performed on
           user{
              name
                email
            }
          }
        }
      }
    }
  }
}
```

Para obter mais informações sobre como iniciar o GraphQL, consulte "[Introdução ao GraphQL]()" e ["Como fazer chamadas com o GraphQL]() ".

## Campos e tipos de GraphQL para a API de contas corporativas

Aqui está uma visão geral das novas consultas, mutações e tipos definidos por esquema disponíveis para uso com a API de contas corporativas.

Para obter mais detalhes sobre as novas consultas, mutações e tipos definidos por esquema disponíveis para uso com a API de Contas Corporativas, consulte o sdiebar com definições detalhadas do GraphQL em qualquer [página de referência do GraphQL]().

Você pode acessar os documentos de referência no GraphQL Explorer no GitHub. Para mais informações, consulte "[Usando o explorer]()". Para outras informações, como detalhes de autenticação e limite de taxa, consulte os [guias]() .