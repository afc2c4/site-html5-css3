# Explicação da estrutura HTML5 e da estilização CSS3

Neste arquivo, a ideia é ler o projeto em duas camadas:

1. **o HTML5 como estrutura** — como se fosse a planta de um ambiente;
2. **o CSS3 como decoração e acabamento** — como se um decorador estivesse escolhendo cores, espaçamentos, alinhamentos e efeitos para valorizar cada parte dessa estrutura.

A proposta abaixo segue o formato pedido: **código + explicação logo abaixo de cada bloco principal**.

---

## 1) Código HTML

```html
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mestres do Front-End | Curso HTML5 & CSS3</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;700&display=swap" rel="stylesheet">
</head>
<body>

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

    <main>
        <section class="hero" id="inicio">
            <h1>Domine o Front-End de Verdade</h1>
            <p>Aprenda a criar interfaces modernas, responsivas e animadas utilizando apenas o poder puro do HTML5 e CSS3.</p>
            <a href="#modulos" class="cta-btn">Começar Agora</a>
        </section>

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
    </main>

    <footer>
        <p>&copy; 2026 Mestres do Front-End. Feito com amor e código puro.</p>
    </footer>

</body>
</html>
```

### Explicação do HTML

#### `<!DOCTYPE html>` e `<html lang="pt-br">`
- O documento começa informando ao navegador que a página usa **HTML5**.
- Em seguida, `lang="pt-br"` avisa que o conteúdo está em português do Brasil, algo importante para acessibilidade, leitura por leitores de tela e entendimento semântico da página.

#### `<head>`
- O `<head>` concentra as configurações que preparam a página.
- `<meta charset="UTF-8">` garante o uso correto de acentos e caracteres especiais.
- `<meta name="viewport" ...>` ajuda a página a se adaptar melhor em telas menores.
- `<title>` define o nome mostrado na aba do navegador.
- O `<link>` importa a fonte **Outfit**, que depois será aplicada visualmente pelo CSS.

#### `<body>`
- O `<body>` é a área visível da página.
- Tudo o que o usuário enxerga está organizado dentro dele.

#### `<header>`
- O `<header>` funciona como o topo institucional da página.
- Ele guarda a navegação principal e serve como a entrada visual do site.

#### `<nav class="nav-container">`
- A tag `<nav>` marca semanticamente a área de navegação.
- A classe `nav-container` será usada pelo CSS para organizar logo, botão do menu mobile e lista de links.
- Ou seja: o HTML entrega a estrutura; o CSS entra depois para alinhar e distribuir os elementos.

#### `<a href="#" class="logo">HTML5.Expert</a>`
- Esse link representa a marca textual do site.
- A classe `logo` existe para que o CSS consiga dar destaque visual a esse nome.

#### `<input type="checkbox" id="menu-toggle">` + `<label for="menu-toggle" class="menu-icon">☰</label>`
- Aqui existe uma solução clássica de menu responsivo sem JavaScript.
- O `input` do tipo checkbox funciona como um interruptor invisível.
- A `label` com a classe `menu-icon` é o ícone clicável.
- Como o `for="menu-toggle"` aponta para o `id="menu-toggle"`, clicar no ícone ativa ou desativa esse checkbox.
- Depois, o CSS usa esse estado marcado para mostrar ou esconder o menu no mobile.

#### `<ul class="nav-menu">`
- A lista não ordenada agrupa os links principais do site.
- A classe `nav-menu` será a responsável por transformar essa lista em menu horizontal no desktop e em painel vertical no mobile.

#### `<main>`
- O `<main>` delimita o conteúdo principal da página.
- Isso melhora a semântica do documento e ajuda ferramentas de acessibilidade a entenderem onde está o foco central do conteúdo.

#### `<section class="hero" id="inicio">`
- A seção `hero` é o grande bloco de destaque da abertura do site.
- O `id="inicio"` permite que o menu leve o usuário diretamente para essa área.
- Dentro dela, o HTML traz três peças centrais: título, descrição e botão de ação.

#### `<h1>`, `<p>` e `<a class="cta-btn">`
- O `<h1>` é o título principal da página.
- O `<p>` complementa esse título com uma explicação curta.
- O link com classe `cta-btn` funciona como um botão visual de chamada para ação.
- Mais uma vez, o HTML só organiza os papéis; o CSS virá como acabamento para transformar esse link em botão.

