---
name: carrossel
description: >
  Cria carrosséis e posts visuais pra Instagram, TikTok, LinkedIn com a identidade visual da marca.
  Gera HTML estilizado + renderiza em PNG 1080x1350 via Playwright, com legenda pronta no final.
  Suporta carrossel texto puro, carrossel com imagem (escolhida na ordem banco de imagens > print > SVG > IA) e post único.
  No início de um carrossel, oferece dois modos de conteúdo: padrão (rápido, sem pesquisa) ou roteiro aprofundado via /roteiro-mac (briefing + pesquisa web).
  Use quando o usuário pedir "carrossel", "post", "conteúdo pro instagram", "criar imagem",
  "gerar foto", "post educativo", ou /carrossel.
---

# /carrossel — Carrossel e posts visuais

Skill central de criação de conteúdo visual. Pega um tema → entrega HTMLs estilizados + PNGs prontos pra postar + legenda no padrão da marca.

## Dependências

- **Identidade visual:** `identidade/design-guide.md` — LER ANTES de criar qualquer visual
- **Contexto do negócio:** `_memoria/empresa.md`
- **Tom de voz:** `_memoria/preferencias.md`
- **Roteiro aprofundado (opcional):** `/roteiro-mac` — via de conteúdo mais densa (briefing + pesquisa web), oferecida na bifurcação do Passo 1.5. Ela escreve o texto; o visual continua sendo montado aqui
- **Ordem de imagem por slide:** `Banco > Print > SVG > IA` (+ `none`) — ver Passo 3. IA nunca é plano A
- **Banco de imagens do negócio:** `identidade/banco-imagens/` — fotos reais próprias, 1ª prioridade (ver `README.md` da pasta pro índice)
- **Playwright:** pra renderizar HTML em PNG (`render.js`) **e** pra capturar print de URL (modalidade Print)
- **SVG inline:** desenhado pela própria skill — sem dependência externa, custo zero
- **OpenAI API (opcional):** última opção da ordem, só quando Banco/Print/SVG não resolvem e há chave configurada
- **Outputs vão em:** `marketing/conteudo/<tipo>-<tema>-<YYYY-MM-DD>/`

---

## Tipos de conteúdo

Ao receber um pedido, identificar qual tipo se encaixa:

### 1. CARROSSEL TEXTO PURO
- **Quando usar:** posts educacionais, dicas, listas, explicações
- **Formato:** 1080x1350 (4:5) — sempre
- **Estilo:** tipografia clean, cores da marca alternadas, sem fotos

### 2. CARROSSEL COM IMAGEM
- **Quando usar:** apresentação visual, prova (dado/tela), conceito, conteúdo aspiracional
- **Formato:** 1080x1350 (4:5)
- **Estilo:** imagem como capa com gradient overlay e/ou dentro dos slides, no padrão alternado
- **Imagem por slide:** escolher a modalidade na ordem **Banco > Print > SVG > IA** (ver Passo 3). Nem todo slide precisa de imagem — `none` (tipografia) é válido

### 3. POST ÚNICO
- **Quando usar:** frase de impacto, dado/estatística, depoimento, bastidores
- **Formato:** 1080x1350
- **Estilo:** varia conforme o conteúdo (citação, número grande, foto com overlay)

Se o tipo não estiver claro, perguntar:
> "Que tipo de conteúdo? (1) carrossel texto, (2) carrossel com foto, (3) post único"

---

## Estilo visual base

O TriunoOS tem um estilo próprio — editorial, calmo, premium. Sem clip-art, sem emoji decorativo, sem gradiente arco-íris, sem template genérico de IA. `identidade/design-guide.md` sobrescreve esses padrões; quando o design-guide for vago ou estiver em branco, usar o que tá aqui (não parar pra pedir `/instalar` — o `/carrossel` funciona com defaults bons).

### Tipografia padrão

- **Fonte:** Inter (Google Fonts), pesos 400/500/600/700/800/900
- **Título de capa:** 90-100px, weight 900, line-height 0.98, letter-spacing **-0.04em**
- **H2 (slides internos):** 60-72px, weight 800, line-height 1.04, letter-spacing **-0.035em**
- **Corpo:** 20-24px, weight 500, line-height 1.5
- **Eyebrow/kicker:** 13-16px, weight 700-800, **UPPERCASE**, letter-spacing **0.22-0.32em**, cor de destaque
- **Page counter (canto sup. dir.):** 14-16px, weight 500-600, letter-spacing 0.18em, cor muted
- **Meta/handle (@):** 15-18px, weight 600

