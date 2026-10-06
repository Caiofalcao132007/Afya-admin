# Afya Admin — Dashboard com Blazor WebAssembly e MudBlazor

## Identificação

| | |
|---|---|
| **Aluno(a)** | Caio Gabriel Falcão Nascimento |
| **Matrícula** | 2627899 |
| **Faculdade** | Afya são Lucas campus 2 pvh-RO |
| **Curso** | Ciências da computação |
| **Disciplina** | Desenvolvimento web |
| **Professor(a)** | Liluyoud cury |
| **Semestre** | 2026.2 |

## Objetivo do projeto

O projeto tem como objetivo me familiarizar com o desenvolvimento web usando Blazor WebAssembly, a biblioteca de componentes MudBlazor e o ambiente .NET. A ideia é construir, passo a passo, uma interface de painel administrativo completa sem escrever CSS próprio, usando apenas componentes, tema e classes utilitárias do MudBlazor.

A página é um dashboard para a plataforma fictícia "Afya Pedagógico", com dados fictícios. Ela tem um sidebar com logo e menu de navegação, uma barra superior (breadcrumb, busca, alternância de tema claro/escuro, notificações e menu do usuário), quatro cards de indicadores com mini gráfico de tendência, um gráfico de linha de Receita x Meta, um gráfico de rosca de Distribuição de Clientes, a lista de Performance dos Projetos, o feed de Atividades Recentes e a tabela de Projetos Recentes.

Como não há backend, os dados ficam em `Data/DashboardData.cs` e chegam aos componentes por parâmetros. A página é responsiva (celular, tablet e desktop), tem tema escuro e lembra a escolha de tema do usuário.

## Tecnologias utilizadas

- .NET 10 / Blazor WebAssembly
- MudBlazor 9
- C# e Razor
- Git e GitHub
- VS Code com a extensão C# Dev Kit
- Fonte Inter (Google Fonts)

## Como executar

Passo a passo para outra pessoa clonar e rodar o projeto:

```bash
git clone https://github.com/Caiofalcao132007/Afya-admin.git
cd Afya-admin
dotnet watch
```

É necessário o **.NET SDK 10** 

## Telas

### Tema claro
![Dashboard — tema claro](wwwroot\prints\Captura de tela 2026-10-05 184959.png)

### Tema escuro
![Dashboard — tema escuro](wwwroot\prints\Captura de tela 2026-10-05 185013.png)

### Versão mobile
![Dashboard — celular](wwwroot\prints\Captura de tela 2026-10-05 185048.png)

### HTML gerado (DevTools)
![Inspeção do HTML no DevTools](wwwroot\prints\Captura de tela 2026-10-05 185121.png)
![Inspeção do HTML no DevTools](wwwroot\prints\Captura de tela 2026-10-05 185309.png)
![Inspeção do HTML no DevTools](wwwroot\prints\Captura de tela 2026-10-05 185318.png)
![Inspeção do HTML no DevTools](wwwroot\prints\Captura de tela 2026-10-05 185327.png)


Inspecionei o card de KPI "Receita" e o botão "Novo Projeto". O `<MudPaper>` do card virou uma `<div>` com as classes `mud-paper` e `mud-elevation-1` (do parâmetro `Elevation="1"`) e, junto delas, a `pa-4` que escrevi em `Class="pa-4"`: o MudBlazor soma a minha classe às que ele mesmo gera. O `<MudStack>` virou uma `<div>` com a classe `mud-stack`, e o `<MudButton>` virou um `<button>` com classes `mud-button`. O mesmo acontece com o `<MudDivider Class="mx-3 my-3">` do layout, que aparece como `<hr class="mud-divider ... mx-3 my-3">`. (Confira este texto contra o seu print antes de enviar.)

## Estrutura do projeto