#### `<section class="container" id="modulos">`
- Essa segunda seção apresenta o conteúdo do curso.
- O `id="modulos"` permite navegação por âncora a partir do menu e do botão principal.
- A classe `container` cria uma área centralizada para o conteúdo não ficar espalhado demais na largura da tela.

#### `<h2 class="section-title">`
- O `<h2>` apresenta o título da seção de módulos.
- A classe `section-title` existe para dar ao CSS um ponto específico de estilização desse subtítulo.

#### `<div class="modules-grid">`
- Essa `div` agrupa todos os cards do curso.
- A classe `modules-grid` será usada para montar um layout em grade.

#### `<div class="card">`
- Cada `card` representa um módulo do curso.
- Dentro de cada card existe um `<h3>` com o nome do módulo e um `<p>` com sua descrição.
- O HTML aqui cria repetição estrutural consistente, e isso facilita muito o trabalho do CSS.

#### `<footer>`
- O rodapé fecha a página com uma informação institucional.
- É uma área semântica própria do HTML5 para conteúdo final da página.

---

## 2) Código CSS

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

body {
    background-color: var(--bg-light);
    color: var(--text-dark);
    line-height: 1.6;
    overflow-x: hidden;
}

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

footer {
    background: var(--text-dark);
    color: white;
    padding: 4rem 2rem;
    text-align: center;
}
```

### Explicação do CSS

#### `:root`
- O `:root` funciona como a base de decisões visuais do projeto.
- Aqui o “decorador” escolhe a paleta principal, as cores de texto, a cor de fundo e até o ritmo das transições.
- As variáveis como `--primary-color` e `--text-light` ajudam a manter consistência.
- Quando outras classes usam `var(--primary-color)`, elas estão puxando o mesmo acabamento da fonte central de estilo.

#### `*`
- O seletor universal `*` atua em praticamente todos os elementos da página.
- Ele remove margens e paddings padrão do navegador e define `box-sizing: border-box`, o que deixa o cálculo visual mais previsível.
- Também aplica a fonte `'Outfit', sans-serif` em toda a interface.
- Aqui existe um efeito de herança importante: como a tipografia é aplicada de forma ampla, muitos elementos já começam com a mesma identidade visual antes mesmo de receberem regras específicas.

#### `body`
- O `body` é como o grande ambiente onde tudo acontece.
- `background-color: var(--bg-light)` pinta o fundo geral da página.
- `color: var(--text-dark)` define a cor-base do texto.
- Essa propriedade `color` costuma ser herdada por vários elementos filhos, então, quando um seletor mais específico não muda essa cor, o texto tende a seguir esse padrão escuro.
- `line-height: 1.6` cria uma leitura mais confortável.
- `overflow-x: hidden` evita rolagem horizontal acidental.

#### `header`
- O `header` recebe um tratamento de topo fixo, como se o decorador transformasse a entrada da página em uma barra elegante que acompanha o usuário.
- O fundo semitransparente com `rgba(...)` e o `backdrop-filter: blur(10px)` criam um efeito sofisticado de vidro fosco.
- `position: fixed`, `top: 0` e `width: 100%` mantêm esse bloco preso ao topo da janela.
- `z-index: 1000` garante que ele fique acima dos outros elementos.

#### `.nav-container`
- Essa classe estiliza o `<nav>` por dentro.
- O papel dela é organizar logo e menu como um decorador que distribui os itens principais em uma bancada horizontal.
- `max-width: 1200px` limita a largura máxima.
- `margin: 0 auto` centraliza o conjunto.
- `display: flex`, `justify-content: space-between` e `align-items: center` alinham os elementos em linha e equilibram os espaços entre eles.

#### `.logo`
- A classe `.logo` destaca visualmente o nome da marca.
- `font-weight: 700` e `font-size: 1.5rem` fazem a marca parecer mais forte e importante.
- `color: var(--primary-color)` usa a cor principal do projeto.
- `text-decoration: none` remove o sublinhado padrão do link, deixando o acabamento mais limpo.

#### `.nav-menu`
- A `.nav-menu` trabalha na lista de navegação como uma composição horizontal.
- `display: flex` coloca os itens lado a lado.
- `list-style: none` remove as bolinhas da lista.
- `gap: 2rem` abre um respiro equilibrado entre cada item.

#### `.nav-menu a`
- Esse seletor não estiliza toda a lista, mas especificamente os links `<a>` que estão **dentro** de `.nav-menu`.
- Aqui aparece um contexto claro de hierarquia: primeiro a lista é organizada por `.nav-menu`; depois os links internos recebem acabamento próprio.
- `color: var(--text-dark)` sobrescreve qualquer variação e reforça a cor escura nos links.
- `transition: var(--transition-smooth)` prepara o efeito suave para mudanças de estado.

#### `.nav-menu a:hover`
- Quando o usuário passa o mouse sobre o link, a cor muda para `var(--primary-color)`.
- É como se o decorador adicionasse um brilho de destaque quando o item recebe atenção.

#### `#menu-toggle`
- O `#menu-toggle` esconde o checkbox com `display: none`.
- Ele continua existindo funcionalmente, mas desaparece visualmente.
- Esse é o mecanismo técnico que sustenta o menu mobile.

