[REFERENCIA](https://developer.github.com/v4/guides/resource-limitations/)

<!--  TODO:: Implementar as caixas que envolvem os numeros nos códigos   -->
----------------------

|CONTEÚDOS                                                                                                                                      |
|-----------------------------------------------------------------------------------------------------------------------------------------------|
| [Visão global](README.md)                                                                                                                                   |   
| [Introdução ao GraphQL](https://github.com/RicardoRaymundo/nome_do_projeto/blob/master/guides/introduction_to_graphql.md)                     |   
| [Formação de chamadas](https://github.com/RicardoRaymundo/nome_do_projeto/blob/master/guides/forming-calls/authenticating-with-graphql.md)    |   
| [Usando IDs de Nó Globais](https://github.com/RicardoRaymundo/nome_do_projeto/blob/master/guides/using_global_node_ids.md)                    |   
| [Migrando do REST](https://github.com/RicardoRaymundo/nome_do_projeto/blob/master/guides/migrating_from_rest_to_graphql.md)                   |   
| [Usando o Explorer](https://github.com/RicardoRaymundo/nome_do_projeto/blob/master/guides/using_the_explorer.md)                              |   
| [Gerenciando contas corporativas](https://github.com/RicardoRaymundo/nome_do_projeto/blob/master/guides/managing-enterprise-accounts.md)      |   
| [Limitações de recursos](https://github.com/RicardoRaymundo/nome_do_projeto/blob/master/guides/graphql_resource_limitations.md)               |   

# Limitações de recursos do GraphQL
1. [Limite de nó](#limite-de-nó)
2. [Taxa limite](#taxa-limite)

Como em qualquer API pública, a API GraphQL v4 protege contra chamadas excessivas ou abusivas para os servidores do GitHub.

## Limite de nó
Para passar [esquema]() de validação, todos v4 GraphQL API [chamadas]() devem atender a essas normas:

- Os clientes devem fornecer um argumento `first` ou `last` em qualquer [conexão]().
- Os valores de `first` e `last` devem estar entre 1 e 100.
- Chamadas individuais não podem solicitar mais de 500.000 [nós]() no total .

### Calculando nós em uma chamada
Esses dois exemplos mostram como calcular o total de nós em uma chamada.

1. onsulta simples:

```graphql
query {
  viewer {
    repositories(first: 50) {
      edges {
        repository:node {
          name

          issues(first: 10) {
            totalCount
            edges {
              node {
                title
                bodyHTML
              }
            }
          }
        }
      }
    }
  }
}
```

Cálculo:

    50           = 50 repositórios
    +
    50 x 10   = 500 problemas no repositório
    
                    = 550 nós no total

2. Consulta complexa:

```graphql
query {
  viewer {
    repositories(first: 50) {
      edges {
        repository:node {
          name

          pullRequests(first: 20) {
            edges {
              pullRequest:node {
                title

                comments(first: 10) {
                  edges {
                    comment:node {
                      bodyHTML
                    }
                  }
                }
              }
            }
          }

          issues(first: 20) {
            totalCount
            edges {
              issue:node {
                title
                bodyHTML

                comments(first: 10) {
                  edges {
                    comment:node {
                      bodyHTML
                    }
                  }
                }
              }
            }
          }
        }
      }
    }

    followers(first: 10) {
      edges {
        follower:node {
          login
        }
      }
    }
  }
}
```

Cálculo:
    
    50               = 50 repositórios
    +
    50 x 20        = 1.000 solicitações de recebimento
    +
    50 x 20 x 10 = 10.000 pullRequest comentários
    +
    50 x 20        = 1.000 edições
    +
    50 x 20 x 10 = 10.000 comentários de edições
    +
    10               = 10 seguidores
    
                     = 22.060 nós no total

## Taxa limite
O limite da API do GraphQL v4 é diferente do [limite]() de 5.000 solicitações por hora da API REST v3 para solicitações autenticadas.

Por que os limites de taxa da API são diferentes? Com o [GraphQL](), uma chamada do GraphQL pode substituir [várias chamadas REST](). Uma única chamada GraphQL complexa pode ser equivalente a milhares de solicitações REST. Embora uma única chamada do GraphQL fique bem abaixo do limite de 5.000 / hora da API REST v3, a consulta pode ser igualmente cara para os servidores do GitHub calcularem.

Para representar com precisão o custo do servidor de uma consulta, a API GraphQL v4 calcula a pontuação do limite de taxa de uma chamada com base em uma escala normalizada de pontos. A pontuação de uma consulta leva em consideração o primeiro e o último argumento em uma conexão pai e seus filhos.

- A fórmula usa os argumentos `first` e `last` em uma conexão pai e seus filhos para pré-calcular a carga potencial nos sistemas do GitHub, como MySQL, ElasticSearch e Git.
- Cada nova conexão tem seu próprio valor de ponto. Os pontos são combinados com outros pontos da chamada em uma pontuação geral de limite de taxa.

O limite de taxa da API do GraphQL v4 é de **5.000 pontos por hora** . Observe que 5.000 pontos por hora não é o mesmo que 5.000 chamadas por hora: a API GraphQL v4 e a API REST v3 usam limites de taxa diferentes.

> Nota : A fórmula atual e o limite de taxa estão sujeitos a alterações, conforme observamos como os desenvolvedores usam a API do GraphQL v4.

### Retornando o status do limite de taxa de uma chamada

Com a API REST v3, você pode verificar o status do limite de taxa [inspecionando]() os cabeçalhos HTTP retornados.

Com a API GraphQL v4, você pode verificar o status do limite de taxa consultando os campos no `rateLimit` objeto:

[Executar no Explorer]()

```graphql
query {
  viewer {
    login
  }
  rateLimit {
    limit
    cost
    remaining
    resetAt
  }
}
```

- O `limit` campo retorna o número máximo de pontos que o cliente pode consumir em uma janela de 60 minutos.

- O `cost` campo retorna o custo em pontos para a chamada atual que conta contra o limite da taxa.

- O `remaining` campo retorna o número de pontos restantes na janela atual do limite de taxa.)

- O `resetAt` campo retorna o horário em que a janela atual do limite de taxa é redefinida em [UTC](), em [segundos]().

### Calculando uma pontuação de limite de taxa antes de executar a chamada

Consultar o `rateLimit` objeto retorna a pontuação de uma chamada, mas a execução conta contra o limite. Para evitar esse dilema, você pode calcular a pontuação de uma chamada antes de executá-la. O cálculo a seguir calcula aproximadamente o mesmo custo que `rateLimit { cost }` retorna.

1. Adicione o número de solicitações necessárias para atender cada conexão exclusiva na chamada. Suponha que cada solicitação atinja os limites `first` ou `last` argumento.
2. Divida o número por **100** e arredonde o resultado para obter o custo agregado final. Esta etapa normaliza grandes números.

> Nota : O custo mínimo de uma chamada para a API do GraphQL v4 é 1 , representando uma única solicitação.

Aqui está um exemplo de consulta e cálculo de pontuação:

[Executar no Explorer]()

```graphql
query {
  viewer {
    login
    repositories(first: 100) {
      edges {
        node {
          id

          issues(first: 50) {
            edges {
              node {
                id

                labels(first: 60) {
                  edges {
                    node {
                      id
                      name
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

Esta consulta requer 5.101 solicitações para atender:

- Embora retornemos 100 repositórios, a API precisa se conectar à conta do visualizador **uma vez** para obter a lista de repositórios. Portanto, solicitações de repositórios = 1
- Embora retornemos 50 problemas, a API precisa se conectar a cada um dos 100 repositórios para obter a lista de problemas. Portanto, solicitações de problemas = **100**
- Embora retornemos 60 marcadores, a API precisa se conectar a cada um dos **5.000** possíveis problemas totais para obter a lista de marcadores. Portanto, solicitações de rótulos = **5.000**
- Total = 5.101

Dividindo por 100 e arredondando, obtemos a pontuação final da consulta: **51**
