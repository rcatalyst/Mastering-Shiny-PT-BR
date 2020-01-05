
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

    * Deve ser uma sequência simples que contenha apenas letras, números e sublinhados (não são permitidos espaços, traços, pontos ou outros caracteres especiais!). Nomeie como você nomearia uma variável em R.
    * Deve ser único. Se não for exclusivo, você não terá como se referir a esse controle na função do servidor!

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

3. Se você tiver uma lista moderadamente longa, é útil criar subtítulos que dividam a lista em pedaços. Leia a documentação de <code>selectInput()</code> para descobrir como. (Dica: o HTML subjacente é chamado <code><optgroup></code>.)

4. Crie um slider de entrada para selecionar valores entre 0 e 100, em que o intervalo entre cada valor selecionável no slider é 5. Em seguida, adicione animação ao widget de entrada para que, quando o usuário pressionar o botão de reprodução, o widget de entrada role automaticamente.

5. Usando a caixa de entrada numérica a seguir, o usuário pode inserir qualquer valor entre 0 e 1000. Qual é o objetivo do argumento step neste widget?

```
numericInput("number", "Select a value", value = 150, min = 0, max = 1000, step = 50)
```

