# site-html5-css3

Atue como um Engenheiro Front-End Sênior e Instrutor Especialista em Web. Este README foi reescrito como um artigo técnico e prático para que você consiga reconstruir a interface deste projeto estudando e codificando bloco por bloco, sem receber o arquivo completo de uma vez. A ideia é entender o raciocínio de engenharia por trás da página antes de decorar propriedades.

O projeto final é uma landing page autoral para um curso de HTML5 e CSS3, feita somente com HTML5 e CSS3, com foco em semântica, responsividade, transições, animações e organização visual consistente.

## Estrutura do projeto

- Arquivo HTML principal: `index.html`
- Arquivo de estilos: `styles.css`

## Como estudar este material

1. Leia um bloco por vez.
2. Copie somente o delta indicado naquele passo.
3. Salve o arquivo.
4. Abra `index.html` no navegador ou use Live Server.
5. Inspecione no DevTools exatamente o que o bloco prometeu alterar.

---

## Módulo 1: O Problema do Acoplamento (HTML vs CSS)

### 1.1. Separação de responsabilidades entre estrutura e apresentação

Antes do CSS, era comum montar páginas com tabelas para layout, `<font>` para cor e tamanho de texto e vários atributos visuais misturados ao HTML. O problema arquitetural dessa abordagem é o acoplamento: o arquivo que deveria descrever significado também passa a carregar regras visuais. Isso torna manutenção, reuso, escalabilidade e consistência muito mais caros.

Aqui, o HTML fica responsável pela semântica e pela ordem lógica do conteúdo. O CSS assume o visual, o espaçamento, a composição e a adaptação responsiva. Essa separação é o que torna possível trocar tema, ajustar layout ou depurar interface sem reescrever o documento inteiro.

**Mapeamento de arquivos**

- Criar `index.html`
- Criar `styles.css`

**Delta em `index.html`**

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<!-- AQUI: vinculamos o CSS externo para separar estrutura de apresentação -->
	<link rel="stylesheet" href="styles.css">
	<title>Curso de HTML5 e CSS3</title>
</head>
<body>
	<!-- AQUI: o HTML descreve a estrutura sem decidir cor, tamanho ou layout -->
	<h1>Curso de HTML5 e CSS3</h1>
	<p>Uma página construída com semântica e CSS desacoplado.</p>
</body>
</html>
```

**Delta em `styles.css`**

```css
/* AQUI: primeira regra CSS da página */
body {
	margin: 0;
	font-family: sans-serif;
}

/* AQUI: seletor = h1, propriedade = color, valor = #08141f */
h1 {
	color: #08141f;
}
```

**Como testar e Resultado Esperado**

Abra `index.html` no navegador. No DevTools, aba Elements, confirme que o HTML contém só estrutura e que o estilo visível do `<h1>` vem do arquivo `styles.css`, não de atributos inline nem de tags obsoletas como `<font>`.

### 1.2. Anatomia de uma regra CSS

Toda regra CSS é uma pequena unidade declarativa composta por seletor, propriedade e valor. Entender isso cedo evita decorar blocos inteiros sem compreender o mecanismo. Quando você lê `.site-header { position: sticky; }`, precisa enxergar claramente quem está sendo selecionado e qual comportamento está sendo alterado.

Esse entendimento é o que permite depurar layouts reais. Em produção, problemas quase nunca aparecem como “o CSS não funciona”. Eles aparecem como “esta regra foi sobrescrita”, “o seletor não está alcançando o nó correto” ou “a propriedade escolhida não afeta esse tipo de caixa”.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
/* seletor: .page-shell | propriedade: width | valor: min(1120px, calc(100vw - 2rem)) */
.page-shell {
	/* AQUI: limitamos a largura máxima sem quebrar a fluidez em telas menores */
	width: min(1120px, calc(100vw - 2rem));
	margin: 0 auto;
}
```

**Como testar e Resultado Esperado**

Adicione uma `<div class="page-shell">` envolvendo o conteúdo atual. Abra o DevTools, selecione a `.page-shell` e observe na aba Computed que a largura muda conforme a viewport, mas respeita o limite máximo de 1120px.

### 1.3. Importação de fonte e estratégia de fallback

Fontes web são um ponto clássico de acoplamento com a infraestrutura externa. Nem toda fonte “desejada” está disponível de forma pública e confiável, então a engenharia correta inclui fallback. Neste projeto, a pilha foi desenhada para priorizar Google Sans, depois Product Sans, e fechar com Noto Sans, que está realmente carregada via Google Fonts.

Isso resolve um problema prático: a interface preserva a intenção visual mesmo que a primeira opção não exista no sistema do usuário. Em vez de depender de uma única fonte inacessível e quebrar o refinamento tipográfico, você monta uma cadeia de degradação controlada.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<!-- AQUI: preconnect reduz o custo inicial da conexão com o servidor de fontes -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- AQUI: Noto Sans é o fallback estável carregado externamente -->
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Noto+Sans:wght@400;500;700;800&display=swap">
```

**Delta em `styles.css`**

```css
:root {
	/* AQUI: definimos a pilha tipográfica para priorizar Google Sans sem depender exclusivamente dela */
	--font-sans: "Google Sans", "Product Sans", "Noto Sans", sans-serif;
}

body {
	font-family: var(--font-sans);
}
```

**Como testar e Resultado Esperado**

Abra a aba Network do DevTools e recarregue a página. Verifique a folha de estilo da Google Fonts sendo carregada. Depois, na aba Computed do elemento `body`, confira a família tipográfica aplicada. O resultado esperado é uma tipografia limpa, geométrica e consistente.

---

## Módulo 2: A Matemática da Cascata e a Geometria da Web

### 2.1. O significado real de “Cascading”

Cascata não é um detalhe secundário; é o sistema de resolução de conflitos do CSS. Quando mais de uma regra atinge o mesmo elemento, o navegador calcula origem, importância, especificidade e ordem de declaração. O desenvolvedor que não domina isso acaba apelando para `!important`, o que normalmente apenas mascara um problema estrutural de seleção.

Neste projeto, a estratégia foi manter seletores previsíveis e de baixa complexidade. Em vez de uma guerra de especificidade, usamos classes com nomes claros, agrupamentos conscientes e ordem de escrita coerente. Isso torna o CSS sustentável ao longo do crescimento da interface.

### 2.2. Peso de seletores e por que evitar `!important`

Uma forma didática de raciocinar a especificidade é usar a régua: tag = 1, classe = 10, ID = 100 e inline = 1000. Não é a implementação exata do navegador, mas é um modelo útil para análise rápida. Se você estiliza `a` e depois `.site-nav a`, a segunda regra vence porque é mais específica.

O ganho arquitetural aqui é evitar IDs para visual e preservar margem de evolução. IDs são caros em especificidade e desnecessários para a maior parte da composição visual. Classes dão mais flexibilidade, mais reuso e menos necessidade de escalada artificial com `!important`.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<header class="site-header">
	<nav class="site-nav" aria-label="Navegação principal">
		<a href="#modulos">Módulos</a>
		<a href="#projetos">Projetos</a>
	</nav>
</header>
```