#### `.menu-icon`
- A `.menu-icon` representa o ícone do menu hambúrguer.
- No estado normal ela fica escondida com `display: none`.
- `cursor: pointer` mostra ao usuário que esse elemento é clicável.

#### `.hero`
- A classe `.hero` estiliza a seção principal da página como um grande painel de apresentação.
- `padding: 180px 2rem 100px` cria bastante respiro, especialmente no topo, o que compensa o cabeçalho fixo.
- `text-align: center` centraliza o conteúdo textual interno.
- `background: linear-gradient(...)` cria um fundo suave, como se a abertura da página recebesse uma pintura em degradê mais nobre.
- `display: flex`, `flex-direction: column`, `justify-content: center` e `align-items: center` alinham título, parágrafo e botão no centro do espaço.

#### `.hero h1`
- Esse seletor atua apenas no `<h1>` que está dentro de `.hero`.
- Não é qualquer título da página: é especificamente o título do bloco principal.
- `font-size: clamp(...)` deixa o tamanho responsivo.
- `margin-bottom: 1.5rem` separa o título do parágrafo.
- `opacity: 0` e `transform: translateY(30px)` colocam o elemento inicialmente invisível e um pouco deslocado para baixo.
- `animation: fadeInUp 0.8s forwards` chama a animação que fará esse título surgir.

#### `.hero p`
- Esse seletor atua somente no parágrafo que está dentro da seção `.hero`.
- Existe aqui uma combinação de contexto e herança: o texto já nasce dentro de uma área centralizada por `.hero`, mas recebe acabamento próprio para não competir com o título.
- `font-size: 1.25rem` aumenta o texto de apoio.
- `color: var(--text-light)` quebra a herança do `body` para usar uma cor mais suave.
- `max-width: 600px` evita linhas longas demais.
- A animação recebe atraso de `0.2s`, fazendo o parágrafo aparecer logo depois do título.

#### `.section-title`
- A `.section-title` estiliza o subtítulo “O que você vai aprender”.
- `text-align: center` centraliza o texto.
- `margin: 4rem 0 3rem` cria espaço acima e abaixo, separando bem essa chamada do restante da página.

#### `.container`
- A `.container` funciona como uma moldura de conteúdo.
- Ela limita a largura da seção e centraliza os elementos internos.
- É como se o decorador dissesse: “essa parte do ambiente precisa de bordas invisíveis para o conteúdo respirar melhor”.

#### `.modules-grid`
- A `.modules-grid` é quem organiza os cards dos módulos.
- `display: grid` ativa o sistema de grade.
- `grid-template-columns: repeat(auto-fit, minmax(300px, 1fr))` faz o layout se adaptar à largura disponível.
- Isso permite que os cards se rearranjem sem quebrar a composição visual.

#### `.card`
- A classe `.card` transforma cada bloco de módulo em um cartão visual.
- `background: var(--white)` cria contraste com o fundo geral da página.
- `padding: 2.5rem` dá espaço interno.
- `border-radius: 20px` arredonda os cantos.
- `box-shadow` cria profundidade.
- `position: relative` prepara o card para receber o pseudo-elemento `::after`.
- `overflow: hidden` garante que esse detalhe decorativo não vaze para fora.

#### `.card:hover`
- Quando o card recebe hover, ele sobe levemente com `transform: translateY(-10px)`.
- A sombra cresce e a borda ganha a cor principal.
- O efeito é o de um bloco que reage ao toque visual do usuário.

