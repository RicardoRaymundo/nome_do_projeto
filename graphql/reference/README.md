[REFERENCIA](https://developer.github.com/v4/)

# Visão global

Aqui estão alguns links rápidos para você começar a trabalhar com a API GraphQL v4:

- [Autenticação]()
- [Ponto final raiz]()
- [Introspecção de esquema]()
- [Limites de taxa]()
- [Migrando do REST]()

## Sobre o GraphQL

A linguagem de consulta de dados do [GraphQL]() é:

- **Uma [especificação]()**. A especificação determina a validade do [esquema]() no servidor da API. O esquema determina a validade das chamadas do cliente.

- [Fortemente digitado](). O esquema define um sistema de tipos de API e todos os relacionamentos de objetos.

- [Introspectivo](). Um cliente pode consultar o esquema para obter detalhes sobre o esquema.

- [Hierárquico](). A forma de uma chamada do GraphQL reflete a forma dos dados JSON que ela retorna. [Os campos aninhados]() permitem consultar e receber apenas os dados especificados em uma única viagem de ida e volta.

- **Uma camada de aplicação**. O GraphQL não é um modelo de armazenamento ou uma linguagem de consulta ao banco de dados. O gráfico refere-se às estruturas de gráfico definidas no esquema, em que os [nós]() definem objetos e as [arestas]() definem os relacionamentos entre os objetos. A API percorre e retorna dados do aplicativo com base nas definições de esquema, independentemente de como os dados são armazenados.

## Por que o GitHub está usando o GraphQL
O GitHub escolheu o GraphQL para a nossa API v4 porque oferece significativamente mais flexibilidade para nossos integradores. A capacidade de definir com precisão os dados que você deseja - e *somente* os dados que você deseja - é uma poderosa vantagem sobre os terminais da API REST v3. O GraphQL permite substituir várias solicitações REST por uma única chamada para buscar os dados que você especificar.

Para mais detalhes sobre por que o GitHub mudou para o GraphQL, consulte a [publicação]() original do [blog de anúncios]().

## Sobre a referência do esquema GraphQL
Os documentos na barra lateral são gerados a partir do [esquema]() do GitHub GraphQL. Todas as chamadas são validadas e executadas no esquema. Use estes documentos para descobrir quais dados você pode chamar:

- Operações permitidas: [consultas]() e [mutações]() .

- Tipos definidos pelo esquema: [escalares](), [objetos](), [enumerações](), [interfaces](), [uniões]() e [objetos de entrada]().

Você pode acessar esse mesmo conteúdo na [barra lateral]() do [Explorer Docs](). Observe que você pode precisar confiar nos documentos e na validação do esquema para chamar com êxito a API do GraphQL.

Para outras informações, como detalhes de autenticação e limite de taxa, consulte os guias .

## Solicitando suporte
Para perguntas, relatórios de bugs e discussões sobre aplicativos GitHub, aplicativos OAuth e desenvolvimento de API, explore o F [órum de suporte e desenvolvimento da API]() do [GitHub](). O fórum é moderado e mantido pela equipe do GitHub, mas as perguntas postadas no fórum não garantem a resposta da equipe do GitHub.

Considere entrar em contato com o [suporte do GitHub]() diretamente usando o formulário de contato para:

- resposta garantida da equipe do GitHub
- solicitações de suporte que envolvam dados confidenciais ou preocupações particulares
- solicitações de recursos
- feedback sobre os produtos GitHub