**Delta em `styles.css`**

```css
a {
	/* AQUI: estilo base para qualquer link do documento */
	color: inherit;
	text-decoration: none;
}

.site-nav a {
	/* AQUI: esta regra vence a regra genérica por maior especificidade */
	color: #bfd0e0;
	transition: color 220ms ease;
}

.site-nav a:hover {
	/* AQUI: o estado interativo altera apenas os links da navegação */
	color: #f4f7fb;
}
```

**Como testar e Resultado Esperado**

Abra o DevTools, selecione um link dentro de `.site-nav` e confira em Styles quais regras estão sendo aplicadas e quais foram sobrescritas. O esperado é ver `a { ... }` como base e `.site-nav a { ... }` refinando o comportamento sem uso de `!important`.

### 2.3. Box Model: margem, borda e preenchimento

Toda caixa renderizada na web ocupa espaço segundo o Box Model. O problema clássico aparece quando você define largura, depois adiciona padding e border, e a caixa “cresce” além do esperado. Em páginas complexas isso vira overflow lateral, desalinhamento entre cards e grids que quebram aparentemente sem motivo.

O projeto foi construído com `box-sizing: border-box` desde o início. Essa escolha muda a geometria da página inteira: padding e border passam a ser absorvidos dentro da largura declarada. É uma decisão de base que simplifica contas mentais, manutenção e previsibilidade do layout.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
* {
	/* AQUI: alteramos o box model global para que borda e padding não expandam a largura final */
	box-sizing: border-box;
}

.module-card {
	/* AQUI: esta caixa pode ter padding e borda sem quebrar sua coluna no grid */
	padding: 1.4rem;
	border: 1px solid rgba(255, 255, 255, 0.12);
}
```

**Como testar e Resultado Esperado**

Abra o navegador, selecione um card de módulo e veja o Box Model no DevTools. O resultado esperado é que padding e borda apareçam dentro da largura da coluna, sem gerar expansão lateral inesperada.

### 2.4. Variáveis CSS como sistema de design mínimo

Sem variáveis, cada ajuste de cor, raio ou sombra exige caça manual por valores espalhados. Isso aumenta inconsistência e custo de manutenção. Ao centralizar tokens em `:root`, você cria um sistema de design mínimo, ainda simples, mas suficientemente robusto para a página inteira.

Esse padrão resolve um problema de engenharia recorrente: decisões visuais repetidas em múltiplos componentes. Ao transformar cor, raio, sombra e transição em variáveis, você faz a interface responder como sistema, não como uma coleção de exceções soltas.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
:root {
	/* AQUI: tokens centrais da interface para manter consistência visual */
	--surface: rgba(255, 255, 255, 0.06);
	--text-main: #f4f7fb;
	--text-muted: #bfd0e0;
	--line: rgba(255, 255, 255, 0.12);
	--accent: #59c3c3;
	--accent-strong: #8af0df;
	--radius-md: 24px;
	--shadow-md: 0 18px 40px rgba(0, 0, 0, 0.22);
	--transition: 220ms ease;
}
```

**Como testar e Resultado Esperado**

Abra `styles.css` e altere temporariamente `--accent`. Recarregue a página. O esperado é ver múltiplos pontos da interface responderem juntos, provando que o valor está centralizado no sistema.

---

## Módulo 3: Fluxo de Documento e Posicionamento

### 3.1. Fluxo normal: block vs inline

O navegador posiciona elementos em fluxo normal antes de qualquer técnica avançada. Tags block ocupam a linha toda e empilham verticalmente; elementos inline ocupam apenas o espaço do conteúdo e coexistem na mesma linha. Entender isso evita usar posicionamento para resolver problemas que são, na verdade, de fluxo básico.

No projeto, títulos, parágrafos, seções e artigos vivem como blocos semânticos. Já links e pequenos marcadores são refinados em contextos específicos. Esse respeito ao fluxo natural reduz complexidade e permite que Flexbox e Grid sejam aplicados em cima de uma base coerente, não como correção emergencial.

**Mapeamento de arquivos**

- Editar `index.html`

**Delta em `index.html`**

```html
<section class="content-section">
	<!-- AQUI: h2 e p são blocos, então empilham naturalmente -->
	<h2>Uma progressão pensada para construir base</h2>
	<p>O conteúdo principal respeita o fluxo normal do documento.</p>

	<!-- AQUI: span é inline, ideal para pequenos rótulos dentro de um bloco maior -->
	<span class="eyebrow">Conteúdo do curso</span>
</section>
```

**Como testar e Resultado Esperado**

Inspecione os elementos no DevTools. O resultado esperado é perceber que `h2` e `p` já ocupam linhas próprias sem nenhuma regra especial, enquanto `span` não quebra linha por padrão.

### 3.2. `position: sticky` no cabeçalho

O cabeçalho precisava continuar acessível durante a rolagem sem se comportar como uma camada fixa desligada do fluxo. `position: sticky` resolve exatamente esse problema: o elemento participa do layout normalmente até atingir um limite, e então passa a “colar” no topo da viewport.

Essa solução é superior a `fixed` quando você quer preservar relação com o documento e reduzir sobreposições agressivas. No projeto, isso mantém a navegação por perto sem roubar a experiência do hero nem exigir JavaScript.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<header class="site-header">
	<div class="brand-block">
		<span class="brand-kicker">Curso intensivo</span>
		<a class="brand" href="#topo">HTML5 + CSS3</a>
	</div>
</header>
```

**Delta em `styles.css`**

```css
.site-header {
	/* AQUI: o cabeçalho acompanha o fluxo até atingir 1rem do topo da viewport */
	position: sticky;
	top: 1rem;
	z-index: 10;

	display: flex;
	justify-content: space-between;
	align-items: center;
}
```

**Como testar e Resultado Esperado**

Role a página. O esperado é que o cabeçalho permaneça visível próximo ao topo. No DevTools, verifique `position: sticky` e confirme que o deslocamento é controlado por `top: 1rem`.

### 3.3. `position: relative` e pseudo-elementos decorativos

Decorativos visuais precisam existir sem poluir o HTML com elementos vazios. Por isso, a combinação de `position: relative` no contêiner e pseudo-elementos posicionados é tão importante. Ela permite criar luz, manchas, ornamentos e sublinhados animados sem adicionar marcação desnecessária.

No hero panel, usamos isso para gerar profundidade visual. O contêiner vira a referência geométrica do pseudo-elemento, e o efeito se mantém encapsulado. Essa abordagem melhora manutenção e evita que um detalhe visual contamine a semântica do documento.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
.hero-panel {
	/* AQUI: o bloco se torna a referência local de posicionamento do pseudo-elemento */
	position: relative;
	overflow: hidden;
}

.hero-panel::before {
	content: "";

	/* AQUI: o brilho decorativo é posicionado em relação ao .hero-panel */
	position: absolute;
	inset: auto auto 1rem -2rem;
	width: 10rem;
	height: 10rem;
	border-radius: 50%;
	background: rgba(255, 179, 107, 0.2);
	filter: blur(24px);
}
```

