
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

<code class="sourceCode r"><a class="sourceLine" id="cb4-1" data-line-number="1"><span class="kw">library</span>(shiny)</a>
<a class="sourceLine" id="cb4-2" data-line-number="2">ui &lt;-<span class="st"> </span><span class="kw">fluidPage</span>(</a>
<a class="sourceLine" id="cb4-3" data-line-number="3">  <span class="st">"Hello, world!"</span></a>
<a class="sourceLine" id="cb4-4" data-line-number="4">)</a>
<a class="sourceLine" id="cb4-5" data-line-number="5">server &lt;-<span class="st"> </span><span class="cf">function</span>(input, output, session) {</a>
<a class="sourceLine" id="cb4-6" data-line-number="6">}</a>
<a class="sourceLine" id="cb4-7" data-line-number="7"><span class="kw">shinyApp</span>(ui, server)</a></code>
