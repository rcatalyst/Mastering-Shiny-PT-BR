
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

Existem várias maneiras de criar um aplicativo Shiny. O mais simples é criar um novo diretório para o seu aplicativo e colocar um único arquivo chamado <code>app.R</code> nele. Este arquivo <code>app.R</code> será usado para informar ao Shiny a aparência e o comportamento do aplicativo.

Experimente criar um novo diretório e adicione um arquivo <code>app.R</code> parecido com este:

```
library(shiny)
ui <- fluidPage(
  "Hello, world!"
)
server <- function(input, output, session) {
}
shinyApp(ui, server)
```
Dica do RStudio: você pode criar facilmente um novo diretório e um arquivo <code>app.R</code> contendo um aplicativo básico Shiny em uma etapa clicando em File | New Project e, em seguida, selecione “New Directory” e “Shiny Web Application”. Ou, se você já criou o arquivo <code>app.R</code>, pode rapidamente usar um atalho digitando "shinyapp" e pressionando Shift+Tab.

Este é um aplicativo Shiny completo, embora trivial! Observando atentamente o código acima, nosso <code>app.R</code> faz quatro coisas:

    1. Ele chama library(shiny) para carregar o pacote Shiny.
    2. Ele define a interface do usuário, a página HTML com a qual os humanos interagem. Nesse caso, é uma página que contém as palavras "Olá, mundo!".
    3. Ele especifica o comportamento do nosso aplicativo, definindo uma função server. No momento, ele está vazio, então nosso aplicativo não faz nada, mas voltaremos a revisar isso em breve.
    4. Ele executa o shinyApp(ui, server) para construir e iniciar um aplicativo Shiny a partir da interface do usuário e do servidor.


2.3 Executando e parando

Existem algumas maneiras de executar este aplicativo:

    * Clique no botão Run App na barra de ferramentas do documento.
    
<img src="https://d33wubrfki0l68.cloudfront.net/23a8bff2e02f95092ff3b3ea6bc524020aef7de3/2db27/images/basic-app/run-app.png" style="display: block; margin: auto auto auto 0;" width="74">
    
    * Use um atalho de teclado: Cmd/Ctrl + Shift + Enter.
    * Se você não estiver usando o RStudio, poderá usar o source() no documento inteiro, ou chamar shiny::runApp() com o caminho para o diretório que contém o app.R.

Escolha uma dessas opções e verifique se você vê o mesmo aplicativo da Figura 2.1. Parabéns! Você criou seu primeiro aplicativo Shiny.

<img src="https://d33wubrfki0l68.cloudfront.net/e9e6b44c85c169aedd2c4e630022e7958aa57696/06ba0/images/basic-app/hello-world.png" alt="The very basic shiny app you'll see when you run the code above" width="440">

Figura 2.1: O aplicativo Shiny muito básico que você verá quando executar o código acima

Antes de fechar o aplicativo, volte ao RStudio e veja o console R. Você notará que ele diz algo como:

<code>#> Listening on http://127.0.0.1:3827</code>

Isso indica a URL em que seu aplicativo pode ser encontrado: 127.0.0.1 é um endereço padrão que significa "este computador" e 3827 é um número de porta atribuído aleatoriamente. Você pode inserir essa URL em qualquer navegador compatível para abrir outra cópia do seu aplicativo.

Observe também que o R está ocupado: o prompt R não está visível e a barra de ferramentas do console exibe um ícone de stop. Enquanto um aplicativo Shiny está em execução, ele "bloqueia" o console do R. Isso significa que você não pode executar novos comandos no console R até que o aplicativo Shiny pare.

Você pode parar o aplicativo e retornar o acesso ao console usando qualquer uma destas opções:

    * Clique no ícone de stop na barra de ferramentas do console R.
    * Clique no console e pressione Esc (ou pressione Ctrl + C se não estiver usando o RStudio).
    * Feche a janela do aplicativo Shiny.

O fluxo de trabalho básico do desenvolvimento de aplicativos Shiny é escrever um código, iniciar o aplicativo, experimentar o aplicativo, reproduzi-lo, escrever um pouco mais de código, ... Você aprenderá outros padrões posteriormente no Capítulo 6.

2.4 Adicionando controles de UI (Interface de Usuário)

Em seguida, adicionaremos algumas entradas e saídas à nossa interface do usuário para que não seja tão mínimo. Vamos criar um aplicativo muito simples que mostra todos os quadros de dados internos incluídos no pacote de conjuntos de dados.

Substitua sua <code>ui</code> por este código:

``` 
ui <- fluidPage(
  selectInput("dataset", label = "Dataset", choices = ls("package:datasets")),
  verbatimTextOutput("summary"),
  tableOutput("table")
)
```
Este exemplo usa quatro novas funções:

    * fluidPage() é uma função de layout que configura a estrutura visual básica da página. Você aprenderá mais sobre eles na Seção 3.4.
    * selectInput() é um controle de entrada que permite ao usuário interagir com o aplicativo fornecendo um valor. Nesse caso, é uma caixa de seleção com o rótulo "Dataset" e permite escolher um dos conjuntos de dados integrados que acompanham o R. Você aprenderá mais sobre as entradas na Seção 3.2.
    * verbatimTextOutput() e tableOutput() são controles de saída que informam ao Shiny onde colocar a saída renderizada (veremos como em outro momento). verbatimTextOutput() exibe código e tableOutput exibe tabelas. Você aprenderá mais sobre saídas na Seção 3.3.