**Como testar e Resultado Esperado**

Selecione `.hero-panel` no DevTools e ative/desative o pseudo-elemento. O esperado é ver o brilho sumir e voltar sem alterar a estrutura HTML da página.

### 3.4. `fixed`, `absolute` e `relative`: quando usar e quando evitar

`fixed` ancora o elemento na viewport; `absolute` remove do fluxo e o ancora no ancestral posicionado; `relative` mantém o elemento no fluxo, mas cria uma referência local. O erro comum é usar `absolute` para resolver layout de componentes que deveriam estar sendo organizados com Grid ou Flexbox.

Neste projeto, `absolute` aparece apenas em detalhes visuais controlados, como o `::after` dos links e o brilho decorativo. Isso é intencional. Posicionamento é ferramenta de exceção para microdetalhes, não substituto da arquitetura de layout.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
.site-nav a {
	/* AQUI: referência local para o sublinhado animado */
	position: relative;
}

.site-nav a::after {
	content: "";

	/* AQUI: absolute é adequado porque o sublinhado é um detalhe visual interno ao link */
	position: absolute;
	left: 0;
	bottom: -0.3rem;
	width: 100%;
	height: 1px;
}
```

**Como testar e Resultado Esperado**

Passe o mouse sobre os links da navegação e inspecione o pseudo-elemento. O esperado é perceber que o traço decorativo acompanha o link sem sair do seu contexto local.

### 3.5. `float` e clearfix: legado que você ainda precisa entender

Mesmo que esta interface não use `float`, um engenheiro front-end ainda precisa entender por que ele existiu e por que caiu de protagonismo. Durante muito tempo, `float` foi usado para “forçar colunas”, o que gerava hacks como clearfix e uma enorme fragilidade estrutural.

Saber isso importa porque sistemas legados ainda trazem esse padrão. Quando você encontrar `float: left` em produção, precisa reconhecer que o fluxo foi alterado, que o pai pode perder altura e que talvez o reparo correto seja encapsular, limpar ou migrar para Flexbox/Grid com critério.

**Mapeamento de arquivos**

- Este conceito é comparativo e não precisa ser incorporado ao projeto atual.

**Exemplo didático em `styles.css`**

```css
.legacy-card {
	/* AQUI: float remove o bloco do fluxo normal, prática comum em layouts antigos */
	float: left;
	width: 50%;
}

.legacy-row::after {
	content: "";

	/* AQUI: clearfix força o contêiner a voltar a reconhecer a altura dos filhos flutuados */
	display: table;
	clear: both;
}
```

**Como testar e Resultado Esperado**

Se quiser estudar o legado, crie um exemplo isolado e observe que, sem clearfix, o pai pode “colapsar” visualmente. O resultado esperado é entender por que Flexbox e Grid eliminaram boa parte dessas gambiarras.

---

## Módulo 4: O Fim das Gambiarras com Flexbox

### 4.1. O contêiner flexível e os eixos principal e transversal

Flexbox resolve um problema histórico: alinhar e distribuir elementos em uma dimensão sem recorrer a hacks. Quando você define `display: flex`, passa a trabalhar com eixo principal e eixo transversal. O desenho da interface deixa de depender de truques e passa a obedecer regras explícitas de alinhamento.

No cabeçalho, isso é essencial. Precisávamos alinhar marca, navegação e CTA em uma única linha, com espaçamento consistente e comportamento aceitável quando faltasse largura. Flexbox faz isso de forma direta e sem sobrecarregar o HTML.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<header class="site-header">
	<div class="brand-block">
		<span class="brand-kicker">Curso intensivo</span>
		<a class="brand" href="#topo">HTML5 + CSS3</a>
	</div>

	<nav class="site-nav" aria-label="Navegação principal">
		<a href="#modulos">Módulos</a>
		<a href="#projetos">Projetos</a>
		<a href="#metodo">Método</a>
		<a href="#faq">FAQ</a>
	</nav>

	<a class="header-cta" href="#inscricao">Quero aprender</a>
</header>
```

**Delta em `styles.css`**

```css
.site-header {
	display: flex;

	/* AQUI: distribui os três blocos principais ao longo do eixo principal */
	justify-content: space-between;

	/* AQUI: centraliza visualmente os itens no eixo transversal */
	align-items: center;

	gap: 1.25rem;
}

.site-nav {
	display: flex;
	flex-wrap: wrap;
	gap: 1rem;
}
```

**Como testar e Resultado Esperado**

Abra a página e redimensione horizontalmente. O esperado é que os elementos do header se mantenham alinhados, com a navegação podendo quebrar linha se necessário, sem colidir com a marca ou com o CTA.

### 4.2. Centralização histórica resolvida com `justify-content` e `align-items`

Centralizar conteúdo costumava gerar tabelas, margens mágicas, `line-height` forçado e hacks inconsistentes. Flexbox elimina isso ao permitir que a centralização seja declarada de forma explícita, tanto horizontal quanto verticalmente, a partir do eixo configurado.

Neste projeto, os botões e ações do hero se beneficiam disso. O contêiner de ações organiza múltiplos links visualmente, respeitando espaçamento e sem acoplamento com larguras fixas desnecessárias.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
.hero-actions {
	display: flex;
	flex-wrap: wrap;

	/* AQUI: distribuímos os CTAs horizontalmente com espaçamento previsível */
	gap: 1rem;

	margin: 2rem 0 1.6rem;
}

.button {
	display: inline-flex;

	/* AQUI: centralização do texto dentro do próprio botão */
	align-items: center;
	justify-content: center;
}
```

**Como testar e Resultado Esperado**

Inspecione `.hero-actions` e um `.button`. O esperado é ver os CTAs alinhados como grupo e o texto de cada botão centralizado internamente, sem hacks de `line-height`.

### 4.3. Empilhamento controlado em telas menores

Responsividade não é apenas “reduzir tamanho de fonte”. Em pontos de ruptura menores, o problema real passa a ser densidade: elementos lado a lado ficam apertados e perdem clareza. Flexbox permite trocar a direção e alongar itens para preservar legibilidade.

Aqui, a estratégia foi empilhar os CTAs no mobile e fazê-los ocupar toda a largura útil. Isso melhora área de toque, leitura e previsibilidade do layout em telas estreitas.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
@media (max-width: 560px) {
	.hero-actions {
		/* AQUI: trocamos a direção para evitar botões comprimidos em telas pequenas */
		flex-direction: column;
		align-items: stretch;
	}

	.button,
	.header-cta {
		/* AQUI: ampliamos a área clicável para a largura disponível */
		width: 100%;
	}
}
```

