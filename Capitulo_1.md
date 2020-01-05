1.0 Prefácio

1.1 O que é Shiny?

Se você nunca usou o Shiny antes, seja bem-vindo! Shiny é um pacote R que permite criar facilmente aplicativos da web interativos e ricos. Shiny permite que você pegue seu trabalho em R e o exponha através de um navegador da Web para que qualquer pessoa possa usá-lo. O Shiny faz você parecer incrível, facilitando a produção de aplicativos da Web polidos com um mínimo de esforço.

No passado, a criação de aplicativos da web era difícil para a maioria dos usuários de R, porque:

<ul>
    <li>Você precisava de um conhecimento profundo de tecnologias da web como HTML, CSS e JavaScript.</li>
    <li>A criação de aplicativos interativos complexos requer uma análise cuidadosa dos fluxos de interação para garantir que, quando uma entrada for alterada, apenas as saídas relacionadas sejam atualizadas.</li>
</ul>

O Shiny torna significativamente mais fácil para o programador R criar aplicativos da web:

<ul>
    <li>Fornecendo um conjunto cuidadosamente organizado de funções da interface do usuário (UI para abreviar) que geram o HTML, CSS e JavaScript necessários para tarefas comuns. Isso significa que você não precisa conhecer os detalhes de HTML / CSS / JS até querer ir além do básico que o Shiny fornece para você.</li>
    <li>Introduzindo um novo estilo de programação chamado programação reativa que rastreia automaticamente as dependências de um pedaço de código. Isso significa que sempre que uma entrada é alterada, o Shiny pode descobrir automaticamente como realizar a menor quantidade de trabalho para atualizar todas as saídas relacionadas.</li>
</ul>

As pessoas usam o Shiny para:

<ul>
    <li>Criar painéis que acompanhem importantes indicadores de desempenho e facilitem a busca por resultados surpreendentes.</li>
    <li>Substituir centenas de páginas de PDFs por aplicativos interativos que permitem que o usuário pule para a fatia exata dos resultados de que gosta.</li>
    <li>Comunicar modelos complexos a um público não técnico com visualizações informativas e análise de sensibilidade interativa.</li>
    <li>Fornecer análise de dados de autoatendimento para fluxos de trabalho comuns, substituindo solicitações de email por um aplicativo Shiny que permite que as pessoas carreguem seus próprios dados e executem análises padrão.</li>
    <li>Criar demonstrações interativas para o ensino de estatística e conceitos de ciência de dados que permitam aos alunos ajustar entradas e observar os efeitos posteriores dessas alterações em uma análise.</li>
</ul>

Em resumo, o Shiny oferece a capacidade de transmitir alguns de seus superpoderes R para qualquer pessoa que possa usar um navegador da web.

1.2 Quem deve ler este livro?

Este livro é destinado a dois públicos principais:

<ul>
    <li>Usuários R interessados em aprender sobre o Shiny para transformar suas análises em aplicativos da web interativos. Para tirar o máximo proveito deste livro, você deve se sentir confortável usando R para fazer a análise de dados e deve ter escrito pelo menos algumas funções.</li>
    <li>Quem já são usuários do Shiny e querem aprimorar seus conhecimentos sobre a teoria subjacente ao Shiny para escrever aplicativos de alta qualidade com mais rapidez e facilidade. Você deve achar este livro particularmente útil se seus aplicativos estiverem começando a aumentar e você estiver tendo problemas para gerenciar a complexidade.</li>
</ul>

1.3 O que você vai aprender?

O livro está dividido em cinco partes:

<ul>
    <li>Em "Introdução", você aprenderá os conceitos básicos do Shiny para poder começar a trabalhar o mais rápido possível. Você aprenderá sobre os conceitos básicos da estrutura do aplicativo, componentes úteis da interface do usuário e os fundamentos da programação reativa.</li>
    <li>O "Shiny em ação", baseia-se no básico para ajudá-lo a resolver problemas comuns, incluindo feedback ao usuário, upload e download de dados, geração de interface do usuário com código, redução da duplicação de código e uso do Shiny para programar com o tidyverse.</li>
    <li>"Dominado a Interface de Usuário (UI)", mergulha nos detalhes da interface do usuário. Você aprenderá pacotes que o ajudarão a criar outros tipos de interface do usuário, como painéis e gadgets RStudio, e aprenderá o básico de HTML e CSS para personalizar o Shiny para atender exatamente às suas necessidades.</li>
    <li>Em "Dominando a reatividade", você aprofundará a teoria e a prática da programação reativa, o paradigma de programação subjacente ao Shiny. Se você já é um usuário brilhante, obterá o máximo de valor deste capítulo, pois ele fornecerá uma base teórica sólida que permitirá criar novas ferramentas especificamente adaptadas aos seus problemas.</li>
    <li>Por fim, em "Domesticando o Shiny", concluiremos uma pesquisa de técnicas úteis para fazer com que seus aplicativos Shiny funcionem bem na produção. Você aprenderá como medir e melhorar o desempenho, depurar problemas quando eles derem errado e gerenciar as dependências do seu aplicativo.</li>