Regra do tipo: títulos grandes com kerning **apertado** (-0.035em), eyebrows pequenos com kerning **aberto** (0.22em+). Esse contraste é o coração do estilo.

### Cores padrão (quando design-guide for vago)

Paleta sóbria: fundo dark + off-white + **UMA** cor de destaque. Nunca quatro cores brigando.

- Fundo escuro: `#0E1116` ou `#1A1A1A`
- Fundo claro alternativo: `#F5ECD7` (cream) ou `#FAFAF7`
- Texto sobre escuro: `#FAFAF7`
- Texto sobre claro: `#1A1A1A` (h2) e `#444` (corpo)
- Destaque: cor da marca (uma só)

### Elementos visuais recorrentes

- **Régua fina** (3-4px de altura, 60-80px de largura, cor de destaque) entre kicker e h2 ou como divisor
- **Logo top-left + page counter top-right** em todos os slides
- **Border-top 1px** `rgba(255,255,255,0.12)` separando rodapé do conteúdo (em slides escuros)
- **Stamps circulares** (200x200, border 3px translúcida, rotate -10deg) pra selos/datas/dados
- **Tags/pills** uppercase, padding generoso, kerning 0.2em, pra rotular categoria do slide
- Padding base: 70-100px nas laterais

### Layouts nomeados

Vocabulário de layout — cada slide tem um nome. Variar entre eles pra criar ritmo:

- **CAPA** — eyebrow + título grande + subtítulo + @handle. Fundo: foto com gradient overlay (`rgba(12,10,9,0.55)` → `rgba(12,10,9,0.85)`) OU sólido (escuro/claro/destaque)
- **SOLO** — split horizontal: foto à esquerda 50% + texto à direita 50% (kicker + h2 + régua + parágrafo)
- **DUO** — texto em cima (kicker + h2 + régua + p) + 2 fotos lado a lado embaixo (ou 1 foto larga)
- **NÚMERO** — numeral gigante (200-320px, weight 800, cor de destaque) como elemento gráfico + h2 + parágrafo de apoio
- **CITAÇÃO** — aspas grandes em watermark + frase em h2 + atribuição
- **CTA FINAL** — fundo na cor de destaque, logo centralizado, headline curta, botão/CTA, telefone/@handle

**Ritmo de slide a slide:** alternar fundo escuro ↔ claro ↔ destaque. Nunca dois slides seguidos com o mesmo fundo.

---

## Padrão do carrossel

**Estrutura base (5 a 10 slides):**
- **Slide 1:** layout `CAPA`
- **Slides internos:** usar 2-3 layouts diferentes entre `SOLO` / `DUO` / `NÚMERO` / `CITAÇÃO`
- **Slide final:** layout `CTA FINAL`

Antes de criar HTML: ler `identidade/design-guide.md`. Se estiver em branco, usar o "Estilo visual base" acima como default.

### Sequência de capas no feed (planejamento de grade)

Antes de definir a capa, considerar a **última capa publicada** pra alternar:
- claro → próxima é foto/escuro
- foto/escuro → próxima é cor da marca
- cor da marca → próxima é claro
- nunca duas capas iguais em sequência

Se o usuário não souber qual foi a última, perguntar.

### Linguagem (regra crítica)

Seguir `_memoria/preferencias.md`. Em geral: frases naturais, sem jargão de marketing, sem corporativês. O público real raramente fala "ticket médio", "performance", "B2B". Falar como ele fala.

### Legenda — sempre gerar junto

Ao terminar de renderizar os PNGs, gerar **automaticamente** a legenda do post e salvar em `legenda.md` na mesma pasta. **Não esperar o usuário pedir.** Estrutura padrão:

1. Hook (pergunta ou afirmação)
2. Contexto (1-2 frases sobre o conteúdo)
3. CTA pra arrastar ("Arraste pro lado e confere")
4. Bloco de oferta (diferenciais da empresa, contato)
5. Hashtags (10-15 — público + nicho + local se aplicável)

---

## Workflow

### Passo 1 — Entender e planejar

1. Ler `_memoria/preferencias.md` e `_memoria/empresa.md`
2. Ler `identidade/design-guide.md` pra cores, fontes e logo
3. Identificar o tipo de conteúdo (1, 2 ou 3)
4. Definir o tema e o ângulo

### Passo 1.5 — Como criar o conteúdo (bifurcação, só pra carrossel)

**Só quando o conteúdo é carrossel (tipos 1 e 2, múltiplos slides).** Pra "post único" (tipo 3), pular esta pergunta e seguir direto.