**Como testar e Resultado Esperado**

Abra o modo responsivo do navegador e reduza a largura para algo próximo de 390px. O esperado é ver os botões empilhados, confortáveis para toque e sem quebra visual do texto.

---

## Módulo 5: Layouts de Alta Complexidade com CSS Grid

### 5.1. Por que Grid para o macro-layout da página

Flexbox é excelente para alinhar itens em uma dimensão, mas o hero desta interface exigia duas colunas com pesos diferentes: conteúdo textual de um lado e painel visual do outro. Esse é um problema bidimensional e de macro-layout. CSS Grid resolve isso com menos atrito conceitual e mais previsibilidade geométrica.

Ao usar Grid no hero, a arquitetura do bloco fica explícita. A página ganha uma composição assimétrica controlada, sem recorrer a larguras mágicas, floats ou posicionamentos invasivos. Isso facilita muito a manutenção quando o layout precisa colapsar para tablet e mobile.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<section class="hero section-grid">
	<div class="hero-copy">
		<p class="eyebrow">Do primeiro elemento ao layout responsivo</p>
		<h1>Aprenda a criar sites em HTML5 e CSS3 com base sólida.</h1>
	</div>

	<div class="hero-panel">
		<div class="panel-card panel-card-main">
			<span class="panel-label">Trilha principal</span>
			<strong>12 aulas</strong>
		</div>
	</div>
</section>
```

**Delta em `styles.css`**

```css
.section-grid {
	display: grid;
	gap: 1.5rem;
}

.hero {
	/* AQUI: duas colunas com pesos diferentes para texto e painel visual */
	grid-template-columns: minmax(0, 1.2fr) minmax(320px, 0.95fr);
	align-items: center;
}
```

**Como testar e Resultado Esperado**

Abra a página em largura de desktop. O esperado é ver o hero dividido em duas colunas equilibradas, com o texto respirando de um lado e o painel visual ocupando o outro sem esmagar o conteúdo.

### 5.2. Grid repetível para cards de módulos

Uma grade de cards precisa distribuir quatro blocos com consistência visual e boa adaptabilidade. Grid é mais adequado aqui porque você quer controlar número de colunas, gaps e futura redução por breakpoint sem reescrever a estrutura.

O ganho arquitetural é a previsibilidade. Você não precisa empurrar margens manualmente entre cards nem depender de largura percentual individual em cada item. O contêiner define a matemática e os filhos apenas ocupam suas células.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<section id="modulos" class="content-section">
	<div class="module-grid">
		<article class="module-card">
			<span class="card-index">01</span>
			<h3>HTML5 semântico</h3>
			<p>Tags estruturais e hierarquia de conteúdo.</p>
		</article>

		<article class="module-card">
			<span class="card-index">02</span>
			<h3>CSS3 moderno</h3>
			<p>Seletores, variáveis e sistema visual consistente.</p>
		</article>
	</div>
</section>
```

**Delta em `styles.css`**

```css
.module-grid {
	display: grid;

	/* AQUI: quatro colunas iguais para a grade principal de conteúdo */
	grid-template-columns: repeat(4, minmax(0, 1fr));
	gap: 1rem;
}

.module-card {
	border-radius: 24px;
	padding: 1.4rem;
}
```

**Como testar e Resultado Esperado**

No navegador, os cards devem aparecer em grade regular. Na aba Layout do DevTools, ative a visualização do grid e confirme as quatro colunas distribuídas com gaps uniformes.

### 5.3. Grid assimétrico na seção de projetos

Layouts interessantes raramente são todos simétricos. Na seção de projetos, usamos uma composição em que um card principal ocupa duas colunas e os demais completam a grade. Esse tipo de hierarquia visual comunica prioridade sem precisar de mais texto.

Esse é um caso clássico em que Grid supera Flexbox. O card principal não só precisa ser “maior”, ele precisa ocupar área estruturalmente diferente. Grid faz isso declarativamente com `grid-column: span 2`.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<div class="project-showcase">
	<article class="showcase-card showcase-large">
		<span>Entrega 01</span>
		<h3>Landing page institucional</h3>
		<p>Estrutura completa com ritmo visual e hierarquia tipográfica.</p>
	</article>

	<article class="showcase-card">
		<span>Entrega 02</span>
		<h3>Versão mobile refinada</h3>
		<p>Empilhamento inteligente e leitura confortável.</p>
	</article>
</div>
```

**Delta em `styles.css`**

```css
.project-showcase {
	display: grid;
	grid-template-columns: repeat(2, minmax(0, 1fr));
	gap: 1rem;
}

.showcase-large {
	/* AQUI: o card principal ocupa a largura de duas colunas do grid */
	grid-column: span 2;
	min-height: 15rem;
}
```

**Como testar e Resultado Esperado**

Abra a seção de projetos e inspecione `.showcase-large`. O esperado é que o primeiro card ocupe a largura de duas colunas, reforçando visualmente sua prioridade.

### 5.4. Responsividade com Grid: trocar a matemática, não remendar componente por componente

Uma boa responsividade não tenta “consertar” cada filho individualmente primeiro. Ela muda a matemática do contêiner. Por isso, as media queries principais deste projeto alteram `grid-template-columns` nos blocos certos e deixam os componentes herdarem a nova geometria.

Esse é o ponto que normalmente separa CSS improvisado de CSS de engenharia. Em vez de dezenas de ajustes pontuais, você redefine a malha estrutural em poucos breakpoints, com comportamento previsível.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
@media (max-width: 1080px) {
	.hero,
	.projects-section,
	.cta-section,
	.timeline,
	.module-grid,
	.testimonial-grid,
	.stats-band {
		/* AQUI: reduzimos o macro-layout para duas colunas em larguras intermediárias */
		grid-template-columns: repeat(2, minmax(0, 1fr));
	}
}

@media (max-width: 820px) {
	.hero,
	.projects-section,
	.cta-section,
	.stats-band,
	.timeline,
	.module-grid,
	.testimonial-grid,
	.project-showcase,
	.hero-highlights,
	.hero-metrics {
		/* AQUI: colapsamos para uma coluna para preservar leitura e toque */
		grid-template-columns: 1fr;
	}
}
```

**Como testar e Resultado Esperado**

