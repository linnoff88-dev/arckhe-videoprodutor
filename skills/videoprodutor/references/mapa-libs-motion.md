# 08 — Mapa biblioteca→tarefa (o cérebro do compositor)

> Origem: análise de um material sobre **Claude Code + Remotion + bibliotecas de animaçêo web**.
> Liçêo central: o valor nêo é "usar Remotion" — é saber **qual biblioteca usar em cada tipo de conteúdo**.
> E esse mapa é **agnóstico de motor**: vale no Remotion (React) e no HyperFrames (HTML, embute qualquer lib web).
> É exatamente a lógica de seleçêo do **compositor** do videoprodutor.

## A matriz (biblioteca → quando usar)

| Biblioteca | Melhor para | Camada | Observaçêo p/ render |
|---|---|---|---|
| **GSAP** | timeline/coreografia precisa, texto cinético, reveals, stagger, easing, intros SaaS, walkthroughs | 2 (texto cinético) | usar `paused`+seek (frame-determinístico). É o que já usamos. |
| **D3** | dados viram conteúdo: gráficos animados, mapas, diagramas, dashboards, viz informativa | 3 (ilustraçêo de tópico) | "os dados sêo o conteúdo" — dar dados limpos + mensagem. Nosso chip/count-up é a versêo embriêo. |
| **Three.js** | 3D: produto girando, fly-through, câmera orbital, visualizaçêo espacial | 1 (cARCKHÉ) | **Vanilla Three.js > React-Three-Fiber** p/ render (menos abstraçêo, frame previsível). É o que o pixflow faz. |
| **Lottie** | ícone/microanimaçêo simples, onboarding, social clip, marca | 1/3 (ilustraçêo leve) | caminho mais rápido prompt→ícone limpo. **≈ nosso fallback SVG.** |
| **Framer Motion** | UI interativa: hover, drag, layout, protótipo, demo | — | **NêO serve p/ vídeo renderizado** (depende de interaçêo). Fica fora do compositor. |

## Regras de seleçêo (para o compositor)

- beat de **dado/comparaçêo/número** → D3 (ou count-up GSAP p/ casos simples).
- beat **3D/produto/espaço** → Three.js (vanilla) — camada 1 (pixflow).
- beat de **texto/ênfase/sequência** → GSAP — camada 2.
- beat de **ícone/microilustraçêo** → Lottie ou **SVG** (fallback determinístico).
- **nunca** Framer Motion p/ saída renderizada.

## Técnicas práticas (aplicáveis a qualquer motor)

1. **Motion path por imagem desenhada** — desenhar a curva numa imagem, mandar o Claude rastrear e animar por ela. Precisêo de trajetória sem descrever em palavras. (Útil no **mdd** p/ câmera/movimento.)
2. **Render com alpha** — title cards/overlays transparentes: **ProRes 4444 / PNG** (última opçêo do dropdown de formato). Sem isso o alpha é achatado. (Útil p/ exportar camadas e compor.)
3. **Remotion Skills** — `npx skills @remotion-dev/skills` injeta padrões de componente/transiçêo/spring/áudio no Claude (sobe a qualidade do `remotion-templates`).
4. **Processo** — começar simples → iterar **no mesmo chat** → conferir frames → expandir. (Já é nossa disciplina.)

## Como cai em cada projeto

| Projeto | Aplicaçêo |
|---|---|
| **videoprodutor** (compositor) | a matriz acima = a lógica de "como realizar cada beat". |
| **motor de render** | evidência pró-Remotion + determinismo; mas o mapa é agnóstico → escolhe só *onde hospedar* as libs. |
| **pixflow** (camada 1) | valida Three.js vanilla + frame-determinismo; usar alpha render p/ exportar a cena cARCKHÉ. |
| **remotion-templates** | instalar Remotion Skills; expandir categorias seguindo a matriz (D3/Three/Lottie). |
| **video-explicativo** (HyperFrames+GSAP) | GSAP/spring/start-simple já aplicam; como é HTML, pode **embutir D3/Three/Lottie** sem trocar de motor. SVG fallback = nicho do Lottie. |
| **mdd** | técnica de motion path por imagem; matriz informa o motor por tomada. |
| **promptprof/KairoBoost** | "como promptar por biblioteca" → presets de prompt (um por lib/uso). |
| **vpe** | estender `motion/recipes.md` com matriz "lib por beat" (hoje só GSAP). |
| **fontefilm** | adicionar beat tipo "viz/dados" (D3) ao contrato. |
| **ARCKHÉimg** | imagem é input/textura (camada 1); movimento é código. Confirma "imagem padrêo, SVG fallback". |
| **ARCKHÉvox/Kokoro** | áudio é área das Remotion Skills; "timing vem do áudio" já alinhado. |

## A liçêo em uma linha
O compositor que faltava ao videoprodutor ganha um **mapa pronto**: biblioteca certa por tipo de conteúdo, agnóstico de motor — D3 (dados), Three vanilla (3D), GSAP (texto/timeline), Lottie/SVG (ícone). Framer Motion fica de fora do render.
