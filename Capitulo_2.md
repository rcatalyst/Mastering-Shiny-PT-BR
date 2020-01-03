
2.0 Seu primeiro aplicativo Shiny

2.1 Introdução

Neste capítulo, criaremos um aplicativo Shiny simples. Começarei mostrando o padrão mínimo necessário para um aplicativo Shiny e, em seguida, você aprenderá como iniciá-lo e pará-lo. Em seguida, você aprenderá os dois componentes principais de cada aplicativo Shiny: a UI (abreviação de interface do usuário) que define a aparência do aplicativo e a função do servidor que define como o aplicativo funciona. O Shiny usa a programação reativa para atualizar automaticamente as saídas quando as entradas mudam. Concluíremos o capítulo aprendendo o terceiro componente importante dos aplicativos Shiny: expressões reativas.

Se você ainda não instalou o Shiny, instale-o agora com:

```
install.packages("shiny")
```

Em seguida, carregue na sua sessão R atual:

```
library(shiny)
```

2.2 Criar diretório e arquivo do aplicativo

Existem várias maneiras de criar um aplicativo Shiny. O mais simples é criar um novo diretório para o seu aplicativo e colocar um único arquivo chamado app.R nele. Este arquivo app.R será usado para informar ao Shiny a aparência e o comportamento do aplicativo.

Experimente criando um novo diretório e adicionando um arquivo app.R parecido com este:

```
library(shiny)
ui <- fluidPage(
  "Hello, world!"
)
server <- function(input, output, session) {
}
shinyApp(ui, server)
```