</ul>

1.4 O que você não aprendeu?

O foco deste livro é tornar aplicativos Shiny eficazes e entender a teoria subjacente da reatividade. Farei o possível para mostrar as práticas recomendadas para ciência de dados, programação R e engenharia de software, mas você precisará de outras referências para dominar essas importantes habilidades. Se você gostou da redação deste livro, poderá aproveitar meus outros livros sobre estes tópicos: R for data science, Advanced R, e R packages.

1.5 Pré-requisitos

Antes de continuarmos, verifique se você tem todo o software necessário para este livro:

<ul>
    <li>R: Se você ainda não possui o R instalado, pode estar lendo o livro errado; Presumo uma familiaridade básica com R ao longo deste livro. Se você quiser aprender a usar o R, recomendo o meu R for Data Science, projetado para colocar você em funcionamento com o R com o mínimo de esforço.</li>
    <li>RStudio: O RStudio é um ambiente de desenvolvimento integrado (IDE) gratuito e de código aberto para R. Embora você possa escrever e usar aplicativos Shiny com qualquer ambiente R (incluindo R GUI e ESS), o RStudio possui alguns recursos interessantes especificamente para criação, depuração e implantando aplicativos brilhantes. Recomendamos experimentá-lo, mas não é necessário ter sucesso com o Shiny ou com este livro. Você pode fazer o download do RStudio Desktop em https://www.rstudio.com/products/rstudio/download</li>
    <li>Pacotes R: Este livro usa vários pacotes R. Você pode instalá-los todos de uma vez executando:</li>
</ul>

```
install.packages(c(
  "gapminder", "ggforce", "openintro", "shiny", "shinyFeedback", 
  "shinythemes", "tidyverse", "vroom", "waiter" 
))
```

1.6 Agradecimentos

Este livro foi escrito em formato aberto e os capítulos foram anunciados no twitter quando concluídos. É realmente um esforço da comunidade: muitas pessoas lêem rascunhos, corrigem erros de digitação, sugerem melhorias e contribuem com conteúdo. Sem esses colaboradores, o livro não seria tão bom quanto é, e estou profundamente agradecido por sua ajuda.

Um grande obrigado a todas as 12 pessoas que contribuíram com melhorias específicas via solicitações de recebimento do GitHub (em ordem alfabética por nome de usuário): @chsafouane, David Granjon (@DivadNojnarg), Federico Marini (@federicomarini), Hedley (@ heds1), Joe Cheng ( @ jcheng5), @jyuu, Malcolm Barrett (@malcolmbarrett), Mine Cetinkaya-Rundel (@ mine-cetinkaya-rundel), Pietro Monticone (@pitmonticone), psicometrista (@psychometrician), Shixiang Wang (@ShixiangWang), Tanner Stauss @tmstauss).

1.7 Cólofon

Este livro foi escrito no RStudio usando bookdown. O site é hospedado com netlify e atualizado automaticamente após cada confirmação por travis-ci. A fonte completa está disponível no GitHub.

Esta versão do livro foi criada com a versão R 3.6.1 (27-01- 2017) e os seguintes pacotes:

<table>
<thead>
<tr class="header">
<th align="left">package</th>
<th align="left">version</th>
<th align="left">source</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">gapminder</td>
<td align="left">0.3.0</td>
<td align="left">CRAN (R 3.6.1)</td>
</tr>
<tr class="even">
<td align="left">ggforce</td>
<td align="left">0.3.1</td>
<td align="left">CRAN (R 3.6.1)</td>
</tr>
<tr class="odd">
<td align="left">openintro</td>
<td align="left">1.7.1</td>
<td align="left">CRAN (R 3.6.1)</td>
</tr>
<tr class="even">
<td align="left">shiny</td>
<td align="left">1.4.0</td>
<td align="left">CRAN (R 3.6.1)</td>
</tr>
<tr class="odd">
<td align="left">shinythemes</td>
<td align="left">1.1.2</td>
<td align="left">CRAN (R 3.6.1)</td>
</tr>
<tr class="even">
<td align="left">tidyverse</td>
<td align="left">1.2.1</td>
<td align="left">CRAN (R 3.6.1)</td>
</tr>
<tr class="odd">
<td align="left">vroom</td>
<td align="left">1.0.2</td>
<td align="left">CRAN (R 3.6.1)</td>
</tr>
</tbody>
</table>

