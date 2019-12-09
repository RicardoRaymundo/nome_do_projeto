[Flutter comandos](README.md)

## Channel
O Flutter possui os seguintes [channels](https://github.com/flutter/flutter/wiki/Flutter-build-release-channels), em ordem crescente de estabilidade:

| Channels | Descrição                                                                                                                                                            |
|:--------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| master | A atual base da árvore, a mais recente construção. Geralmente funcional, embora às vezes quebremos acidentalmente as coisas.                    |
| dev    | A versão mais recente e totalmente testada. Geralmente funcional, mas consulte [Bad Builds](https://github.com/flutter/flutter/wiki/Bad-Builds) para obter uma lista de construções de desenvolvimento "ruins" conhecidas. |
| beta   | Todos os meses, escolhemos o "melhor" desenvolvedor do mês anterior e o promovemos para a versão beta. Essas versões foram testadas com os [codelabs](https://github.com/flutter/flutter/wiki/Codelabs).                 |
| stable | Quando acreditamos que temos uma construção particularmente boa, a promovemos para o canal estável.                                                                  |

Para trocar o canal:

| Comando         | Descrição                                                                                                                                              | Exemplo                               |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------|
| channel         |  Liste os canais de Flutter.                                     | flutter channel    |
| channel         |  Troque os canais de Flutter.                                     | flutter channel `<channel>`   |