Abra o modo responsivo do navegador e teste faixas próximas de 1024px, 820px e 390px. O esperado é uma transição limpa de 2 colunas para 1 coluna, sem overflow horizontal e sem cards esmagados.

### 5.5. `minmax()` e prevenção de colapso estrutural

Ao escrever `minmax(0, 1fr)`, estamos dizendo ao navegador que a coluna pode encolher até zero sem forçar overflow. Isso parece detalhe pequeno, mas resolve uma classe inteira de bugs de grid, especialmente quando conteúdos internos têm textos longos, sombras ou elementos com largura implícita.

Esse padrão aparece várias vezes no projeto porque ele evita que o navegador preserve um “mínimo automático” que pode estourar a malha. É uma proteção geométrica discreta, porém importante.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
.hero {
	/* AQUI: minmax(0, ...) previne que o conteúdo interno force overflow nas colunas */
	grid-template-columns: minmax(0, 1.2fr) minmax(320px, 0.95fr);
}

.module-grid {
	/* AQUI: cada coluna fr pode encolher com segurança sem quebrar a grade */
	grid-template-columns: repeat(4, minmax(0, 1fr));
}
```

**Como testar e Resultado Esperado**

Inspecione uma coluna no DevTools e reduza a largura da viewport. O esperado é perceber que a grade se comprime com mais previsibilidade e menor chance de overflow lateral.

---

## Módulo 6: A Ilusão das Abstrações (Tailwind e Bootstrap)

### 6.1. O que frameworks resolvem e o que eles escondem

Frameworks e bibliotecas utilitárias aceleram entrega, mas também escondem a física real do layout. Quem monta interface apenas combinando classes prontas muitas vezes não desenvolve modelo mental de cascata, especificidade, box model, fluxo, eixo flexível e malha bidimensional. Quando algo falha em produção, a abstração some e sobra o CSS puro.

Este projeto foi construído sem Bootstrap e sem Tailwind exatamente para expor a mecânica real. Você vê de onde vêm as decisões de largura, por que um grid colapsa em certo breakpoint, por que um botão ocupa toda a largura no mobile e como o sticky header continua funcionando sem JavaScript.

### 6.2. Dominar CSS puro é dominar o plano de contingência

Em times reais, abstrações falham por conflito de classes, regra herdada, token inconsistente, componente encapsulado demais ou override imprevisto. O profissional que entende CSS puro e DevTools consegue diagnosticar causa-raiz; o que depende apenas do framework costuma reagir com remendos frágeis.

O valor desta interface, como exercício, é justamente esse: ela te força a entender o que a abstração esconderia. Depois disso, usar framework vira escolha consciente, não muleta.

**Mapeamento de arquivos**

- Este módulo é conceitual e usa o projeto atual como evidência prática.

**Exemplo comparativo em `styles.css`**

```css
.button-primary {
	/* AQUI: no CSS puro, vemos explicitamente a origem do estilo visual do CTA */
	background: linear-gradient(135deg, var(--accent) 0%, var(--accent-strong) 100%);
	color: #072233;
}

.button-secondary {
	/* AQUI: fica claro por que este botão tem aparência de ação secundária */
	border-color: var(--line);
	background: rgba(255, 255, 255, 0.03);
	color: var(--text-main);
}
```

**Como testar e Resultado Esperado**

Abra o DevTools e compare os dois botões do hero. O esperado é identificar rapidamente quais propriedades tornam um CTA primário e outro secundário, sem precisar rastrear classes utilitárias geradas por terceiros.

---

## Construindo o layout real deste projeto, bloco por bloco

### Bloco A. Casca da página e fundo atmosférico

O objetivo aqui é criar uma moldura centralizada e um fundo com profundidade visual. Não é apenas estética: uma casca controlada (`.page-shell`) evita que conteúdos se espalhem demais em telas largas, enquanto o fundo com gradientes e textura discreta cria contraste suficiente para destacar as superfícies translúcidas.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<body>
	<!-- AQUI: a casca centraliza toda a aplicação visual -->
	<div class="page-shell">
		<!-- os próximos blocos serão inseridos aqui -->
	</div>
</body>
```

**Delta em `styles.css`**

```css
body {
	margin: 0;
	min-height: 100vh;
	font-family: var(--font-sans);
	color: var(--text-main);

	/* AQUI: camada de fundo com profundidade e leitura melhor para superfícies translúcidas */
	background:
		radial-gradient(circle at top left, rgba(138, 240, 223, 0.16), transparent 30%),
		radial-gradient(circle at right 20%, rgba(255, 179, 107, 0.12), transparent 24%),
		linear-gradient(180deg, #09111a 0%, #08141f 55%, #0d2031 100%);
}

body::before {
	content: "";
	position: fixed;
	inset: 0;
	pointer-events: none;

	/* AQUI: textura sutil para evitar fundo chapado demais */
	background-image:
		linear-gradient(rgba(255, 255, 255, 0.025) 1px, transparent 1px),
		linear-gradient(90deg, rgba(255, 255, 255, 0.025) 1px, transparent 1px);
	background-size: 32px 32px;
}

.page-shell {
	width: min(1120px, calc(100vw - 2rem));
	margin: 0 auto;
	padding: 1rem 0 3.5rem;
}
```

**Como testar e Resultado Esperado**

Abra a página e observe o fundo. O esperado é uma atmosfera mais sofisticada do que um único `background-color`, com a área útil centralizada pela `.page-shell`.

### Bloco B. Cabeçalho sticky com navegação e CTA

O cabeçalho resolve três problemas ao mesmo tempo: identidade, navegação e ação principal. Ele precisa permanecer acessível, mas sem parecer uma barra fixa agressiva. Por isso a combinação foi sticky, superfície translúcida e distribuição com Flexbox.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<header class="site-header">
	<div class="brand-block">
		<span class="brand-kicker">Curso intensivo</span>
		<a class="brand" href="#topo" aria-label="Ir para o topo da página">HTML5 + CSS3</a>
	</div>

	<nav class="site-nav" aria-label="Navegação principal">
		<a href="#modulos">Módulos</a>
		<a href="#projetos">Projetos</a>
		<a href="#metodo">Método</a>
		<a href="#faq">FAQ</a>
	</nav>

	<a class="header-cta" href="#inscricao">Quero aprender</a>
</header>
```

**Delta em `styles.css`**

```css
.site-header {
	position: sticky;
	top: 1rem;
	z-index: 10;
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 1.25rem;
	padding: 1rem 1.25rem;
	margin-bottom: 2.5rem;
	border: 1px solid var(--line);
	border-radius: 999px;
	background: rgba(7, 18, 28, 0.72);
	box-shadow: var(--shadow-md);
}

.brand-block {
	display: grid;
	gap: 0.2rem;
}