Funções de layout, entradas e saídas têm usos diferentes, mas são basicamente as mesmas: são todas maneiras sofisticadas de gerar HTML e, se você chamar qualquer uma delas fora de um aplicativo Shiny, verá HTML impresso no console. Não tenha medo de bisbilhotar para ver como esses vários layouts e controles funcionam sob o capô. Você aprenderá mais sobre os detalhes no capítulo 13.

Vá em frente e execute o aplicativo novamente. Agora você verá a Figura 2.2, uma página que contém uma caixa de seleção. Nós vemos apenas a entrada, e não as duas saídas, porque ainda não dissemos ao Shiny como as entradas e saídas estão relacionadas.

<img src="https://d33wubrfki0l68.cloudfront.net/17eadbf2ccdea8d4648b05d486dfb465f562df69/1f1b0/screenshots/basic-app/ui.png" alt="The datasets app with UI" width="600">

Figura 2.2: O aplicativo datasets com UI

2.5 Adicionando comportamento

Em seguida, daremos vida às saídas definindo-as na função de servidor.

Shiny usa programação reativa para tornar os aplicativos interativos. Você aprenderá mais sobre programação reativa no Capítulo 4, mas, por enquanto, esteja ciente de que isso envolve dizer ao Shiny como executar um cálculo, não ordenando que o Shiny o faça. É como a diferença entre dar a alguém uma receita e exigir que ela faça um sanduíche para você.

Nesse caso simples, informaremos ao Shiny como preencher o <code>summary</code> e saídas de <code>table</code> - fornecendo as "receitas" para esses resultados. Substitua sua função vazia de <code>server</code> por esta:

```
server <- function(input, output, session) {
  output$summary <- renderPrint({
    dataset <- get(input$dataset, "package:datasets")
    summary(dataset)
  })
  
  output$table <- renderTable({
    dataset <- get(input$dataset, "package:datasets")
    dataset
  })
}
```

Quase toda saída que você escrever no Shiny seguirá o mesmo padrão:

```
output$ID <- renderTYPE({
  # Expressão que gera qualquer tipo de saída 
  # que o renderTYPE espera
})
```
O lado esquerdo do operador de atribuição (<code><-</code>), <code>output$ID</code>, indica que você está fornecendo a receita da saída do Shiny com o ID correspondente. O lado direito da atribuição usa uma função de renderização específica para concluir algum código que você fornece; no exemplo acima, usamos <code>renderPrint()</code> e <code>renderTable()</code> para encerrar nossa lógica específica do aplicativo.

Cada função <code>render*</code> foi projetada para funcionar com um tipo específico de saída que é passado para uma função <code>*Output</code>. Nesse caso, estamos usando <code>renderPrint()</code> para capturar e exibir um resumo estatístico dos dados com texto de largura fixa (literalmente) e <code>renderTable()</code> para exibir o quadro de dados real em uma tabela.

Execute o aplicativo novamente e brinque, observando o que acontece com a saída quando você altera uma entrada. A Figura 2.3 mostra o que você verá quando abrir o aplicativo.

<img src="https://d33wubrfki0l68.cloudfront.net/bb766cc235f190fd2c28d8f011edb7f9cbe526a7/4a065/screenshots/basic-app/server.png" alt="Now that we've provided a server function that connects and inputs, we have a fully functional app" width="701">

Figura 2.3: Agora que fornecemos uma função de servidor que se conecta e insere, temos um aplicativo totalmente funcional

Observe que não escrevi nenhum código que verifique se há alterações no <code>input$dataset</code> e atualize explicitamente os dois outputs. Isso ocorre porque as saídas são reativas: elas recalculam automaticamente quando as entradas são alteradas. Como os dois blocos de código de renderização que escrevi usavam o <code>input$dataset</code>, sempre que o valor de <code>input$dataset</code> muda (ou seja, o usuário altera sua seleção na UI), ambas as saídas recalculam e atualizam no navegador.

2.6 Reduzindo a duplicação com expressões reativas

Mesmo neste exemplo simples, temos algum código duplicado: a seguinte linha está presente nas duas saídas.

```
dataset <- get(input$dataset, "package:datasets")
```

Em todo tipo de programação, é uma prática ruim ter código duplicado; pode ser um desperdício computacional e, mais importante, aumenta a dificuldade de manter ou depurar o código. Não é tão importante aqui, mas eu queria ilustrar a ideia básica em um contexto muito simples.

No script R tradicional, usamos duas técnicas para lidar com código duplicado: capturamos o valor usando uma variável ou capturamos o cálculo com uma função. Infelizmente, nenhuma dessas abordagens funciona aqui, por razões que você aprenderá na Seção 14.2, e precisamos de um novo mecanismo: expressões reativas.

Você cria uma expressão reativa envolvendo um bloco de código em <code>reactive({...})</code> e atribuindo-o a uma variável e usando uma expressão reativa chamando-a como uma função. Mas, embora pareça que você está chamando uma função, uma expressão reativa tem uma diferença importante: ela é executada apenas na primeira vez em que é chamada e, em seguida, armazena em cache o resultado até precisar ser atualizada.

Podemos potencializar nosso <code>server()</code> para usar expressões reativas, como mostrado abaixo. O aplicativo se comporta de forma idêntica, mas funciona de forma um pouco mais eficiente, pois só precisa recuperar o conjunto de dados uma vez, e não duas.

```
server <- function(input, output, session) {
  dataset <- reactive({
    get(input$dataset, "package:datasets")
  })

  output$summary <- renderPrint({
    summary(dataset())
  })
  
  output$table <- renderTable({
    dataset()
  })
}
```

Voltaremos à programação reativa várias vezes, mas mesmo com um conhecimento superficial de entradas, saídas e expressões reativas, é possível criar aplicativos Shiny bastante úteis!



