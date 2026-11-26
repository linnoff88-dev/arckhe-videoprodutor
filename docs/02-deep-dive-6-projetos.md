# 02 — Deep-dive dos 6 projetos-fonte

Análise aprofundada de `mdd`, `fontefilm`, `promptprof`, `skill-video-plan-editor`, `remotion-templates`,
`cchyperframes`. Objetivo: o que cada um já entrega de concreto e reutilizável para a fábrica.

## Descobertas-chave

1. **`fontefilm` já é um protótipo da fábrica.** Extrai do assunto uma `direcao.md` + `panels.json` com
   `{id, seed, camera, prompt (fg/mid/bg), narr (PT-BR)}` — e **já foi aplicado nas 12 lições do Hormozi**
   (hook + 12 + CTA). Nêo é teoria; é o caminho já testado.

2. **Três contratos sêo quase o mesmo:**
   ```
   fontefilm panels.json  ≈  pixflow movie spec  ≈  (subset do) plano-edicao.json
   {id, seed, camera, prompt, narr} ↔ {id, image, camera, ...} ↔ timeline[beat]
   ```
   Faxina nº 1: **fundir num spec único** (o do vpe é o mais rico → vira a espinha).

3. **As camadas 2 e 3 já existem prontas, em Remotion.** `remotion-templates` tem **54 componentes TSX**:
   texto cinético (typewriter, glitch, char-stagger, mask-reveal, text-highlight…), ilustraçêo de tópico
   (list/stagger, count-up, bar/charts, particle-explosion, progress-steps, lower-third, spotlight-reveal…)
   e cARCKHÉ (ken-burns, parallax-pan, film-burn, vignette, whip-pan…).

4. **~70% da fábrica já existe.** O que falta é a cola (orquestrador, integrador de b-roll, compositor).

## Tabela: projeto → camadas → ativos reaproveitáveis

| Projeto | Estágio | Camadas | Ativos concretos |
|---|---|---|---|
| **mdd** | pronto | direçêo, prompt | 7 blocos (cartêo, cena, bloqueios, storyboard 8/12/16, faixa do diretor, prompt final, negativo); biblioteca de tomadas |
| **fontefilm** | protótipo | extraçêo, storyboard, prompt | `direcao.md` + `panels.json` (id/seed/camera/prompt/narr); caso Hormozi pronto |
| **promptprof** (KairoBoost) | pronto | prompt, presets | `SYSTEM-PROMPT.md` (diretor de arte) + `presets.md` (5 estilos) + `vocabulario.md` (lente/luz/cor/textura) |
| **video-plan-editor** | pronto | input, estratégia, plano | `plano-edicao.json` + base de conhecimento (11 .md) + CLI `vpe` |
| **remotion-templates** | pronto | texto cinético, ilustraçêo, cARCKHÉ | **54 componentes TSX** (text/content/cARCKHÉtic/transition/intro-outro/charts) |
| **cchyperframes** | pronto | render flat, narraçêo | motor HTML+GSAP→Chrome→FFmpeg; Kokoro TTS; 12 projetos prontos; house style |

## Base de conhecimento do vpe (`skill-video-plan-editor/knowledge/`)

- **strategy/**: `frameworks.md` (Viral5, Save the Cat, Hero, Hook-Value-CTA), `hooks.md`, `cases.md`, `formats.md` (Reels/VSL/Autoridade), `templates.md` (PAS, Tutorial Reverso), `matrix.md`, `checklist.md`.
- **camera/vocabulary.md**: 30+ movimentos (push-in, parallax, dof, mask-reveal, ken_burns, whip-pan, focus-pull, dolly, crane…). Ponte: vira **prompt** E **parâmetro de motion**.
- **storyboard.md**: direçêo de cena (conflito visual, câmera por funçêo, continuidade, freeze final).
- **prompting/**: `best-practices.md` (nota p/ Flux2-Klein), `structures.md` (Production Brief × Time-Coded Shotlist), `clip-direction.md` (prompt-final + negativo), `library.md`.
- **motion/recipes.md**: snippets **GSAP determinísticos** — push-in, parallax+DOF, mask-reveal, char-stagger, pop, count-up, bar-grow, wipe-underline, whip-pan, knockout-text, distortion. + `eases.md`, `textures.md` (grêo 35mm, halaçêo feTurbulence).
- **archetypes/**: cenas prontas (cARCKHÉtic-hero, product-glint, reveal, offering, data-rise).
- **tokens.md** (design system dark premium âmbar) + **pacing.md** (word-by-word, pattern interrupt, energia por preset).
- exemplo pronto: `examples/exemplo-viral-pao.json`.

## KairoBoost (`promptprof/kairoboost/`)

Sistema LLM-agnóstico conceito→prompt cARCKHÉtográfico. `SYSTEM-PROMPT.md` (diretor de arte), `presets.md`
(CARCKHÉtográfico, Editorial, Neon Noir, Corporate, Nostálgico — cada um mapeia lente/luz/cor/textura/modelo),
`vocabulario.md` (dicionário visual). Aplicado em `hormozi-12/PROMPT-PLANEJAMENTO.md`.

## Sobreposições entre os 6

- **Direçêo (mdd × vpe × fontefilm):** mdd = completo (7 blocos); vpe = orquestrador que **delega** direçêo ao mdd em beats generativos; fontefilm = protótipo/laboratório de metáforas. Papéis distintos, nêo competem se bem amarrados.
- **Prompt (promptprof × vpe):** vpe chama KairoBoost para refinar o `gen_prompt` de cada beat. Sem duplicar.
- **Render (remotion-templates × cchyperframes):** dois motores irmêos (ver `docs/05`).

## O que falta construir (sem equivalente)

1. **Orquestrador** (link/fonte → plano) — *fontefilm mostrou o caminho*.
2. **Integrador de b-roll** (gen_prompt → flux2-klein → assets com seed/cache) — *parcial: `genimg.mjs` do pixflow já gera*.
3. **Compositor** (plano → seleciona archetype + motion + tokens → monta a composiçêo de render) — **peça-chave nova**.
4. Acessórios: banco de assets (vozes/paletas/ícones/música), pós-produçêo, multi-formato.