.site-nav {
	display: flex;
	flex-wrap: wrap;
	justify-content: center;
	gap: 1rem;
}

.header-cta {
	display: inline-flex;
	align-items: center;
	justify-content: center;
	min-height: 3rem;
	padding: 0.85rem 1.25rem;
	border-radius: 999px;
}
```

**Como testar e Resultado Esperado**

Role a página e veja o header preso no topo. No DevTools, confira que o cabeçalho continua no fluxo até atingir o limite de `top` e que navegação e CTA permanecem alinhados.

### Bloco C. Hero principal com duas colunas

Este é o coração do layout. O hero precisa apresentar valor, conduzir ação e exibir um painel visual complementar sem competir com a mensagem principal. Por isso o texto recebe mais espaço e o painel atua como contraponto visual, não como distração.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<main id="topo">
	<section class="hero section-grid">
		<div class="hero-copy reveal reveal-delay-1">
			<p class="eyebrow">Do primeiro elemento ao layout responsivo</p>
			<h1>Aprenda a criar sites em HTML5 e CSS3 com base sólida e acabamento profissional.</h1>
			<p class="hero-text">
				Um curso direto ao ponto para quem quer entender semântica, estilização moderna,
				responsividade de verdade e efeitos visuais elegantes, tudo sem depender de JavaScript.
			</p>
		</div>

		<div class="hero-panel reveal reveal-delay-2">
			<div class="panel-card panel-card-main">
				<span class="panel-label">Trilha principal</span>
				<strong>12 aulas</strong>
				<p>Estrutura, estilo, composição visual e adaptação para mobile, tablet e desktop.</p>
			</div>
		</div>
	</section>
</main>
```

**Delta em `styles.css`**

```css
.section-grid {
	display: grid;
	gap: 1.5rem;
}

.hero {
	grid-template-columns: minmax(0, 1.2fr) minmax(320px, 0.95fr);
	align-items: center;
	min-height: calc(100vh - 11rem);
	padding: 2rem 0 1.5rem;
}

.hero-copy {
	max-width: 41rem;
}

.hero h1 {
	margin: 0.75rem 0 0;
	font-size: clamp(3rem, 6vw, 5.7rem);
	letter-spacing: -0.05em;
	line-height: 0.98;
}

.hero-text {
	max-width: 36rem;
	margin: 1.25rem 0 0;
	color: var(--text-muted);
	line-height: 1.7;
}
```

**Como testar e Resultado Esperado**

Abra em desktop. O esperado é um hero amplo, com título dominante e painel complementar ao lado, sem sensação de aperto visual.

### Bloco D. CTAs, lista de destaques e estados interativos

Uma hero section sem ação clara perde capacidade de conversão. Aqui, construímos dois níveis de CTA e uma lista de benefícios que quebra a densidade do texto. As transições entram como refinamento de usabilidade, deixando os estados mais perceptíveis sem virar ruído.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<div class="hero-actions">
	<a class="button button-primary" href="#inscricao">Começar agora</a>
	<a class="button button-secondary" href="#modulos">Ver conteúdo</a>
</div>

<ul class="hero-highlights" aria-label="Destaques do curso">
	<li>HTML5 semântico e acessível</li>
	<li>CSS3 com grid, flexbox e media queries</li>
	<li>Transições, animações e estados interativos</li>
</ul>
```

**Delta em `styles.css`**

```css
.button {
	display: inline-flex;
	align-items: center;
	justify-content: center;
	min-height: 3rem;
	padding: 0.85rem 1.25rem;
	border-radius: 999px;
	border: 1px solid transparent;
	font-weight: 700;

	/* AQUI: transições suaves melhoram a percepção de interatividade */
	transition:
		transform var(--transition),
		background-color var(--transition),
		border-color var(--transition),
		color var(--transition),
		box-shadow var(--transition);
}

.button-primary {
	background: linear-gradient(135deg, var(--accent) 0%, var(--accent-strong) 100%);
	color: #072233;
}

.button-secondary {
	border-color: var(--line);
	background: rgba(255, 255, 255, 0.03);
	color: var(--text-main);
}

.button:hover,
.button:focus-visible {
	/* AQUI: deslocamento sutil indica resposta da interface ao usuário */
	transform: translateY(-2px);
}

.hero-highlights {
	display: grid;
	grid-template-columns: repeat(3, minmax(0, 1fr));
	gap: 0.85rem;
	padding: 0;
	margin: 0;
	list-style: none;
}
```

**Como testar e Resultado Esperado**

Passe o mouse sobre os botões e veja o deslocamento suave. O esperado é sentir uma resposta visual elegante, sem pulo brusco nem efeito exagerado.

### Bloco E. Painel visual com métricas e “janela de código”

O painel lateral existe para traduzir o curso em sinais visuais rápidos. Métricas, rótulos e a pseudo-janela de código criam reconhecimento imediato do tema sem exigir imagens externas nem JavaScript. Isso reduz dependência de assets e mantém a página leve.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<div class="hero-panel reveal reveal-delay-2" aria-label="Resumo visual do curso">
	<div class="panel-card panel-card-main">
		<span class="panel-label">Trilha principal</span>
		<strong>12 aulas</strong>
		<p>Estrutura, estilo, composição visual e adaptação para mobile, tablet e desktop.</p>
	</div>

	<div class="hero-metrics">
		<article class="metric-card">
			<span>Projeto final</span>
			<strong>Landing page completa</strong>
		</article>
		<article class="metric-card">
			<span>Foco prático</span>
			<strong>100% HTML5 + CSS3</strong>
		</article>
	</div>

	<div class="code-window" aria-hidden="true">
		<div class="window-top">
			<span></span>
			<span></span>
			<span></span>
		</div>
		<div class="window-body">
			<p>&lt;section class="hero"&gt;</p>
			<p class="indent">&lt;h1&gt;Curso de HTML5 e CSS3&lt;/h1&gt;</p>
			<p class="indent">&lt;p&gt;Layout moderno e responsivo&lt;/p&gt;</p>
			<p>&lt;/section&gt;</p>
		</div>
	</div>
</div>
```

**Delta em `styles.css`**

```css
.hero-panel {
	position: relative;
	overflow: hidden;
	padding: 1.3rem;
	border-radius: 32px;
	border: 1px solid var(--line);
	background:
		linear-gradient(180deg, rgba(255, 255, 255, 0.07), rgba(255, 255, 255, 0.03)),
		rgba(4, 14, 23, 0.9);
}

.hero-metrics {
	display: grid;
	grid-template-columns: repeat(2, minmax(0, 1fr));
	gap: 1rem;
	margin: 1rem 0;
}

.metric-card,
.code-window,
.panel-card {
	border-radius: 24px;
	border: 1px solid var(--line);
	background: var(--surface);
}
```

