
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


