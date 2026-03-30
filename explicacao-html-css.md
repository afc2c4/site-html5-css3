# Explicação intercalada do HTML5 + CSS3

Neste arquivo, a leitura foi reorganizada no formato pedido: **cada bloco segue a ordem código HTML + explicação do HTML + código CSS correspondente + explicação do CSS correspondente**. Assim, a estrutura HTML5 aparece junto da sua "decoração" em CSS, até cobrir todo o código-fonte do projeto.

---

## 1) Estrutura inicial do documento

### Código HTML

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mestres do Front-End | Curso HTML5 & CSS3</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;700&display=swap" rel="stylesheet">
</head>
```

### Explicação do HTML

- `<!DOCTYPE html>` informa ao navegador que o documento usa **HTML5**.
- `<html lang="pt-br">` define o idioma principal da página, melhorando semântica e acessibilidade.
- O `<head>` concentra as configurações que preparam a página antes da renderização visual.
- `<meta charset="UTF-8">` garante que acentos e caracteres especiais sejam exibidos corretamente.
- `<meta name="viewport" ...>` ajuda a página a se adaptar melhor em telas menores.
- `<title>` define o texto da aba do navegador.
- O `<link>` importa a fonte **Outfit**, que depois será usada pelo CSS na identidade visual do site.

### Código CSS correspondente

```css
:root {
    --primary-color: #2563eb;
    --secondary-color: #6366f1;
    --text-dark: #1e293b;
    --text-light: #64748b;
    --bg-light: #f8fafc;
    --white: #ffffff;
    --transition-smooth: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Outfit', sans-serif;
}
```

### Explicação do CSS

#### `:root`
- O `:root` funciona como a central de estilo do projeto.
- É como se o decorador definisse primeiro a paleta, os tons de texto, o fundo, a cor branca padrão e o ritmo das transições.
- As variáveis como `--primary-color` e `--bg-light` serão reaproveitadas em várias partes do site.
- Isso mantém coerência visual e facilita manutenção.

#### `*`
- O seletor universal `*` aplica uma preparação visual em praticamente todos os elementos.
- `margin: 0` e `padding: 0` removem os espaçamentos automáticos do navegador.
- `box-sizing: border-box` faz largura e altura incluírem padding e borda no cálculo, deixando o layout mais previsível.
- `font-family: 'Outfit', sans-serif` espalha a tipografia base pelo documento.
- Aqui existe um efeito amplo parecido com herança visual: muitos elementos já começam com essa fonte antes mesmo de receberem estilos mais específicos.

---

## 2) Estrutura do corpo da página

### Código HTML

```html
<body>

    <header>
        <!-- navegação -->
    </header>

    <main>
        <!-- conteúdo principal -->
    </main>

    <footer>
        <!-- rodapé -->
    </footer>

</body>
```

### Explicação do HTML

- O `<body>` é a área visível do documento.
- Tudo o que o usuário enxerga fica dentro dele.
- Dentro dessa estrutura, o HTML organiza a página em três grandes zonas semânticas:
  - `<header>` para o topo e navegação;
  - `<main>` para o conteúdo principal;
  - `<footer>` para o rodapé.
- Essa divisão facilita leitura, manutenção e acessibilidade.

### Código CSS correspondente

```css
body {
    background-color: var(--bg-light);
    color: var(--text-dark);
    line-height: 1.6;
    overflow-x: hidden;
}
```

### Explicação do CSS

- O `body` funciona como o grande ambiente da página.
- `background-color: var(--bg-light)` pinta o fundo geral com um tom claro.
- `color: var(--text-dark)` define a cor-base dos textos.
- Essa `color` pode ser herdada por muitos elementos filhos quando não existe uma regra mais específica sobrescrevendo esse valor.
- `line-height: 1.6` melhora a leitura, deixando o texto mais arejado.
- `overflow-x: hidden` evita rolagem horizontal indesejada.

---

## 3) Cabeçalho e navegação

### Código HTML

```html
<header>
    <nav class="nav-container">
        <a href="#" class="logo">HTML5.Expert</a>
        
        <input type="checkbox" id="menu-toggle">
        <label for="menu-toggle" class="menu-icon">☰</label>

        <ul class="nav-menu">
            <li><a href="#inicio">Início</a></li>
            <li><a href="#modulos">Módulos</a></li>
            <li><a href="#sobre">Sobre</a></li>
            <li><a href="#precos">Inscrição</a></li>
        </ul>
    </nav>