**Como testar e Resultado Esperado**

O esperado é que o lado direito do hero pareça um painel de produto, com profundidade e leitura imediata, sem sobrecarregar o layout com imagens pesadas.

### Bloco F. Faixa de estatísticas

A faixa logo após o hero funciona como compressão de valor. Em vez de mais um parágrafo explicativo, mostramos indicadores curtos que quebram a rolagem e reforçam a proposta. É um bloco útil para ritmo visual e para introduzir repetição de componentes simples.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<section class="stats-band reveal reveal-delay-2" aria-label="Indicadores do curso">
	<article>
		<strong>4</strong>
		<span>blocos de aprendizado</span>
	</article>
	<article>
		<strong>8</strong>
		<span>exercícios guiados</span>
	</article>
</section>
```

**Delta em `styles.css`**

```css
.stats-band {
	display: grid;
	grid-template-columns: repeat(4, minmax(0, 1fr));
	gap: 1rem;
	padding: 1rem;
	margin: 1rem 0 4.5rem;
	border-radius: 32px;
}

.stats-band article {
	padding: 1.15rem;
	border: 1px solid var(--line);
	border-radius: 16px;
	background: var(--surface);
}
```

**Como testar e Resultado Esperado**

Verifique que os indicadores apareçam como quatro blocos regulares no desktop e sem desalinhamento vertical. Em breakpoints menores, eles devem reorganizar sem esmagamento.

### Bloco G. Seções de conteúdo repetíveis

As seções de módulos, projetos, método e resultados compartilham lógica de espaçamento e título. Criar esse padrão reduz inconsistência e evita retrabalho. Em vez de ajustar cada seção manualmente, você define um envelope de seção e uma cabeça reutilizável.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<section id="modulos" class="content-section">
	<div class="section-heading reveal reveal-delay-1">
		<p class="eyebrow">Conteúdo do curso</p>
		<h2>Uma progressão pensada para construir base, repertório visual e confiança.</h2>
	</div>
</section>
```

**Delta em `styles.css`**

```css
.content-section {
	padding: 2.2rem 0;
}

.section-heading {
	max-width: 48rem;
	margin-bottom: 1.8rem;
}

.content-section h2 {
	margin: 0.55rem 0 0;
	font-size: clamp(2rem, 4vw, 3.6rem);
	letter-spacing: -0.05em;
}
```

**Como testar e Resultado Esperado**

As seções devem apresentar respiro consistente entre si. O esperado é sentir repetição intencional de hierarquia, não blocos montados de forma isolada.

### Bloco H. Cards de módulos, timeline e depoimentos

Esses blocos mostram como um mesmo padrão de superfície pode ser reaproveitado em componentes semanticamente distintos. O ganho aqui é reduzir variedade visual desnecessária: a hierarquia nasce do conteúdo e da malha, não de um excesso de estilos incompatíveis.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<div class="module-grid">
	<article class="module-card reveal reveal-delay-1">
		<span class="card-index">01</span>
		<h3>HTML5 semântico</h3>
		<p>Tags estruturais, hierarquia de conteúdo e boas práticas de marcação.</p>
	</article>
</div>

<div class="timeline">
	<article class="timeline-item reveal reveal-delay-1">
		<span class="timeline-step">Passo 1</span>
		<h3>Estruturar antes de decorar</h3>
		<p>Você aprende a pensar a página em blocos semânticos.</p>
	</article>
</div>

<div class="testimonial-grid">
	<blockquote class="testimonial-card reveal reveal-delay-1">
		<p>"Finalmente entendi como deixar a versão mobile organizada."</p>
		<cite>Aluno iniciante</cite>
	</blockquote>
</div>
```

**Delta em `styles.css`**

```css
.module-grid,
.timeline,
.testimonial-grid {
	display: grid;
	gap: 1rem;
}

.module-grid {
	grid-template-columns: repeat(4, minmax(0, 1fr));
}

.timeline {
	grid-template-columns: repeat(3, minmax(0, 1fr));
}

.testimonial-grid {
	grid-template-columns: repeat(3, minmax(0, 1fr));
}

.module-card,
.timeline-item,
.testimonial-card {
	padding: 1.4rem;
	border: 1px solid var(--line);
	border-radius: 24px;
	background: var(--surface);

	/* AQUI: a transição reforça interatividade sem transformar o card em brinquedo visual */
	transition: transform var(--transition), border-color var(--transition), background-color var(--transition);
}

.module-card:hover,
.timeline-item:hover,
.testimonial-card:hover {
	transform: translateY(-4px);
	border-color: rgba(138, 240, 223, 0.32);
	background: rgba(255, 255, 255, 0.08);
}
```

**Como testar e Resultado Esperado**

Passe o mouse sobre os cards e confira a elevação sutil. No mobile, confirme que o hover não é requisito para entendimento do conteúdo.

### Bloco I. FAQ sem JavaScript usando `details` e `summary`

O FAQ precisava ser interativo, mas a exigência do projeto é evitar JavaScript. `details` e `summary` resolvem isso com semântica nativa, suporte razoável e custo operacional baixo. O CSS entra para adaptar o visual do componente e indicar abertura com um ícone simples.

Essa escolha é importante do ponto de vista arquitetural: você evita construir uma interação inteira com JavaScript para algo que o HTML já sabe fazer sozinho.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<div class="faq-list">
	<details class="faq-item reveal reveal-delay-1">
		<summary>Preciso saber programar antes?</summary>
		<p>Não. O curso parte dos fundamentos e evolui até uma landing page completa.</p>
	</details>
</div>
```

**Delta em `styles.css`**

```css
.faq-list {
	display: grid;
	gap: 1rem;
}

.faq-item {
	padding: 1.4rem;
	border: 1px solid var(--line);
	border-radius: 24px;
	background: var(--surface);
}

.faq-item summary {
	cursor: pointer;
	list-style: none;
	padding-right: 2rem;
	font-size: 1.05rem;
	font-weight: 700;
	position: relative;
}

.faq-item summary::after {
	content: "+";

	/* AQUI: o sinal visual muda quando o details está aberto */
	position: absolute;
	right: 0;
	top: 50%;
	transform: translateY(-50%);
	transition: transform var(--transition);
}

.faq-item[open] summary::after {
	transform: translateY(-50%) rotate(45deg);
}
```

**Como testar e Resultado Esperado**

Clique em uma pergunta. O esperado é o conteúdo expandir sem JavaScript e o sinal `+` girar para indicar estado aberto.

### Bloco J. CTA final e fechamento da página