```
afya-admin/
├── Components/
│   ├── AtividadesRecentes.razor
│   ├── CabecalhoPagina.razor
│   ├── DashboardCard.razor
│   ├── GraficoDistribuicaoClientes.razor
│   ├── GraficoReceita.razor
│   ├── KpiCard.razor
│   ├── PerformanceProjetos.razor
│   ├── ProjetosRecentes.razor
│   ├── SeletorPeriodo.razor
│   └── Ui.cs
├── Data/
│   └── DashboardData.cs
├── Layout/
│   ├── MainLayout.razor
│   └── NavMenu.razor
├── Pages/
│   ├── Dashboard.razor
│   └── NotFound.razor
├── Properties/launchSettings.json
├── docs/prints/
├── wwwroot/
│   ├── css/app.css
│   ├── img/alex-morgan.jpg
│   └── index.html
├── _Imports.razor
├── afya-admin.csproj
├── App.razor
├── Program.cs
└── README.md
```

- `Components`: peças visuais reutilizáveis; recebem tudo por parâmetros e não sabem de onde vêm os dados.
- `Data`: records (modelos) e os dados fictícios; responde "o quê" mostrar.
- `Layout`: a moldura da aplicação (tema, AppBar, sidebar e menu), usada em todas as páginas.
- `Pages`: páginas com rota (`@page`); o `Dashboard.razor` apenas monta os componentes.
- `wwwroot`: arquivos estáticos servidos ao navegador (`index.html`, imagens e o CSS global do template).

## Componentes criados

| Componente | Responsabilidade | Parâmetros que recebe |
|---|---|---|
| `DashboardCard` | Card base com título, subtítulo opcional, ações, menu "⋮" e conteúdo; usado por cinco blocos | `Titulo`, `Subtitulo`, `Acoes`, `Menu`, `ChildContent` |
| `CabecalhoPagina` | Título e subtítulo da página à esquerda, botões à direita | `Titulo`, `Subtitulo`, `Acoes` |
| `SeletorPeriodo` | Menu em forma de botão para escolher o período; avisa a página da escolha | `Opcoes`, `Valor`, `ValorChanged` |
| `KpiCard` | Card de indicador com ícone, valor, variação e sparkline | `Kpi` |
| `GraficoReceita` | Gráfico de linha Receita x Meta | `Meses`, `Receita`, `Meta` |
| `GraficoDistribuicaoClientes` | Gráfico de rosca com total no centro e legenda com percentuais | `Total`, `Segmentos` |
| `PerformanceProjetos` | Lista de projetos com barra de progresso e tarefas concluídas | `Projetos` |
| `AtividadesRecentes` | Feed de atividades com ícone, iniciais, descrição e tempo | `Atividades` |
| `ProjetosRecentes` | Tabela de projetos com status, progresso, prazo e menu de ações | `Projetos` |

## O que aprendi

1. Como uma aplicação Blazor WebAssembly inicia no navegador? Qual é o papel do `index.html`, da `<div id="app">` e do `Program.cs`?

  Uma aplicação Blazor WebAssembly começa pelo arquivo index.html, que é carregado pelo navegador. Nele existe a <div id="app">, que funciona como o espaço onde a aplicação Blazor vai ser exibida.

Depois, o Program.cs é responsável por iniciar a aplicação Blazor e configurar os componentes e serviços necessários. Quando o Blazor é carregado, ele usa a <div id="app"> como ponto inicial para renderizar a interface.

2. Qual é a diferença entre um **Layout**, uma **Page** e um **Component** neste projeto? Dê um exemplo de cada.

   O Layout define a estrutura que será usada em várias páginas da aplicação, como o menu lateral e o cabeçalho. Um exemplo é o MainLayout.razor.

A Page é uma tela específica da aplicação que pode ser acessada por uma rota. Um exemplo é o Home.razor, que representa a página inicial.

O Component é uma parte reutilizável da interface, que pode ser usada dentro de páginas ou layouts. Um exemplo seria um NavMenu.razor, usado para criar o menu de navegação.

3. O que é um `RenderFragment` e como o `DashboardCard` usa esse recurso para ser reutilizado por vários cards?

  Um RenderFragment é uma forma de passar um conteúdo de interface para dentro de um componente. O DashboardCard usa esse recurso para receber diferentes conteúdos e assim poder ser reutilizado para criar vários cards com informações diferentes.