**Guarda anti-loop:** se o texto/roteiro já veio pronto (handoff do `/roteiro-mac`, ou colado pelo usuário), NÃO perguntar a bifurcação e NÃO rodar o Passo 2 — ir direto pro Passo 4 (visual).

Se for um carrossel novo (texto ainda não existe), perguntar exatamente:

> "Antes de começar, como você quer criar o conteúdo do seu carrossel?
>
> **1. Padrão (rápido)** — uso o tema, a memória do teu negócio e meu conhecimento. Menos perguntas, sai rápido.
>
> **2. Roteiro aprofundado** — mais perguntas, mais direcionamento e eu farei uma pesquisa na web para trazer dados reais e atuais sobre o tema (ou a fonte que você mandar). Demora mais, mas o conteúdo sai mais denso e direcionado.
>
> Qual?"

- **Se 1 (Padrão):** seguir pro Passo 2 (fluxo atual, sem pesquisa — tema + memória + conhecimento).
- **Se 2 (Roteiro aprofundado):** chamar a skill `/roteiro-mac`. Ela conduz o briefing, a pesquisa e escreve o roteiro completo. Ela **só libera pro visual depois que o usuário aprovar o roteiro E a quantidade de slides** (checkpoints da Fase 4/plano e Fase 5-7/roteiro da própria skill) — mesma lógica do checkpoint de aprovação do fluxo padrão. Quando o roteiro aprovado voltar, **pular o Passo 2** (texto já pronto) e ir direto pro Passo 4 (visual).

### Passo 2 — Texto

**Pular este passo se o texto já veio pronto** (via `/roteiro-mac` ou colado pelo usuário) — nesse caso ir direto pro Passo 4.

Escrever o conteúdo seguindo as regras de tom:

**Pra carrossel (5-10 slides):**
- Slide 1 (Capa): título impactante, máx 8 palavras. Oferecer 3 opções
- Slides internos: um insight por slide, frases naturais, sem bullet points
- Slide final: CTA + logo

**Pra post único:**
- Frase principal em destaque
- Contexto de apoio (se necessário)
- CTA sutil

**CHECKPOINT:** Mostrar o texto completo. Esperar aprovação antes do visual.

### Passo 3 — Imagem dos slides (quando o slide pede visual)

Nem todo slide precisa de imagem — muitos são tipografia pura (NÚMERO, CITAÇÃO, mensagem). **A árvore só roda quando o slide realmente pede um visual.** Quando pedir, escolher a modalidade nesta ordem:

**`Banco > Print > SVG > IA`** — e `none` (slide sem imagem) é sempre saída válida.

A lógica: não pague nem invente uma imagem se um ativo real ou um desenho honesto resolve. **IA nunca é o plano A.** Antes de marcar IA, descartar Banco, Print e SVG explicitamente.

#### Árvore de decisão (por slide)

1. **Já existe foto real nossa no banco que mostra isso?** (produto, equipe, você, empresa) → **Banco** (3a)
2. Senão: **existe URL/print real citável?** (dashboard, ferramenta, resultado, tela, gráfico de fonte oficial) → **Print** (3b)
3. Senão: **é interface, diagrama, mockup, funil ou chart** que dá pra representar com geometria estilizada? → **SVG** (3c)
4. Senão: **é cena, pessoa, objeto físico ou conceito abstrato** que só ilustração/foto gerada resolve? → **IA** (3d, passa pelo gate de custo)
5. Nenhum? → **none** (slide sem imagem — tipografia resolve)

Mapa rápido nos nossos layouts: capa/aspiracional/mood → Banco ou IA; prova/dado/ferramenta → Print; conceito/processo/comparativo → SVG; número/citação/mensagem → none.

#### 3a. Banco de imagens (1ª prioridade)

Antes de qualquer outra coisa, olhar o acervo real do negócio:

1. Ler o índice em `identidade/banco-imagens/README.md` pra ver o que tem no banco. Se o índice estiver vazio mas a pasta tiver imagens sem descrição, abrir as imagens pra entender o conteúdo (e aproveitar pra preencher o índice).
2. Se houver foto(s) real(is) que combina(m) com o tema/slides, **priorizar elas**. Propor ao usuário quais imagens do banco encaixam em quais slides (ex: "usei a `3.jpg` na capa e a `7.jpg` no slide do produto").
3. Copiar as imagens escolhidas do banco pra pasta do conteúdo (ex: `foto-capa.jpg`) e referenciar localmente no HTML. Não referenciar o banco por caminho relativo (evita quebra no render).

