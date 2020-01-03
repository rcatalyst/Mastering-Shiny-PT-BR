
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