4. Como funciona o `@bind-Valor` no `SeletorPeriodo`? Qual é o papel do `ValorChanged`?

  O @bind-Valor faz a ligação entre o valor selecionado no SeletorPeriodo e a variável da página. Quando o usuário muda o período, o ValorChanged é usado para avisar que o valor mudou e atualizar a informação na tela.

5. Por que os dados ficam na pasta `Data`, separados dos componentes? Que vantagem isso traz se, no futuro, os dados vierem de uma API?

   Os dados ficam na pasta Data para separar os dados da parte visual da aplicação. Isso deixa o projeto mais organizado e facilita a manutenção. No futuro, se os dados vierem de uma API, podemos trocar a fonte dos dados sem precisar modificar todos os componentes da interface.

6. Como o `MudGrid` com `xs`, `sm` e `lg` faz os cards de KPI se reorganizarem em telas de tamanhos diferentes?

   O MudGrid usa xs, sm e lg para definir quantas colunas cada card ocupa dependendo do tamanho da tela. Assim, em telas pequenas os cards ficam mais empilhados e, em telas maiores, podem ficar lado a lado.

7. Como foi possível estilizar a página inteira sem escrever CSS? Explique o papel do tema (`MudTheme`) e das classes utilitárias.

  Foi possível estilizar a página sem escrever CSS porque o MudBlazor fornece um sistema de tema e várias classes utilitárias. O MudTheme define coisas como cores, tipografia e aparência geral, enquanto as classes utilitárias ajudam a controlar espaçamento, alinhamento, tamanho e outros estilos.

8. Por que o namespace do projeto é `afya_admin` e não `afya-admin`?

  O namespace é afya_admin porque o hífen (-) não pode ser usado normalmente em nomes de namespaces do C#. O _ é permitido, por isso afya_admin é utilizado em vez de afya-admin.

## Dificuldades e soluções

1. **Pouca familiaridade com a sintaxe e com a quantidade de pastas.** O projeto tem `Components`, `Data`, `Layout`, `Pages` e `wwwroot`, e no começo eu não sabia onde cada coisa ficava nem por que `@using afya_admin.Components` e `@using afya_admin.Data` precisavam estar no `_Imports.razor`. Fui entendendo ao seguir o tutorial na ordem e ao ver o erro "The type or namespace name 'DashboardCard' could not be found" quando faltava o `@using`.

2. **Erros de fechamento de tags e de sintaxe.** Tive vários: `</MudButtom>` com "m" a mais no `Dashboard.razor`, `Color.Inf` no lugar de `Color.Info` em `DashboardData.cs`, o `</MudItem>` que sumiu na coluna do `MudProgressLinear` em `ProjetosRecentes.razor`, tags cortadas como `</MudButto` e um `fill="currentColor` sem fechar as aspas no gráfico de rosca. O Razor não compilava ou a tela saía quebrada. Resolvi lendo as mensagens do `dotnet build` e comparando linha a linha com o tutorial.