</header>
```

### Explicação do HTML

- O `<header>` representa o topo institucional da página.
- Dentro dele, a tag `<nav>` marca semanticamente a área de navegação principal.
- A classe `nav-container` existe para o CSS organizar internamente esse bloco.
- O link com classe `logo` representa a marca textual do site.
- O `input` com `id="menu-toggle"` é um checkbox usado como gatilho de menu mobile.
- A `label` com classe `menu-icon` aponta para esse checkbox e vira o botão clicável do menu hambúrguer.
- A lista `<ul class="nav-menu">` agrupa os links principais do site.

### Código CSS correspondente

```css
header {
    background: rgba(255, 255, 255, 0.9);
    backdrop-filter: blur(10px);
    position: fixed;
    width: 100%;
    top: 0;
    z-index: 1000;
    box-shadow: 0 2px 10px rgba(0,0,0,0.05);
}

.nav-container {
    max-width: 1200px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
}

.logo {
    font-weight: 700;
    font-size: 1.5rem;
    color: var(--primary-color);
    text-decoration: none;
}

.nav-menu {
    display: flex;
    list-style: none;
    gap: 2rem;
}

.nav-menu a {
    text-decoration: none;
    color: var(--text-dark);
    font-weight: 500;
    transition: var(--transition-smooth);
}

.nav-menu a:hover {
    color: var(--primary-color);
}

#menu-toggle {
    display: none;
}

.menu-icon {
    display: none;
    cursor: pointer;
    font-size: 1.5rem;
}
```

### Explicação do CSS

#### `header`
- O `header` recebe acabamento de barra superior fixa.
- `background: rgba(255, 255, 255, 0.9)` cria um branco semitransparente.
- `backdrop-filter: blur(10px)` adiciona o efeito de vidro fosco.
- `position: fixed`, `top: 0` e `width: 100%` prendem o cabeçalho no topo da tela.
- `z-index: 1000` garante que ele fique acima do restante da página.

#### `.nav-container`
- Essa classe decora o `<nav>` por dentro.
- `max-width: 1200px` limita a largura máxima.
- `margin: 0 auto` centraliza o bloco.
- `display: flex` coloca os filhos em linha.
- `justify-content: space-between` separa logo e menu.
- `align-items: center` alinha verticalmente os itens.
- `padding: 1rem 2rem` cria respiro interno.

#### `.logo`
- A classe `.logo` dá identidade visual à marca.
- `font-weight: 700` deixa o nome mais forte.
- `font-size: 1.5rem` aumenta sua presença.
- `color: var(--primary-color)` aplica a cor principal do projeto.
- `text-decoration: none` remove o sublinhado padrão do link.

#### `.nav-menu`
- A `.nav-menu` estiliza a lista de navegação como um menu horizontal.
- `display: flex` posiciona os itens lado a lado.
- `list-style: none` remove as bolinhas da lista.
- `gap: 2rem` cria espaço equilibrado entre os links.

#### `.nav-menu a`
- Esse seletor atua apenas nos links `<a>` que estão dentro de `.nav-menu`.
- Isso mostra contexto, não herança: o estilo vale para âncoras inseridas nesse bloco específico.
- `color: var(--text-dark)` usa a cor-base escura para os links.
- `font-weight: 500` dá firmeza ao texto do menu.
- `transition: var(--transition-smooth)` suaviza mudanças de estado.

#### `.nav-menu a:hover`
- No hover, o link troca para a cor principal.
- É um detalhe de destaque visual quando o usuário interage.

#### `#menu-toggle`
- O checkbox é escondido com `display: none`.
- Ele continua existindo funcionalmente, mas não aparece visualmente.

#### `.menu-icon`
- A `.menu-icon` representa o ícone do menu hambúrguer.
- No desktop ela começa escondida com `display: none`.
- `cursor: pointer` avisa visualmente que o ícone pode ser clicado.

---

## 4) Seção principal de abertura (hero)

### Código HTML

```html
<main>
    <section class="hero" id="inicio">
        <h1>Domine o Front-End de Verdade</h1>
        <p>Aprenda a criar interfaces modernas, responsivas e animadas utilizando apenas o poder puro do HTML5 e CSS3.</p>
        <a href="#modulos" class="cta-btn">Começar Agora</a>
    </section>
</main>
```

### Explicação do HTML