**CHECKPOINT:** Se usou foto do banco, mostrar quais e seguir.

#### 3b. Print (screenshot de tela/dado real)

Custo zero, credibilidade máxima (é a coisa de verdade). Usar pra dashboard, ferramenta, resultado, tela ou gráfico de fonte oficial.

1. Capturar a URL via Playwright headless, salvando na pasta do conteúdo (ex: `print-dashboard.png`).
2. **Validar o arquivo depois de capturar** (ex: PNG > 10 KB) pra detectar login wall, rate limit ou redirect silencioso. Se falhar, oferecer URL alternativa ou cair pra `none`.
3. Referenciar localmente no HTML, igual às outras fotos.

Depende de um script de captura (ex: `scripts/capturar-print.js`). Se não existir ainda, é o mesmo padrão do `gerar-imagem.js`: criar no primeiro uso. O Playwright já é a ferramenta de render, então dá pra reaproveitar.

#### 3c. SVG (você desenha)

Custo zero, iteração grátis, honesto. A skill escreve o SVG **inline** no HTML. Ideal pra UI, diagrama, funil, comparativo, chart.

- Geometria limpa: fills sólidos, sem gradiente complexo, raios consistentes (8-16px), strokes 2-4px
- Tipografia mínima dentro do SVG: labels curtos, **nunca parágrafo, nunca itálico**
- `viewBox` alinhado ao slot do layout (não distorcer)
- Cores e acento vindos de `identidade/design-guide.md` (mesma paleta do resto — não inventar cor nova)

#### 3d. IA (última opção — a modalidade cara, tem cerimônia)

Só quando Banco, Print e SVG foram descartados. Reservado pra cena, pessoa, objeto físico ou conceito abstrato.

**Gate de custo ANTES de gerar (obrigatório):**

1. Montar o(s) prompt(s) e mostrar pro usuário: **prompt + modelo + aspect ratio + custo médio estimado por imagem + custo total do carrossel**.
2. Esperar **"ok" explícito**. Nesse momento o usuário pode aprovar OU pedir pra trocar de provedor se achar caro. Encadear gerações sem aprovação é violação.