3. **Problemas com layout e mobile.** Tive alguns problemas relacionados ao layout, em especial o usuário "absoluto" e duplicado, e a adaptação para telas pequenas.

   - **Usuário duplicado e solto na tela.** Na hora de adicionar o menu do usuário (foto, nome, "Online" e o e-mail), colei o bloco `<MudDivider>` + `<MudMenu>` logo depois de `<MudLayout>` no `Layout/MainLayout.razor`, e não dentro do `<MudAppBar>`. Como o `MudLayout` espera receber a AppBar, o Drawer e o conteúdo, esse bloco ficou como filho direto do layout e foi desenhado sozinho, por cima da página. Por isso o avatar aparecia no canto do sidebar e, com o sidebar fechado, só o e-mail aparecia cortado embaixo da AppBar, além de um espaço vazio acima do título "Dashboard". Percebi pelo DevTools, na aba Elements: o `<hr class="mud-divider ...">` e o `<div class="mud-menu">` estavam como filhos de `div.mud-layout`, antes do `<header class="mud-appbar">`. Para resolver, apaguei o bloco duplicado e mantive só o menu que já estava dentro do `MudStack` da AppBar. Depois conferi com Ctrl + F que ficaram apenas dois `<MudMenu>` no arquivo: o de notificações e o do usuário.

   - **A correção não aparecia na tela.** Mesmo com o código corrigido, a página continuava igual. O terminal mostrava o erro `SocketException (10048)`, de endereço de soquete já em uso: havia um `dotnet watch` antigo ainda aberto na mesma porta, então o navegador exibia a versão velha e a nova não conseguia iniciar. Resolvi encerrando os processos `dotnet` antigos, rodando `dotnet clean`, apagando as pastas `bin` e `obj`, iniciando o `dotnet watch` de novo e recarregando o navegador com Ctrl + Shift + R.

   - **Layout no celular.** No modo celular do DevTools (Ctrl + Shift + M), os botões "Últimos 30 dias" e "Novo Projeto" ficavam cortados na lateral, porque ficavam em linha sem poder quebrar. Acrescentei `Wrap="Wrap.Wrap"` no `MudStack` dos botões em `CabecalhoPagina.razor`, para o segundo botão descer para a linha de baixo, e também no `MudStack` do título em `DashboardCard.razor`, para a legenda e o menu "⋮" não espremerem o título. No `MainLayout.razor`, troquei o espaçamento do `MudContainer` de `py-6` para `py-4 py-md-6`, para ocupar menos espaço vertical no celular. Na tabela de Projetos Recentes, troquei `Breakpoint.Sm` por `Breakpoint.Md`, para ela virar lista de cards também em telas médias, onde as 7 colunas não cabiam. Tudo isso foi feito com parâmetros e classes utilitárias do MudBlazor, sem CSS próprio.



## Melhorias futuras (opcional)

Cumpri o desafio número 3 da seção 20 do tutorial: **Período funcional**. O objetivo era fazer a troca de período no `SeletorPeriodo` alterar os valores dos KPIs, usando um dicionário de dados por período em `DashboardData`.

Como funciona:

- Em `Data/DashboardData.cs`, criei o dicionário `KpisPorPeriodo`, do tipo `Dictionary<string, List<Kpi>>`. A chave é o nome do período ("Últimos 7 dias", "Últimos 30 dias" e "Últimos 90 dias") e o valor é a lista de KPIs daquele período, com valor, variação e dados do mini gráfico. O período de 30 dias reaproveita a lista `Kpis` que já existia.
- Ainda no `DashboardData.cs`, criei o método `KpisDoPeriodo(string periodo)`, que procura o período no dicionário com `TryGetValue`. Se não encontra, como no caso de "Personalizado", devolve os dados de 30 dias.
- Em `Pages/Dashboard.razor`, o `@foreach` dos cards passou de `DashboardData.Kpis` para `DashboardData.KpisDoPeriodo(_periodo)`.
- O `SeletorPeriodo` e o `KpiCard` não precisaram mudar. O `SeletorPeriodo` usa `@bind-Valor="_periodo"`: quando escolho uma opção, ele dispara o `ValorChanged` e a página atualiza o `_periodo`. Com isso a página é renderizada de novo e o `@foreach` busca a lista do novo período. Como o `KpiCard` monta o gráfico no `OnParametersSet`, o mini gráfico também se atualiza.

Os valores de cada período são fictícios, como o resto do dashboard. O gráfico de Receita x Meta e os demais blocos ainda não mudam com o período.

O que eu implementaria a seguir:

- Criar as páginas do menu que hoje levam ao 404 (Projetos, Analytics, Clientes, Financeiro, Relatórios, Administração, Usuários, Permissões, Integrações, Configurações e Ajuda), começando por Projetos e reaproveitando `CabecalhoPagina` e `DashboardCard`.
- Fazer o breadcrumb depender da página atual com `NavigationManager`, já que hoje ele sempre mostra "Home / Dashboard".
- Fazer os outros blocos (gráficos, atividades e tabela) também responderem ao período.
- Fazer o campo "Pesquisar..." filtrar a tabela de Projetos Recentes.
- Salvar a preferência de tema claro/escuro no `localStorage` com `IJSRuntime` e detectar o tema do sistema na primeira visita.
- Mover os dados fictícios para um serviço (`IDashboardService`), para depois trocar por uma API real.