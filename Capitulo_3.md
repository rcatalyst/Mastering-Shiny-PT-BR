
3.0 UI Básica

3.1 Introdução

Agora que você tem um aplicativo básico, exploraremos os detalhes que o fazem funcionar. Como você viu no capítulo anterior, o Shiny incentiva a separação do código que gera sua interface do usuário (o front end) do código que impulsiona o comportamento do seu aplicativo (o back-end). Neste capítulo, vamos nos aprofundar no front end e explorar as entradas, saídas e layouts em HTML fornecidos pelo Shiny.

Aprender mais sobre o frontend permitirá gerar aplicativos visualmente atraentes, mas simples. No próximo capítulo, você aprenderá mais sobre a reatividade que alimenta o back-end do Shiny, permitindo criar respostas mais ricas à interação.

Como sempre, começaremos carregando o pacote shiny:

```
library(shiny)
```

3.2 Inputs

Como vimos no capítulo anterior, você usa funções como <code>sliderInput()</code>, <code>selectInput()</code>, <code>textInput()</code> e <code>numericInput()</code> para inserir controles de entrada na especificação da UI. Agora discutiremos a estrutura comum subjacente a todas as funções de input e forneceremos uma rápida visão geral das entradas incorporadas ao Shiny.

3.2.1 Estrutura comum

Todas as funções de entrada têm o mesmo primeiro argumento: <code>inputId</code>. Este é o identificador usado para conectar o front-end ao back-end: se sua interface do usuário tiver uma entrada com o ID <code>"name"</code>, a função do server o acessará com <code>input$name</code>.

O <code>inputId</code> possui duas restrições:

<ul>
    <li>Deve ser uma sequência simples que contenha apenas letras, números e sublinhados (não são permitidos espaços, traços, pontos ou outros caracteres especiais!). Nomeie como você nomearia uma variável em R.</li>
    <li>Deve ser único. Se não for exclusivo, você não terá como se referir a esse controle na função do servidor!</li>
</ul>

A maioria das funções de entrada possui um segundo parâmetro chamado <code>label</code>. Isso é usado para criar um rótulo legível por humanos para o controle. O Shiny não impõe restrições a essa sequência, mas você deve pensar cuidadosamente sobre isso para garantir que seu aplicativo possa ser usado por humanos! O terceiro parâmetro geralmente é o valor, que, sempre que possível, permite definir o valor padrão. Os parâmetros restantes são exclusivos para o controle.

Ao criar uma entrada, recomendo fornecer os argumentos <code>inputId</code> e <code>label</code> por posição e todos os outros argumentos por nome:

```
sliderInput("min", "Limit (minimum)", value = 50, min = 0, max = 100)
```

As seções a seguir descrevem as entradas incorporadas ao Shiny, agrupadas livremente de acordo com o tipo de controle que eles criam. O objetivo é fornecer uma visão geral rápida de suas opções, não descrever exaustivamente todos os argumentos. Mostrarei os parâmetros mais importantes para cada controle abaixo, mas você precisará ler a documentação para obter detalhes completos.

3.2.2 Texto livre

Colete pequenas quantidades de texto com <code>textInput()</code>, senhas com <code>passwordInput()</code> e parágrafos de texto com <code>textAreaInput()</code>.

