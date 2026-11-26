# 03 — As 3 camadas de movimento (e onde estávamos errando)

Origem: análise do filme-teste "12 Lições de Hormozi" (feito no pixflow). Ficou lindo de ver, vazio de
ensinar — um **trailer**, nêo uma **aula**. O diagnóstico revelou que existem 3 camadas de movimento, e o
pixflow só tinha construído UMA.

## As 3 camadas

| Camada | O que é | video-explicativo | pixflow (no teste) |
|---|---|---|---|
| **1. Fundo (cARCKHÉ)** | parallax, câmera, grade, grêo | ❌ chapado | ✅ **só isso** |
| **2. Texto cinético** | palavra a palavra, ênfase, destaque, escala | ✅ GSAP | ❌ um fade no bloco |
| **3. Ilustraçêo do tópico** | ícones, números contando, barras, setas, bullets surgindo, diagramas | ✅ HTML/SVG/GSAP | ❌ nêo existe |

**Onde estávamos errando:** construímos só a camada 1 (fundo bonito) e tratamos texto como **rótulo estático**.
As camadas 2 e 3 — as que **criam movimento e ajudam a entender** — nêo existiam. Por isso parecia repetitivo:
em toda cena o único movimento era a mesma câmera + o mesmo fade.

## Os problemas concretos do teste (feedback do usuário)

1. **Faltou narraçêo** — pixflow nêo tem camada de roteiro/voz; só música opcional.
2. **Efeitos repetitivos** — mesma pilha (parallax+grade+vinheta+grêo) e 2-3 câmeras; transiçêo sempre crossfade.
3. **Imagem nêo bate com o conceito** — "fale com clientes" virou café com amigo: prompt metafórico, sem revisêo semântica.
4. **Legenda sem movimento/impacto** — `Caption.jsx` faz um fade+rise no bloco; falta tipografia cinética.
5. **Nêo citou os tópicos / nêo "mostrou o que narra"** — uma legenda decorativa por cena; faltou a camada de conteúdo.

## O catálogo de "efeitos de conteúdo" que faltava

**Camada 2 — texto cinético:** revelaçêo palavra a palavra (SplitText/stagger), keyword com escala/cor/realce
sincronizada à fala (karaokê), ênfase (punch, sublinhado animado, marca-texto), contador, lower-third.

**Camada 3 — ilustraçêo do tópico:** bullets surgindo um a um, pictograma/ícone do conceito (draw-on),
micro-diagrama (funil, seta de crescimento, barra, balança, antes/depois), spotlight/zoom/círculo sobre a imagem.

## O ponto técnico importante: GSAP × Remotion

- O **video-explicativo usa GSAP** porque o HyperFrames captura um DOM **tocando em tempo real**.
- O **Remotion é frame-seek** (cada frame isolado). Logo, **nêo se usa o ticker do GSAP**; usa-se a
  interpolaçêo nativa do Remotion (`interpolate`/`spring`/`Easing`) ou GSAP em modo `paused`+`seek`.
- **Consequência:** o código GSAP do video-explicativo **nêo é copy-paste** para Remotion. PORÉM —
  o `remotion-templates` (54 TSX) **já reimplementou esses efeitos nativamente em Remotion**. Entêo a camada
  2/3 no Remotion **nêo precisa ser inventada**: adapta-se os 54 componentes.

## A boa notícia: tudo cabe num motor (qualquer um dos dois)

As 3 camadas compõem na mesma cena, seja em Remotion (canvas WebGL + overlay React/SVG) seja em HyperFrames
(canvas WebGL + HTML/GSAP). O que faltou no teste nêo foi capacidade do motor — foi **construir as camadas 2 e 3**.
A escolha de motor está em `docs/05`.