O CTA final retoma a promessa do hero em uma posição de alta intenção, depois que o usuário já viu conteúdo, método e FAQ. Visualmente, ele precisa parecer importante, mas sem competir com o hero. Por isso ele herda a linguagem de superfície e usa uma grade simples com texto e ação.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<section id="inscricao" class="cta-section reveal reveal-delay-2">
	<div>
		<p class="eyebrow">Pronto para começar?</p>
		<h2>Monte seu repertório em HTML5 e CSS3 com um projeto visualmente forte e responsivo.</h2>
	</div>
	<a class="button button-primary" href="mailto:curso@htmlcss.dev">Solicitar matrícula</a>
</section>

<footer class="site-footer">
	<p>Curso autoral de HTML5 e CSS3, inspirado na estrutura de landing page da referência enviada.</p>
	<a href="#topo">Voltar ao topo</a>
</footer>
```

**Delta em `styles.css`**

```css
.cta-section {
	display: grid;
	grid-template-columns: minmax(0, 1fr) auto;
	align-items: center;
	padding: 1.5rem;
	margin-top: 2rem;
	border: 1px solid var(--line);
	border-radius: 32px;
	background:
		radial-gradient(circle at left top, rgba(255, 179, 107, 0.12), transparent 28%),
		rgba(255, 255, 255, 0.05);
}

.site-footer {
	display: flex;
	align-items: center;
	justify-content: space-between;
	gap: 1rem;
	margin-top: 2.5rem;
	padding: 1.25rem 1.4rem;
	border: 1px solid var(--line);
	border-radius: 24px;
	background: var(--surface);
}
```

**Como testar e Resultado Esperado**

Desça até o final da página. O esperado é um fechamento claro, com CTA forte e rodapé simples, sem sensação de corte abrupto.

### Bloco K. Responsividade de verdade: tablet, mobile e microajustes

Boa responsividade depende de observar larguras intermediárias, não só desktop e mobile extremo. Por isso este projeto trabalha com três momentos críticos: até 1080px, até 820px e até 560px. Em cada faixa, o objetivo é reconfigurar o layout, não apenas reduzir tipografia.

O que está sendo resolvido aqui é densidade, legibilidade e área de toque. Quando a viewport encolhe, o layout precisa trocar número de colunas, liberar a navegação sticky, empilhar ações e aumentar previsibilidade do fluxo.

**Mapeamento de arquivos**

- Editar `styles.css`

**Delta em `styles.css`**

```css
@media (max-width: 1080px) {
	.site-header {
		border-radius: 2rem;
		padding: 1rem;
	}

	.hero,
	.projects-section,
	.cta-section,
	.timeline,
	.module-grid,
	.testimonial-grid,
	.stats-band {
		grid-template-columns: repeat(2, minmax(0, 1fr));
	}
}

@media (max-width: 820px) {
	.site-header {
		/* AQUI: sticky deixa de fazer sentido quando o header ocupa mais altura no mobile */
		position: static;
		flex-direction: column;
		align-items: stretch;
		border-radius: 1.5rem;
	}

	.hero,
	.projects-section,
	.cta-section,
	.stats-band,
	.timeline,
	.module-grid,
	.testimonial-grid,
	.project-showcase,
	.hero-highlights,
	.hero-metrics {
		grid-template-columns: 1fr;
	}
}

@media (max-width: 560px) {
	.hero-actions {
		flex-direction: column;
		align-items: stretch;
	}

	.button,
	.header-cta {
		width: 100%;
	}

	.window-body {
		/* AQUI: reduzimos a densidade tipográfica da pseudo-janela de código no mobile */
		font-size: 0.82rem;
	}
}
```

**Como testar e Resultado Esperado**

Teste em 1280px, 1024px, 820px, 768px, 560px e 390px. O esperado é não haver scroll horizontal, textos comprimidos nem CTAs difíceis de tocar. Inspecione grids e flex containers no DevTools para confirmar a mudança estrutural entre os breakpoints.

### Bloco L. Animações e respeito a acessibilidade com `prefers-reduced-motion`

Animação deve dar ritmo e hierarquia, não atrapalhar leitura. Aqui, a escolha foi por entradas simples de opacidade e deslocamento vertical curto. Isso produz um acabamento leve, coerente com uma landing page educacional, sem exageros visuais.

Ao mesmo tempo, é engenharia responsável respeitar usuários que preferem menos movimento. `prefers-reduced-motion` reduz quase todo o custo de animação sem exigir lógica extra em JavaScript.

**Mapeamento de arquivos**

- Editar `index.html`
- Editar `styles.css`

**Delta em `index.html`**

```html
<div class="hero-copy reveal reveal-delay-1">
	...
</div>

<div class="hero-panel reveal reveal-delay-2">
	...
</div>
```

**Delta em `styles.css`**

```css
.reveal {
	opacity: 0;
	transform: translateY(22px);

	/* AQUI: animação curta e controlada para entrada suave dos blocos */
	animation: reveal-up 0.8s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

.reveal-delay-1 {
	animation-delay: 0.1s;
}

.reveal-delay-2 {
	animation-delay: 0.22s;
}

@keyframes reveal-up {
	from {
		opacity: 0;
		transform: translateY(22px);
	}

	to {
		opacity: 1;
		transform: translateY(0);
	}
}

@media (prefers-reduced-motion: reduce) {
	*,
	*::before,
	*::after {
		/* AQUI: respeitamos usuários sensíveis a movimento reduzindo animações e transições */
		animation-duration: 0.01ms !important;
		animation-iteration-count: 1 !important;
		transition-duration: 0.01ms !important;
	}
}
```

**Como testar e Resultado Esperado**

Recarregue a página. O esperado é uma entrada sutil dos blocos. Se o navegador permitir simular `prefers-reduced-motion`, ative a opção e confirme a quase remoção das animações.

---

## Checklist final de engenharia

- O HTML carrega semântica, não aparência inline.
- O CSS está desacoplado em `styles.css`.
- A tipografia usa fallback seguro.
- `box-sizing: border-box` está ativo globalmente.
- O header usa `sticky` apenas onde faz sentido.
- Grid controla o macro-layout; Flexbox controla alinhamentos locais.
- O FAQ funciona sem JavaScript.
- As media queries reorganizam a estrutura, não apenas o texto.
- As animações respeitam `prefers-reduced-motion`.
- A página renderiza sem erros em `index.html` e `styles.css`.

## Conclusão

Se você reconstruir esta interface seguindo os blocos em ordem, vai aprender mais do que “fazer uma landing page bonita”. Vai entender separação de responsabilidades, especificidade, box model, fluxo, posicionamento, Flexbox, Grid, responsividade e o papel real das animações em uma interface moderna.

Esse é o ponto central: dominar HTML5 e CSS3 puros não é nostalgia nem purismo. É o que te permite diagnosticar layout quebrado, escalar design system e trabalhar com frameworks sem depender deles cegamente.