- O `<main>` delimita o conteúdo principal da página.
- Dentro dele, a seção `<section class="hero" id="inicio">` funciona como a abertura visual do site.
- O `id="inicio"` permite navegação por âncora.
- O `<h1>` é o título principal da página.
- O `<p>` reforça a proposta da seção com um texto de apoio.
- O link com classe `cta-btn` é semanticamente um link, mas visualmente será tratado como botão de chamada para ação.

### Código CSS correspondente

```css
.hero {
    padding: 180px 2rem 100px;
    text-align: center;
    background: linear-gradient(135deg, #eff6ff 0%, #ffffff 100%);
    min-height: 80vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.hero h1 {
    font-size: clamp(2.5rem, 8vw, 4rem);
    margin-bottom: 1.5rem;
    opacity: 0;
    transform: translateY(30px);
    animation: fadeInUp 0.8s forwards;
}

.hero p {
    font-size: 1.25rem;
    color: var(--text-light);
    max-width: 600px;
    margin-bottom: 2rem;
    opacity: 0;
    animation: fadeInUp 0.8s 0.2s forwards;
}

.cta-btn {
    background: var(--primary-color);
    color: white;
    padding: 1rem 2.5rem;
    border-radius: 50px;
    text-decoration: none;
    font-weight: 700;
    transition: var(--transition-smooth);
    display: inline-block;
    box-shadow: 0 10px 15px -3px rgba(37, 99, 235, 0.3);
}

.cta-btn:hover {
    background: var(--secondary-color);
    transform: scale(1.05);
    box-shadow: 0 20px 25px -5px rgba(37, 99, 235, 0.4);
}

@keyframes fadeInUp {
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
```

### Explicação do CSS

#### `.hero`
- A `.hero` transforma a seção de abertura em um grande painel de destaque.
- `padding: 180px 2rem 100px` cria espaço generoso, principalmente no topo, para compensar o cabeçalho fixo.
- `text-align: center` centraliza o conteúdo textual.
- `background: linear-gradient(...)` pinta a seção com um degradê suave.
- `display: flex`, `flex-direction: column`, `justify-content: center` e `align-items: center` organizam título, texto e botão no centro.

#### `.hero h1`
- Esse seletor atua apenas no `<h1>` dentro da `.hero`.
- Isso é contexto estrutural: o CSS não está estilizando qualquer `h1`, mas especificamente o da área principal.
- `font-size: clamp(...)` torna o título responsivo.
- `opacity: 0` e `transform: translateY(30px)` preparam a entrada animada.
- `animation: fadeInUp 0.8s forwards` aplica a animação de surgimento.

#### `.hero p`
- Esse seletor atua apenas no parágrafo dentro da hero.
- `color: var(--text-light)` quebra a herança da cor-base escura do `body` e usa um tom mais suave.
- `max-width: 600px` evita linhas longas demais.
- O atraso `0.2s` na animação faz o texto aparecer depois do título.

#### `.cta-btn`
- A `.cta-btn` pega um link comum e o decora como botão.
- `background`, `padding`, `border-radius` e `box-shadow` criam a aparência de chamada principal.
- `display: inline-block` ajuda o link a se comportar como elemento de botão.
- `font-weight: 700` reforça o destaque.

#### `.cta-btn:hover`
- No hover, o botão troca para a cor secundária e cresce levemente.
- Isso dá feedback visual de interação.

#### `@keyframes fadeInUp`
- A animação define o estado final dos elementos animados.
- `opacity: 1` faz o elemento aparecer.
- `transform: translateY(0)` devolve o conteúdo à posição normal.

---

## 5) Seção de módulos e cards

### Código HTML

```html
<section class="container" id="modulos">
    <h2 class="section-title">O que você vai aprender</h2>
    <div class="modules-grid">
        <div class="card">
            <h3>01. Semântica HTML5</h3>
            <p>Estruture sites que o Google ama. Aprenda a usar tags como header, main, section e article de forma estratégica para SEO.</p>
        </div>
        <div class="card">
            <h3>02. CSS Flexbox & Grid</h3>
            <p>Esqueça os floats. Domine os sistemas de layout mais poderosos para criar alinhamentos complexos em minutos.</p>
        </div>
        <div class="card">
            <h3>03. Design Responsivo</h3>
            <p>Técnicas de Mobile-First e Media Queries para garantir que seu site brilhe em qualquer tamanho de tela.</p>
        </div>
        <div class="card">
            <h3>04. Keyframes & Efeitos</h3>
            <p>Traga vida ao seu código com transições suaves e animações complexas que retêm a atenção do usuário.</p>
        </div>
        <div class="card">
            <h3>05. Variáveis CSS (Themes)</h3>
            <p>Aprenda a criar sistemas de cores dinâmicos e manutenção simplificada usando Custom Properties.</p>
        </div>
        <div class="card">
            <h3>06. Acessibilidade (A11y)</h3>
            <p>Crie web para todos. Entenda como o CSS e HTML trabalham juntos para garantir o acesso de usuários com deficiência.</p>
        </div>
    </div>
</section>
```