#### `.card h3`
- Esse seletor atua apenas no título `<h3>` dentro de `.card`.
- De novo, não é herança pura: é um refinamento contextual.
- O título do card recebe `color: var(--primary-color)`, criando destaque interno.
- `margin-bottom: 1rem` afasta o título do texto descritivo.

#### `.card::after`
- O `::after` cria um pseudo-elemento decorativo no final do card.
- Ele funciona como uma barra inferior que inicialmente nasce com `width: 0`.
- Como `.card` está com `position: relative`, esse pseudo-elemento consegue se posicionar corretamente dentro do cartão.

#### `.card:hover::after`
- No hover, a barra se expande até `width: 100%`.
- Isso cria um acabamento animado na base do card, como um detalhe de design que só aparece quando o usuário interage.

#### `.cta-btn`
- A `.cta-btn` transforma um link simples em botão visual.
- `background`, `padding`, `border-radius` e `box-shadow` constroem a aparência de botão.
- `display: inline-block` permite que o link aceite melhor dimensões e espaçamentos.
- `font-weight: 700` reforça o tom de chamada principal.

#### `.cta-btn:hover`
- No hover, o botão troca para a cor secundária e cresce levemente com `transform: scale(1.05)`.
- A sombra também fica mais intensa.
- É um efeito de destaque para incentivar clique.

#### `@keyframes fadeInUp`
- Essa animação define o movimento de entrada dos elementos do hero.
- O estado final faz `opacity` chegar a `1` e `transform` voltar para `translateY(0)`.
- Na prática, o decorador faz o conteúdo “subir suavemente” para dentro da cena.

#### `@media (max-width: 768px)`
- Esse bloco adapta a decoração para telas menores.
- Aqui o estilo muda de acordo com o tamanho da tela, respeitando o mesmo conteúdo HTML.

#### `.menu-icon` dentro do `@media`
- Em telas menores, a `.menu-icon` passa a usar `display: block`.
- Isso faz o botão do menu aparecer apenas no mobile.

#### `.nav-menu` dentro do `@media`
- O menu deixa de ser uma linha horizontal e passa a virar um painel vertical.
- `position: absolute`, `top: 100%` e `left: -100%` colocam o menu fora da tela inicialmente.
- `flex-direction: column` reorganiza os itens em coluna.
- O CSS aqui literalmente redecorou a mesma estrutura HTML para outro contexto de uso.

#### `#menu-toggle:checked ~ .nav-menu`
- Esse seletor é um dos pontos mais interessantes do arquivo.
- Ele significa: “quando o checkbox com id `menu-toggle` estiver marcado, a `.nav-menu` irmã que vem depois dele deve mudar de posição”.
- O `~` é um combinador de irmãos, não herança.
- Com `left: 0`, o menu entra na tela.
- Ou seja, o comportamento visual mobile nasce apenas da relação entre HTML estruturado e CSS contextual.

#### `.hero` dentro do `@media`
- O `padding-top` cai para `140px`.
- Isso ajusta o espaço do topo em telas menores para evitar exagero vertical.

#### `.modules-grid` dentro do `@media`
- A grade passa para `grid-template-columns: 1fr`.
- Em outras palavras, os cards ficam em coluna única no celular.

#### `footer`
- O rodapé recebe fundo escuro e texto branco.
- Como `color: white` é aplicado no próprio `footer`, os textos internos tendem a herdar essa cor, salvo alguma sobrescrita mais específica.
- `text-align: center` centraliza o conteúdo.
- `padding: 4rem 2rem` cria uma área de fechamento confortável e bem destacada.

---

## 3) Leitura final da relação entre HTML e CSS

- O **HTML5** monta a estrutura lógica da página: topo, navegação, área principal, cards e rodapé.
- O **CSS3** entra como um decorador que estiliza essa estrutura: define cores, organiza layout, cria profundidade, anima a entrada dos elementos e adapta o conteúdo para o mobile.
- Sempre que aparece algo como `.hero h1`, `.hero p` ou `.card h3`, o CSS está mostrando que o acabamento depende do **contexto do elemento dentro da estrutura HTML**.
- Já quando vemos propriedades como `color` ou `font-family`, pode existir **herança visual**, porque filhos costumam aproveitar características definidas em elementos pais, a menos que outra regra mais específica sobrescreva esse comportamento.
