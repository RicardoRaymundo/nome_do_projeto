[REFERENCIA](https://developer.github.com/v4/query/)

# Inquerir
Todo esquema do GraphQL tem um tipo de raiz para consultas e mutações. O [tipo de consulta]() define operações do GraphQL que recuperam dados do servidor.

Para mais informações, consulte "[Sobre consultas]()".

## Conexões
**marketplaceListings** ([MarketplaceListingConnection!]())
Procurar listagens de mercado

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `adminId`           | [`ID`]()      |Selecione listagens que podem ser administradas pelo usuário especificado.          |
| `after`          | [`String`]()     |Retorna os elementos na lista que vêm após o cursor especificado.           |
| `allStates`          | [`Boolean`]()     |Selecione listagens visíveis para o espectador, mesmo que não sejam aprovadas. Se omitido ou falso, somente as listagens aprovadas serão retornadas.           |
| `before`          | [`String`]()     |Retorna os elementos na lista que vêm antes do cursor especificado.           |
| `categorySlug`          | [`	String	`]()     |Selecione apenas listagens com a categoria especificada.          |
| `first`          | [`Int`]()     |Retorna os primeiros n elementos da lista.           |
| `last`          | [`Int`]()     |Retorna os últimos n elementos da lista.           |
| `organizationId`  | [`ID`]()     |Selecione listagens de produtos pertencentes à organização especificada.           |
| `primaryCategoryOnly`         | [`Boolean`]()     |Selecione apenas listagens onde a categoria principal corresponde à lesma de categoria fornecida. O valor padrão é **false**.          |
| `slugs`          | [`String`]()     |Selecione as listagens com essas lesmas, se estiverem visíveis para o visualizador.           |
| `useTopicAliases`          | [`Boolean`]()     |Verifique também os aliases de tópico para a categoria slug           |
| `viewerCanAdmin`          | [`Boolean`]()     |Selecione listagens às quais o usuário tem acesso de administrador. Se omitido, as listagens visíveis ao visualizador são retornadas.           |
| `withFreeTrialsOnly`          | [`Boolean`]()     |Selecione apenas listagens que oferecem uma avaliação gratuita. O valor padrão é `false`.           |

**search** ( [SearchResultItemConnection!]())
Faça uma pesquisa entre os recursos.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `after`           | [`String`]()      |Retorna os elementos na lista que vêm após o cursor especificado.         |
| `before`           | [`String`]()      |Retorna os elementos na lista que vêm antes do cursor especificado.          |
| `first`           | [`Int`]()      |Retorna os primeiros n elementos da lista.          |
| `last`           | [`Int`]()      |Retorna os últimos n elementos da lista.         |
| `query`           | [`String!`]()      |A cadeia de pesquisa a procurar.          |
| `type`           | [`SearchType!`]()      |Os tipos de itens de pesquisa a serem pesquisados.          |

**securityAdvisories** ([SecurityAdvisoryConnection!]())
Avisos de segurança do GitHub

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `after`           | [`String`]()      |Retorna os elementos na lista que vêm após o cursor especificado.          |
| `before`           | [`String`]()      |Retorna os elementos na lista que vêm antes do cursor especificado.         |
| `first`           | [`Int`]()      |Retorna os primeiros n elementos da lista.          |
| `identifier`           | [`SecurityAdvisoryIdentifierFilter`]()      |Filtre os avisos por identificador, por exemplo, GHSA ou CVE.          |
| `last`           | [`Int`]()      |Retorna os últimos n elementos da lista.          |
| `orderBy`           | [`SecurityAdvisoryOrder`]()      |Opções de pedido para os tópicos retornados. O valor padrão é {"field"=>"UPDATED_AT", "direction"=>"DESC"}.         |
| `publishedSince`           | [`DateTime`]()      |Filtre os avisos aos publicados desde uma época passada.          |
| `updatedSince`           | [`DateTime`]()      |Filtre os avisos aos atualizados desde um tempo passado.          |

**securityVulnerabilities** ([SecurityVulnerabilityConnection!]())
Vulnerabilidades de software documentadas pelo GitHub Security Advisories

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `after`           | [`String`]()      |Retorna os elementos na lista que vêm após o cursor especificado.          |
| `before`           | [`String`]()      |Retorna os elementos na lista que vêm antes do cursor especificado.         |
| `ecosystem`           | [`SecurityAdvisoryEcosystem`]()      |Um ecossistema para filtrar vulnerabilidades.          |
| `first`           | [`Int`]()      |Retorna os primeiros n elementos da lista.          |
| `last`           | [`Int`]()      |Retorna os últimos n elementos da lista.          |
| `orderBy`           | [`SecurityVulnerabilityOrder`]()      |Opções de pedido para os tópicos retornados. O valor padrão é {"field"=>"UPDATED_AT", "direction"=>"DESC"}.          |
| `package`           | [`String`]()      |Um nome de pacote pelo qual filtrar vulnerabilidades.          |
| `severities`           | [`[SecurityAdvisorySeverity!]`]()      |Uma lista de severidades para filtrar as vulnerabilidades.          |


## Campos
**codeOfConduct** ([CodeOfConduct]())
Procure um código de conduta por sua chave

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `key`           | [`String!`]()      |A chave do código de conduta          |

**codesOfConduct** ( [CodeOfConduct])
Procure um código de conduta por sua chave

**enterprise** ([Enterprise]())
Procure uma empresa por slug de URL.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `invitationToken`           | [`String`]()      |O token de convite da empresa.          |
| `slug`           | [`String!`]()      |A lesma de URL da empresa.          |


**enterpriseAdministratorInvitation** ([EnterpriseAdministratorInvitation]())
Procure um convite de administrador de empresa pendente por convidado, empresa e função.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `enterpriseSlug`           | [`String!`]()      |A lesma da empresa à qual o usuário foi convidado a participar.          |
| `role`           | [`EnterpriseAdministratorRole!`]()      |A função do convite do membro de negócios.          |
| `userLogin`           | [`String!`]()      |O login do usuário convidado para ingressar na empresa.          |

**enterpriseAdministratorInvitationByToken** ([EnterpriseAdministratorInvitation]())
Procure um convite de administrador corporativo pendente por token de convite.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `invitationToken`           | [`String!`]()      |O token de convite enviado com o email de convite.          |

**license** ([License]())
Procure uma licença de código aberto por sua chave

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `key`           | [`String!`]()      |O ID SPDX oculto da licença  |

**licences** ( [License]!)

Retornar uma lista de licenças de código aberto conhecidas

**marketplaceCategories** ( [[MarketplaceCategory!]!]() )

Obter lista alfabética de categorias do Marketplace

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `excludeEmpty`           | [`Boolean!`]()      |Excluir categorias sem listagens.  |
| `excludeSubcategories`           | [`Boolean`]()      |Retorna apenas categorias de nível superior, excluindo quaisquer subcategorias.  |
| `includeCategories`           | [`[String!]`]()      |Retorne apenas as categorias especificadas.  |

**marketplaceCategory** ([MarketplaceCategory]())
Procure uma categoria do Marketplace por sua slug.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `slug`           | [`String!`]()      |A lesma de URL da categoria.  |
| `useTopicAliases`           | [`Boolean`]()      |Verifique também os aliases de tópico para a categoria slug  |

**marketplaceListing** ([MarketplaceListing]())
Procure uma única listagem do Marketplace

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `slug`           | [`String!`]()      |Selecione a listagem que corresponde a esta lesma. É o nome abreviado da listagem usada em seu URL. |

**meta** ([GitHubMetadata!]())
Retornar informações sobre a instância do GitHub

**node** ([Node]())
Busca um objeto com seu ID.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `id`           | [`ID!`]()      |ID do objeto.  |

nodes ([[Node]!]())
Pesquise nós por uma lista de IDs.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `id`           | [`[ID!]!`]()      |A lista de IDs de nós.  |

organization ([Organization]())
Pesquise uma organização por login.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `login`           | [`String!`]()      |O logon da organização.  |

**rateLimit** ([RateLimit]())
As informações de limite de taxa do cliente.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `dryRun`           | [`Boolean`]()      |Se verdadeiro, calcule o custo da consulta sem avaliá-la. O valor padrão é false.  |

relay ( Query!)
Corte para solução alternativa [https://github.com/facebook/relay/issues/112](https://github.com/facebook/relay/issues/112) reexpondo o objeto de consulta raiz

**repository** ([Repository]())
Pesquise um determinado repositório pelo proprietário e nome do repositório.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `name`           | [`String!`]()      |O nome do repositório  |
| `owner`           | [`String!`]()      |O campo de logon de um usuário ou organização  |

**repositoryOwner** ([RepositoryOwner]())
Pesquise o proprietário de um repositório (ou seja, um Usuário ou uma Organização) por login.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `login`           | [`String!`]()      |O nome de usuário para pesquisar o proprietário.  |

**resource** ([UniformResourceLocatable]())
Pesquisa de recurso por um URL.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `url`           | [`URI!`]()      |O URL  |

**securityAdvisory** ([SecurityAdvisory]())
Obter um comunicado de segurança por seu ID GHSA

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `ghsaId`           | [`String!`]()      |ID do comunicado de segurança do GitHub.  |

**sponsorsListing** ([SponsorsListing]())
> Aviso de descontinuação
> `Query.sponsorsListing` será removido. Use em `Sponsorable.sponsorsListing` vez disso. Remoção em 2020-04-01 UTC.

Procure uma única listagem de patrocinadores

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `slug`           | [`String!`]()      |Selecione a lista de patrocinadores que corresponde a esta lesma  |

**topic** ([Topic]())
Procure um tópico pelo nome.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `name`           | [`String!`]()      |O nome do tópico.  |

**usuário** ([User]())
Procure um usuário por login.

| Argumento | Tipo | Descrição |
|-----------|------|-----------|
| `login`           | [`String!`]()      |O login do usuário.          |
		


**visualizador** ([User!]())
O usuário atualmente autenticado.
