
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