### Explicação do HTML

- A seção usa a classe `container` para centralizar o conteúdo e controlar largura.
- O `id="modulos"` permite navegação por âncora a partir do menu e do botão principal.
- O `<h2 class="section-title">` apresenta o título da seção.
- A `<div class="modules-grid">` agrupa os cards em uma área pensada para layout em grade.
- Cada `<div class="card">` representa um módulo do curso.
- Dentro de cada card, o `<h3>` traz o nome do módulo e o `<p>` mostra a descrição.
- A repetição dessa estrutura torna o HTML consistente e fácil de estilizar.

### Código CSS correspondente

```css
.section-title {
    text-align: center;
    margin: 4rem 0 3rem;
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
}

.modules-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin-bottom: 5rem;
}

.card {
    background: var(--white);
    padding: 2.5rem;
    border-radius: 20px;
    box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1);
    transition: var(--transition-smooth);
    border: 1px solid #e2e8f0;
    cursor: pointer;
    position: relative;
    overflow: hidden;
}

.card:hover {
    transform: translateY(-10px);
    box-shadow: 0 20px 25px -5px rgba(0,0,0,0.1);
    border-color: var(--primary-color);
}

.card h3 {
    margin-bottom: 1rem;
    color: var(--primary-color);
}

.card::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 4px;
    background: var(--primary-color);
    transition: width 0.6s ease;
}

.card:hover::after {
    width: 100%;
}
```

### Explicação do CSS

#### `.section-title`
- A `.section-title` centraliza o título da seção e cria um respiro vertical forte.
- Isso dá à abertura dos módulos um destaque visual claro.

#### `.container`
- A `.container` funciona como uma moldura invisível.
- `max-width: 1200px` evita que o conteúdo fique espalhado demais.
- `margin: 0 auto` centraliza a área.
- `padding: 0 2rem` impede que o conteúdo encoste nas bordas laterais.

#### `.modules-grid`
- A `.modules-grid` organiza os cards como grade.
- `display: grid` ativa o sistema de grid.
- `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))` permite que a quantidade de colunas se adapte à largura da tela.
- `gap: 2rem` cria espaçamento uniforme entre os cards.

#### `.card`
- A classe `.card` transforma cada módulo em um cartão visual.
- `background: var(--white)` destaca o card sobre o fundo claro do `body`.
- `padding: 2.5rem` cria conforto interno.
- `border-radius: 20px` arredonda os cantos.
- `box-shadow` adiciona profundidade.
- `position: relative` prepara o card para posicionar corretamente o pseudo-elemento `::after`.
- `overflow: hidden` impede que esse detalhe decorativo escape da área do card.

#### `.card:hover`
- No hover, o card sobe levemente com `translateY(-10px)`.
- A sombra aumenta e a borda ganha a cor principal.
- O efeito faz o card parecer mais vivo e interativo.

#### `.card h3`
- Esse seletor estiliza apenas o `<h3>` dentro de `.card`.
- Aqui existe contexto estrutural: o CSS refina o título do card sem afetar outros `h3` fora desse bloco.
- `color: var(--primary-color)` reforça a identidade visual.

#### `.card::after`
- O pseudo-elemento `::after` cria uma barra decorativa no rodapé do card.
- Como o card está com `position: relative`, essa barra consegue se posicionar em relação ao próprio card.
- Ela nasce com `width: 0`, ficando invisível no estado inicial.

#### `.card:hover::after`
- No hover, a barra cresce até `width: 100%`.
- Esse detalhe funciona como um acabamento animado de interação.

---

## 6) Rodapé

### Código HTML

```html
<footer>
    <p>&copy; 2026 Mestres do Front-End. Feito com amor e código puro.</p>
</footer>
```

### Explicação do HTML

- O `<footer>` fecha a página com conteúdo institucional.
- O parágrafo interno exibe a mensagem final do site.
- Semanticamente, essa é a área apropriada para encerramento do documento.

### Código CSS correspondente