**Referência de custo (CONFIRMAR o preço vigente em https://openai.com/api/pricing antes da 1ª geração — a OpenAI migrou pra cobrança por token nos modelos gpt-image; os valores abaixo são referência editável):**

| Modelo / tamanho | Custo aprox. por imagem |
|---|---|
| DALL-E 3 — 1024x1024 (standard) | ~US$ 0,04 *(confirmar)* |
| DALL-E 3 — 1024x1792 retrato (standard) | ~US$ 0,08 *(confirmar)* |
| gpt-image (cobrança por token) | varia — calcular no link |

**Gerar (depois do "ok"):**

1. Prompt em inglês, **denso (80-180 palavras)**: sujeito + composição + cenário + iluminação + paleta + materiais + mood.
2. **Negative inline no próprio prompt** (muitos modelos ignoram o campo `negative_prompt` separado).
3. **Aspect ratio pelo parâmetro do modelo**, não por pixels.
4. **Sujeito consistente entre slides:** repetir a descrição literal do sujeito em cada prompt (os modelos não conservam identidade entre chamadas). Vale só pra **sujeitos/objetos/cenas NÃO identificáveis** — nunca gerar rosto/pessoa identificável.
5. Gerar via script (se `scripts/gerar-imagem.js` existir):
```bash
node --env-file=.env scripts/gerar-imagem.js "PROMPT" "marketing/conteudo/<pasta>/foto-<nome>.png"
```
Se não tiver o script ainda, configurar `OPENAI_API_KEY` no `.env` e criar no primeiro uso.

**CSS-antes-de-regen:** se o problema é de container (crop, borda, posição, `object-fit`, sombra, escala), resolver no CSS e re-exportar — **não regerar a imagem** (regerar custa de novo). Só regerar se o conteúdo da imagem em si estiver errado.

6. Mostrar a foto pro usuário.

**CHECKPOINT:** Foto aprovada → seguir. Se não, ajustar (CSS ou prompt) e, se for regerar, passar pelo gate de custo de novo.

### Passo 4 — Criar visuais (HTML + PNG)

**Se o texto veio do `/roteiro-mac`:** manter o texto do roteiro **integral no slide** — NÃO condensar, NÃO cortar pra legenda. O roteiro já trabalha com 30-65 palavras por slide justamente pra caber; o que muda é o visual. **Adaptar a arte** pra acomodar esse texto: usar um layout mais texto-forward, com a tipografia numa escala que comporte 30-65 palavras com respiro (não o H2 gigante que só serve pra frase curta). Manter a identidade (paleta, logo, contador, régua) — muda a escala do texto, não a marca. A legenda continua sendo gerada à parte, não é depósito do que sobrou do slide.

1. Criar **um único `carrossel.html`** com TODOS os slides como `<div class="slide">` dentro do mesmo arquivo. Inline CSS, Google Fonts como única dependência externa. Aplicar:
   - Cores e tipografia de `identidade/design-guide.md`
   - Mínimo 2 layouts diferentes (não repetir o mesmo em todos os slides)
   - Logo top-left + slide-counter top-right em todos os slides
   - Slide final: logo + CTA, fundo na cor principal

   **Pra incluir foto/print no HTML (banco, print ou IA):**
   ```html
   <div class="slide" style="
     background-image: linear-gradient(rgba(0,0,0,0.55), rgba(0,0,0,0.7)), url('foto-xxx.png');
     background-size: cover;
     background-position: center;
   ">
     <div class="content">
       <h2>Texto sobre a foto</h2>
     </div>
   </div>
   ```

   **Pra SVG:** escrever o `<svg>` **inline** dentro do `.slide` (não é background) — geometria limpa, cores do design-guide, `viewBox` no slot do layout.

2. Criar `render.js` na mesma pasta — script Node com Playwright que abre o HTML e tira screenshot de cada `.slide` em 1080x1350. Pode reutilizar `node_modules` de uma pasta anterior (não precisa rodar `npm install` toda vez):
```bash
NODE_PATH="<pasta-com-node_modules>/node_modules" node render.js
```

3. Mostrar slide 1, 2 e o CTA final renderizados. Se aprovado, mostrar os intermediários.

### Passo 5 — Salvar e organizar

```
marketing/conteudo/<tipo>-<tema>-<YYYY-MM-DD>/
  texto.md              ← texto aprovado + legenda
  foto-<nome>.png       ← fotos usadas (copiadas do banco ou geradas por IA)
  print-<nome>.png      ← screenshots capturados de URL (se houver)
  carrossel.html
  render.js
  instagram/
    slide-01.png → slide-NN.png
  tiktok/ (se pedido — formato 9:16)
    slide-01.png → ...
  legenda.md            ← legenda Insta+FB
  legenda-linkedin.md   ← (se pedido, mais formal)
```

### Passo 6 — Conexão com blog (opcional)

Depois de criar o conteúdo visual, perguntar:

> "Esse conteúdo dá pra virar artigo no blog também. Quer que eu crie a versão blog pra SEO?"

Se sim, chamar `/publicar-tema` com o mesmo tema.

---

## Regras

- Sempre ler `identidade/design-guide.md` antes de criar qualquer visual
- Carrossel: 1080x1350 (4:5 retrato) — sempre. TikTok/Reels: 1080x1920 (9:16) — só quando pedido explicitamente
- Linguagem segue `_memoria/preferencias.md` estritamente
- Sempre considerar a sequência de capa no feed antes de definir capa nova
- Sempre gerar legenda automaticamente ao final, salvando em `legenda.md`
- Imagem por slide: seguir a ordem **Banco > Print > SVG > IA** (+ `none`). IA nunca é plano A — antes de marcar IA, descartar Banco, Print e SVG explicitamente
- Print: validar o arquivo após capturar (PNG > 10 KB) pra detectar login wall/redirect; senão, cair pra `none`
- SVG: geometria limpa, sem gradiente complexo, sem itálico, sem parágrafo; cores do design-guide
- IA: **gate de custo ANTES de gerar** — mostrar prompt + modelo + aspect ratio + custo estimado por imagem e esperar "ok" (aí o usuário aprova ou troca de provedor). Encadear gerações sem aprovação é violação
- IA: prompts em inglês, densos (80-180 palavras), com negative inline; aspect ratio via parâmetro do modelo
- IA: **CSS-antes-de-regen** — problema de container resolve no CSS, não regera a imagem
- IA: nunca gerar pessoas/rostos identificáveis. Consistência de sujeito entre slides vale só pra sujeitos/objetos/cenas não identificáveis
- HTMLs: um único arquivo `carrossel.html` com todos os slides + `render.js` na mesma pasta. Inline CSS
- Render: reutilizar `node_modules` quando possível (não rodar `npm install` em cada pasta)
- Não repetir layout entre slides — usar variação visual