```
ui <- fluidPage(
  textInput("name", "What's your name?"),
  passwordInput("password", "What's your password?"),
  textAreaInput("story", "Tell me about yourself", rows = 3)
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/7d05eded3bee980b9e441f8638890258c45e81b9/a2aaf/screenshots/basic-ui/free-text.png" style="display: block; margin: auto;" width="600">

Se você deseja garantir que o texto tenha determinadas propriedades, use <code>validate()</code>, ao qual voltaremos no capítulo 7.

3.2.3 Entradas numéricas

Para coletar valores numéricos, crie um slider com <code>sliderInput()</code> ou uma caixa de texto restrita com <code>numericInput()</code>. Se você fornecer um vetor numérico de comprimento 2 para o valor padrão de <code>sliderInput()</code>, você obtém um "range" no slider com duas extremidades.

```
ui <- fluidPage(
  numericInput("num", "Number one", value = 0, min = 0, max = 100),
  sliderInput("num2", "Number two", value = 50, min = 0, max = 100),
  sliderInput("rng", "Range", value = c(10, 20), min = 0, max = 100)
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/ba6c90aecddbd0d3df1c366f482f124fe7c6aba3/603a2/screenshots/basic-ui/numeric.png" style="display: block; margin: auto;" width="600">

Geralmente, eu recomendo usar apenas sliders para pequenos intervalos ou casos em que o valor exato não é tão importante. Tentar selecionar com precisão um número em um pequeno slider é um exercício de frustração!

Sliders são extremamente personalizáveis ​​e há muitas maneiras de ajustar sua aparência. Consulte <code>?sliderInput</code> e https://shiny.rstudio.com/articles/sliders.html para obter mais detalhes.

3.2.4 Datas

Colete um único dia com <code>dateInput()</code> ou um intervalo de dois dias com <code>dateRangeInput()</code>. Eles fornecem um seletor de calendário conveniente, e argumentos adicionais como <code>datesdisabled</code> e <code>daysofweekdisabled</code> permitem restringir o conjunto de entradas válidas.

```
ui <- fluidPage(
  dateInput("dob", "When were you born?"),
  dateRangeInput("holiday", "When do you want to go on vacation next?")
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/eb6baa615a5c8d19a871626d6ce021bb1376f0a1/814a6/screenshots/basic-ui/date.png" style="display: block; margin: auto;" width="600">

O formato da data, o idioma e o dia em que a semana começa são os padrões dos EUA. Se você estiver criando um aplicativo com um público internacional, defina o <code>format</code>, o <code>language</code> e o <code>weekstart</code> para que as datas sejam naturais para seus usuários.

3.2.5 Escolhas limitadas

Existem duas abordagens diferentes para permitir ao usuário escolher entre um conjunto pré-especificado de opções: <code>selectInput()</code> e <code>radioButtons()</code>.


```
animals <- c("dog", "cat", "mouse", "bird", "other", "I hate animals")

ui <- fluidPage(
  selectInput("state", "What's your favourite state?", state.name),
  radioButtons("animal", "What's your favourite animal?", animals)
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/2605fed791b02e16d28d2c389df9130d349bf1b3/e49e2/screenshots/basic-ui/limited-choices.png" style="display: block; margin: auto;" width="600">

Os radio buttons têm dois recursos interessantes: mostram todas as opções possíveis, tornando-os adequados para listas curtas e, por meio dos argumentos <code>choiceNames</code> / <code>choiceValues</code>, eles podem exibir outras opções além do texto sem formatação.

```
ui <- fluidPage(
  radioButtons("rb", "Choose one:",
    choiceNames = list(
      icon("angry"),
      icon("smile"),
      icon("sad-tear")
    ),
    choiceValues = list("angry", "happy", "sad")
  )
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/dbe9e03aec37653f1244e95edf4f29c48135bfa5/e7044/screenshots/basic-ui/radio-icon.png" style="display: block; margin: auto;" width="600">

Os Dropdowns criados com <code>selectInput()</code> ocupam a mesma quantidade de espaço, independentemente do número de opções, tornando-as mais adequadas para opções mais longas. Você também pode definir <code>multiple = TRUE</code> para permitir que o usuário selecione vários elementos.

```
ui <- fluidPage(
  selectInput(
    "state", "What's your favourite state?", state.name,
    multiple = TRUE
  )
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/c53795ad09b7866f0ed7adc1b3adabdd6fc120db/437be/images/basic-ui/multi-select.png" style="display: block; margin: auto;" width="234">

Não há como selecionar vários valores com os radio buttons, mas há uma alternativa conceitualmente semelhante: <code>checkboxGroupInput()</code>.

```
ui <- fluidPage(
  checkboxGroupInput("animal", "What animals do you like?", animals)
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/d3d61d703bac03a0d2823da98e2dbba03d6619d4/3276f/screenshots/basic-ui/multi-radio.png" style="display: block; margin: auto;" width="600">

Se você deseja uma única caixa de seleção para uma única pergunta sim/não, use <code>checkboxInput()</code>:

```
ui <- fluidPage(
  checkboxInput("cleanup", "Clean up?", value = TRUE),
  checkboxInput("shutdown", "Shutdown?")
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/ff021265e68d432ea7e3e574849a8f6a8f25b9b0/8dec7/screenshots/basic-ui/yes-no.png" style="display: block; margin: auto;" width="600">

3.2.6 Uploads de arquivos

Permita que o usuário faça upload de um arquivo com <code>fileInput()</code>:

```
ui <- fluidPage(
  fileInput("upload", NULL)
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/92e2422e9b00cec1d6a852cbdb484071ce51ae4e/dacfd/screenshots/basic-ui/upload.png" style="display: block; margin: auto;" width="600">

<code>fileInput()</code> requer tratamento especial no lado do servidor e é discutido em detalhes no Capítulo 8.

3.2.7 Botões de ação

Deixe o usuário executar uma ação com <code>actionButton()</code> ou <code>actionLink()</code>. Eles são mais naturalmente associados a <code>observeEvent()</code> ou <code>eventReactive()</code> na função server; Ainda não discuti essas funções, mas voltaremos a elas no próximo capítulo.

```
ui <- fluidPage(
  actionButton("click", "Click me!"),
  actionButton("drink", "Drink me!", icon = icon("cocktail"))
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/91ce7a6b83974609e9838c57019645f25b8fd2cd/8a1d2/screenshots/basic-ui/action.png" style="display: block; margin: auto;" width="600">

3.2.8 Exercícios

1. Quando o espaço é escasso, é útil rotular as caixas de texto usando um espaço reservado que aparece dentro da área de entrada de texto. Como você chama <code>textInput()</code> para gerar a UI abaixo?

<img src="https://d33wubrfki0l68.cloudfront.net/0250dd2b285e770d5fd2a66670a6604775bb7f1e/42653/screenshots/basic-ui/placeholder.png" style="display: block; margin: auto;" width="600">

2. Leia atentamente a documentação de <code>sliderInput()</code> para descobrir como criar um slider de data, conforme mostrado abaixo.

<img src="https://d33wubrfki0l68.cloudfront.net/16dea4a0f7a4462dfd578a917bdf3e492ed6a7cd/9686e/screenshots/basic-ui/date-slider.png" style="display: block; margin: auto;" width="600">

3. Se você tiver uma lista moderadamente longa, é útil criar subtítulos que dividam a lista em pedaços. Leia a documentação de <code>selectInput()</code> para descobrir como. (Dica: o HTML subjacente é chamado <code>&lt;optgroup&gt;</code>.)

4. Crie um slider de entrada para selecionar valores entre 0 e 100, em que o intervalo entre cada valor selecionável no slider é 5. Em seguida, adicione animação ao widget de entrada para que, quando o usuário pressionar o botão de reprodução, o widget de entrada role automaticamente.

5. Usando a caixa de entrada numérica a seguir, o usuário pode inserir qualquer valor entre 0 e 1000. Qual é o objetivo do argumento step neste widget?

```
numericInput("number", "Select a value", value = 150, min = 0, max = 1000, step = 50)
```

3.3 Outputs

As saídas na UI criam espaços reservados posteriormente preenchidos pela função server. Assim como as entradas, as saídas recebem um ID exclusivo como primeiro argumento: se a especificação da UI criar uma saída com o ID "plot", você a acessará na função server com <code>output$plot</code>.

Cada função de <code>output</code> no front-end é acoplada a uma função <code>render</code> no back-end. Existem três tipos principais de output, correspondentes às três coisas que você geralmente inclui em um relatório: texto, tabelas e gráficos. As seções a seguir mostram os conceitos básicos das funções de output no front end, juntamente com as funções <code>render</code> correspondentes no back end.

3.3.1 Texto

Use <code>textOutput()</code> para saída de texto regular e <code>verbatimTextOutput()</code> para código fixo e saída no console.

```
ui <- fluidPage(
  textOutput("text"),
  verbatimTextOutput("code")
)
server <- function(input, output, session) {
  output$text <- renderText({ 
    "Hello friend!" 
  })
  output$code <- renderPrint({ 
    summary(1:10) 
  })
}
```

<img src="https://d33wubrfki0l68.cloudfront.net/61f37c119d66f0b25bb834d6773274856b764727/6beee/screenshots/basic-ui/output-text.png" style="display: block; margin: auto;" width="600">

Observe que o <code>{}</code> não é necessário nas funções de renderização, a menos que você precise executar várias linhas de código. Você também pode escrever a função server de forma mais compacta. Eu acho que esse geralmente é um bom estilo, pois você deve fazer o mínimo possível de cálculo em suas funções de renderização.

```
server <- function(input, output, session) {
  output$text <- renderText("Hello friend!")
  output$code <- renderPrint(summary(1:10))
}
```

Observe que existem duas funções de renderização que podem ser usadas com uma das funções de saída de texto:

<ul>
<li><code>renderText()</code> que exibe o texto retornado pelo código.</li>
<li><code>renderPrint()</code> que exibe o texto impresso pelo código.</li>
</ul>

Para ajudar a entender a diferença, examine a seguinte função. Ela imprime <code>a</code> e <code>b</code>, e retorna <code>"c"</code>. Uma função pode imprimir várias coisas, mas pode retornar apenas um único valor.

```
print_and_return <- function() {
  print("a")
  print("b")
  "c"
}
x <- print_and_return()
#> [1] "a"
#> [1] "b"
x 
#> [1] "c"
```

3.3.2 Tabelas

Existem duas opções para exibir data frames em tabelas:

<ul>
<li><code>tableOutput()</code> e <code>renderTable()</code> processam uma tabela estática de dados, mostrando todos os dados de uma só vez.</li>
<li><code>dataTableOutput()</code> e <code>renderDataTable()</code> processam uma tabela dinâmica, mostrando um número fixo de linhas junto com os controles para alterar quais linhas estão visíveis.</li>
</ul>

<code>tableOutput()</code> é mais útil para resumos pequenos e fixos (por exemplo, coeficientes de modelo); <code>dataTableOutput()</code> é mais apropriado se você deseja expor um data frame completo para o usuário.

```
ui <- fluidPage(
  tableOutput("static"),
  dataTableOutput("dynamic")
)
server <- function(input, output, session) {
  output$static <- renderTable(head(mtcars))
  output$dynamic <- renderDataTable(mtcars, options = list(pageLength = 5))
}
```

<img src="https://d33wubrfki0l68.cloudfront.net/2fe4c674645896fa18d345ad162f479434746dd2/78343/screenshots/basic-ui/output-table.png" style="display: block; margin: auto;" width="100%">

3.3.3 Plots

Você pode exibir qualquer tipo de gráfico R (base, ggplot2 ou outro) com <code>plotOutput()</code> e <code>renderPlot()</code>:

```
ui <- fluidPage(
  plotOutput("plot", width = "400px")
)
server <- function(input, output, session) {
  output$plot <- renderPlot(plot(1:5))
}
```

<img src="https://d33wubrfki0l68.cloudfront.net/2bc961497fb491d1fc1ace9f30e06245aca0da67/daa6c/screenshots/basic-ui/output-plot.png" style="display: block; margin: auto;" width="600">

Por padrão, <code>plotOutput()</code> ocupará toda a largura de seu contêiner (veremos mais sobre isso em breve) e terá 400 pixels de altura. Você pode substituir esses padrões pelos argumentos de <code>height</code> e <code>width</code>.

Os gráficos são especiais porque são saídas que também podem atuar como entradas. <code>plotOutput()</code> possui vários argumentos como <code>click</code>, <code>dblclick</code> e <code>hover</code>. Se você passar como strings estas <code>click = "plot_click"</code>, elas criarão uma entrada reativa (<code>input$plot_click</code>) que você pode usar para lidar com a interação do usuário na plotagem. Voltaremos aos gráficos interativos em Shiny no capítulo XYZ.

3.3.4 Downloads

Você pode permitir que o usuário baixe um arquivo com <code>downloadButton()</code> ou <code>downloadLink()</code>. Isso exige novas técnicas na função server, portanto, voltaremos a isso no Capítulo 8.

3.3.5 Exercícios

<ol>
  <li>Recrie o aplicativo Shiny da seção de plotagens, dessa vez definindo a altura para 300px e a largura para 700px.</li>
  <li>Adicione uma plotagem adicional à direita da plotagem existente e dimensione-a para que cada plot ocupe metade da largura do aplicativo.</li>
  <li>Atualize as opções da <code>renderDataTable()</code> abaixo para que a tabela seja exibida, mas nada mais, ou seja, remova os comandos de pesquisa, ordenação e filtragem. Você precisará ler <code>?RenderDataTable</code> e revisar as opções em https://datatables.net/reference/option/.</li>
</ol>

```
ui <- fluidPage(
  dataTableOutput("table")
)
server <- function(input, output, session) {
  output$table <- renderDataTable(mtcars, options = list(pageLength = 5))
}
```
3.4 Layouts

Agora que você sabe como criar uma gama completa de entradas e saídas, é necessário organizá-las na página. Esse é o trabalho das funções de layout, que fornecem a estrutura visual de alto nível de um aplicativo. Aqui, focaremos no <code>fluidPage()</code>, que fornece o estilo de layout usado pela maioria dos aplicativos. Nos próximos capítulos, você aprenderá sobre outras famílias de layout, como painéis e caixas de diálogo.

3.4.1 Visão geral

Os layouts são criados por uma hierarquia de chamadas de função, em que a hierarquia em R corresponde à hierarquia de saída. Quando você vê um código de layout complexo como este:

```
fluidPage(
  titlePanel("Hello Shiny!"),
  sidebarLayout(
    sidebarPanel(
      sliderInput("obs", "Observations:", min = 0, max = 1000, value = 500)
    ),
    mainPanel(
      plotOutput("distPlot")
    )
  )
)
```

Primeiro, deslize-o concentrando-se na hierarquia das chamadas de função:

```
fluidPage(
  titlePanel(),
  sidebarLayout(
    sidebarPanel(
      sliderInput("obs")
    ),
    mainPanel(
      plotOutput("distPlot")
    )
  )
)
```

Mesmo sem saber nada sobre as funções de layout, você pode ler os nomes das funções para adivinhar como será esse aplicativo. Você pode imaginar que esse código gerará um design clássico de aplicativo: uma barra de título na parte superior, seguida por uma barra lateral (contendo um slider), com o painel principal contendo uma plotagem.

3.4.2 Funções da página

A função de layout mais importante, mas menos interessante, é <code>fluidPage()</code>. Você já viu isso em todos os exemplos acima, porque usamos para inserir várias entradas ou saídas em um único aplicativo. O que acontece se você usar <code>fluidPage()</code> por si só?

<img src="https://d33wubrfki0l68.cloudfront.net/ad1d199cecafc2c2be10425930b1dcfb5e8dd5d7/46916/images/basic-app/fluid-page.png" style="display: block; margin: auto;" width="70%">

Parece muito chato porque não há conteúdo, mas nos bastidores, <code>fluidPage()</code> está fazendo muito trabalho. A função de página configura todo o HTML, CSS e JS que o Shiny precisa. <code>fluidPage()</code> usa um sistema de layout chamado Bootstrap, https://getbootstrap.com, que fornece padrões atraentes. Mais adiante, no capítulo XYZ, falaremos sobre como você pode usar um pouco de conhecimento sobre o Bootstrap para obter maior controle sobre a aparência visual do seu aplicativo, para torná-lo mais elegante ou para corresponder ao seu guia de estilo corporativo.

Tecnicamente, <code>fluidPage()</code> é tudo o que você precisa para um aplicativo, porque você pode colocar entradas e saídas diretamente dentro dele. Mas, embora isso seja bom para aprender o básico do Shiny, despejar todas as entradas e saídas em um só lugar não parece muito bom, então você precisa aprender mais funções de layout. Aqui, apresentarei duas estruturas comuns, uma página com barra lateral e um aplicativo com várias linhas, e depois terminaremos com uma rápida discussão de temas.

3.4.3 Página com barra lateral

<code>sidebarLayout()</code>, junto com <code>titlePanel()</code>, <code>sidebarPanel()</code> e <code>mainPanel()</code>, facilita a criação de um layout de duas colunas com entradas à esquerda e saídas à direita. O código básico é mostrado abaixo; ele gera a estrutura mostrada na Figura 3.1.

```
fluidPage(
  titlePanel(
    # app title/description
  ),
  sidebarLayout(
    sidebarPanel(
      # inputs
    ),
    mainPanel(
      # outputs
    )
  )
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/bb7351f4082fffdad9e4c199bc12190d104898cb/e2ac8/diagrams/basic-ui/sidebar.png" alt="Structure of a basic app with sidebar" width="336">

Figura 3.1: Estrutura de um aplicativo básico com barra lateral

O exemplo a seguir mostra como usar esse layout para criar um aplicativo muito simples que demonstra o Teorema do Limite Central. Se você mesmo executar esse aplicativo, poderá ver como o aumento do número de amostras torna uma distribuição muito semelhante a uma distribuição normal.

```
ui <- fluidPage(
  headerPanel("Central limit theorem"),
  sidebarLayout(
    sidebarPanel(
      numericInput("m", "Number of samples:", 2, min = 1, max = 100)
    ),
    mainPanel(
      plotOutput("hist")
    )
  )
)

server <- function(input, output, session) {
  output$hist <- renderPlot({
    means <- replicate(1e4, mean(runif(input$m)))
    hist(means, breaks = 20)
  })
}
```

<img src="https://d33wubrfki0l68.cloudfront.net/a3c6cfafe8e207655a8166c64780151c3bfa0c86/39327/screenshots/basic-ui/sidebar.png" style="display: block; margin: auto;" width="100%">

3.4.4 Várias linhas

Sob o capô, o <code>sidebarLayout()</code> é construído sobre um layout flexível de várias linhas, que você pode usar diretamente para criar aplicativos visualmente mais complexos. Como sempre, você começa com <code>fluidPage()</code>. Em seguida, você cria linhas com <code>fluidRow()</code> e colunas com <code>column()</code>. O modelo a seguir gera a estrutura mostrada na Figura 3.2.

```
fluidPage(
  fluidRow(
    column(4, 
      ...
    ),
    column(8, 
      ...
    )
  ),
  fluidRow(
    column(6, 
      ...
    ),
    column(6, 
      ...
    )
  )
)
```

<img src="https://d33wubrfki0l68.cloudfront.net/bb9dffe04f31627d7eb552b73227f7315ca20585/de3d9/diagrams/basic-ui/multirow.png" alt="The structure underlying a simple multi-row app" width="336">

Figura 3.2: A estrutura subjacente a um aplicativo simples de várias linhas

Observe que o primeiro argumento da <code>column()</code> é a largura, e a largura de cada linha deve adicionar até 12. Isso oferece flexibilidade substancial, pois você pode criar facilmente layouts de 2, 3 ou 4 colunas (mais do que isso começa a ficar apertado) ou use colunas estreitas para criar espaçadores.

3.4.5 Temas

No capítulo XYZ, abordaremos todos os detalhes da personalização da aparência visual do seu aplicativo Shiny. Criar um tema completo do zero é muito trabalhoso (mas geralmente vale a pena!), Mas você pode obter algumas vitórias fáceis usando o pacote shinythemes. O código a seguir mostra quatro opções:

```
theme_demo <- function(theme) {
  fluidPage(
    theme = shinythemes::shinytheme(theme),
    sidebarLayout(
      sidebarPanel(
        textInput("txt", "Text input:", "text here"),
        sliderInput("slider", "Slider input:", 1, 100, 30)
      ),
      mainPanel(
        h1("Header 1"),
        h2("Header 2"),
        p("Some text")
      )
    )
  )
}
theme_demo("darkly")
theme_demo("flatly")
theme_demo("sandstone")
theme_demo("united")
```

<p><img src="https://d33wubrfki0l68.cloudfront.net/b48c12e1e4925c8e7849be1c592356b4edfc958f/b7ae2/screenshots/basic-ui/theme-darkly.png" width="50%"><img src="https://d33wubrfki0l68.cloudfront.net/d537e90ccab138e57e24b74d8344a20901ad18b4/25bfc/screenshots/basic-ui/theme-flatly.png" width="50%"><img src="https://d33wubrfki0l68.cloudfront.net/8fd4e4d0af7cb45e93797a4d42d087c6ae44c5c5/27f12/screenshots/basic-ui/theme-sandstone.png" width="50%"><img src="https://d33wubrfki0l68.cloudfront.net/2ef0afc4700714f27c7ae8b3a1b6c5ff216ccd92/72e44/screenshots/basic-ui/theme-united.png" width="50%"></p>

Como você pode ver, o tema do seu aplicativo é bastante direto: você só precisa usar o argumento do tema para <code>fluidPage()</code>. Para descobrir quais temas estão disponíveis e como eles são, dê uma olhada no aplicativo seletor de temas Shiny em https://shiny.rstudio.com/gallery/shiny-theme-selector.html.

3.4.6 Exercícios

<ol>
<li>Modifique o aplicativo Teorema do limite central para que a barra lateral fique à direita e não à esquerda.</li>
<li>Navegue pelos temas disponíveis no pacote shinythemes, escolha um tema atraente e aplique-o no aplicativo Teorema do limite central.</li>
</ol>

3.5 Por debaixo dos panos

No exemplo anterior, você pode ter ficado surpreso ao ver que eu crio um aplicativo Shiny usando uma função, <code>theme_demo()</code>. Isso funciona porque o código Shiny é o código R e você pode usar todas as ferramentas existentes para reduzir a duplicação. Lembre-se da regra de três: se você copiar e colar código mais de três vezes, considere escrever uma função ou usar um loop for.

Todas as funções de entrada, saída e layout retornam HTML, a linguagem descritiva que sustenta todos os sites. Você pode ver esse HTML executando as funções da interface do usuário diretamente no console:

```
fluidPage(
  textInput("name", "What's your name?")
)
```

``` 
<div class="container-fluid">
  <div class="form-group shiny-input-container">
    <label for="name">What's your name?</label>
    <input id="name" type="text" class="form-control" value=""/>
  </div>
</div>
``` 

O Shiny foi desenvolvido para que, como usuário R, você não precise aprender sobre os detalhes do HTML. No entanto, se você já conhece HTML (ou deseja aprender!), Também pode trabalhar diretamente com as tags HTML para atingir qualquer nível de personalização que desejar. E essas abordagens não são de forma alguma exclusivas: você pode misturar funções de alto nível com HTML de baixo nível o quanto quiser. Voltaremos a essas idéias no Capítulo 13, onde você aprenderá mais sobre os recursos de nível inferior para criar HTML diretamente.