```css
footer {
    background: var(--text-dark);
    color: white;
    padding: 4rem 2rem;
    text-align: center;
}
```

### Explicação do CSS

- O `footer` recebe um fundo escuro para se diferenciar do restante da página.
- `color: white` pinta o texto de branco.
- Esse valor pode ser herdado pelos elementos internos, como o `<p>`, já que não há outra cor mais específica sobrescrevendo isso dentro do rodapé.
- `padding: 4rem 2rem` cria uma área de fechamento confortável.
- `text-align: center` centraliza a mensagem.

---

## 7) Responsividade e adaptação para telas menores

### Código HTML

```html
<input type="checkbox" id="menu-toggle">
<label for="menu-toggle" class="menu-icon">☰</label>
<ul class="nav-menu">
    <li><a href="#inicio">Início</a></li>
    <li><a href="#modulos">Módulos</a></li>
    <li><a href="#sobre">Sobre</a></li>
    <li><a href="#precos">Inscrição</a></li>
</ul>

<section class="hero" id="inicio">
    <h1>Domine o Front-End de Verdade</h1>
    <p>Aprenda a criar interfaces modernas, responsivas e animadas utilizando apenas o poder puro do HTML5 e CSS3.</p>
    <a href="#modulos" class="cta-btn">Começar Agora</a>
</section>

<div class="modules-grid">
    <div class="card">...</div>
</div>
```

### Explicação do HTML

- Não existe um novo HTML exclusivo para a responsividade.
- O que acontece é que o **mesmo HTML** já criado para menu, hero e grade de módulos é reaproveitado no mobile.
- A adaptação acontece no CSS, que redecorará essas mesmas estruturas para telas menores.

### Código CSS correspondente

```css
@media (max-width: 768px) {
    .menu-icon {
        display: block;
    }

    .nav-menu {
        position: absolute;
        top: 100%;
        left: -100%;
        width: 100%;
        height: 100vh;
        background: white;
        flex-direction: column;
        align-items: center;
        padding-top: 3rem;
        transition: 0.5s ease-in-out;
    }

    #menu-toggle:checked ~ .nav-menu {
        left: 0;
    }

    .hero {
        padding-top: 140px;
    }

    .modules-grid {
        grid-template-columns: 1fr;
    }
}
```

### Explicação do CSS

#### `@media (max-width: 768px)`
- Esse bloco só entra em ação quando a tela tem até 768px de largura.
- É aqui que o decorador adapta o mesmo ambiente para celular e tablet.

#### `.menu-icon` no mobile
- A `.menu-icon` muda de `display: none` para `display: block`.
- Assim, o ícone hambúrguer passa a aparecer nas telas menores.

#### `.nav-menu` no mobile
- O menu deixa de ser horizontal e passa a funcionar como painel vertical.
- `position: absolute` e `top: 100%` posicionam o menu logo abaixo do cabeçalho.
- `left: -100%` joga o menu para fora da tela inicialmente.
- `flex-direction: column` reorganiza os links em coluna.
- `height: 100vh` amplia a área do painel.

#### `#menu-toggle:checked ~ .nav-menu`
- Esse seletor significa: quando o checkbox `#menu-toggle` estiver marcado, a `.nav-menu` irmã seguinte deve mudar.
- O `~` é combinador de irmãos, não herança.
- `left: 0` traz o menu para dentro da tela.
- Esse é o ponto em que HTML e CSS trabalham juntos para criar comportamento visual sem JavaScript.

#### `.hero` no mobile
- O `padding-top` da hero é reduzido para `140px`.
- Isso evita excesso de espaço vertical em telas menores.

#### `.modules-grid` no mobile
- A grade passa para `grid-template-columns: 1fr`.
- Na prática, os cards deixam de ocupar várias colunas e passam a ficar em coluna única.

---

## 8) Leitura final do conjunto

- O HTML5 monta a estrutura lógica: documento, corpo, cabeçalho, navegação, hero, módulos, cards e rodapé.
- O CSS3 entra como o decorador dessa estrutura: define cores, espaçamentos, alinhamentos, profundidade, animação e responsividade.
- Quando aparecem seletores como `.hero h1`, `.hero p`, `.nav-menu a` e `.card h3`, o estilo depende do **contexto do elemento dentro da estrutura HTML**.
- Quando aparecem propriedades como `color` e `font-family`, pode haver **herança visual** para os filhos, desde que nenhuma regra mais específica sobrescreva esse comportamento.
