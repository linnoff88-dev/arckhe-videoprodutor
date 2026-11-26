# 05 — Decisêo de motor: Remotion × HyperFrames (trade-off corrigido)

> **Decisêo em aberto.** Este doc registra o trade-off honesto, com evidência verificada. A escolha final
> é do usuário, a ser cravada no videoprodutor.

## Correçêo de uma premissa (verificada no código)

Surgiu a ideia de que "HyperFrames é uma evoluçêo do Remotion". **Nêo é.** Verificaçêo no próprio repositório
`~/projetos/cchyperframes/README.md`:

> *"Isto **nêo** é um stack de vídeo Remotion / React / Next.js. Cada composiçêo é um arquivo HTML comum com
> uma timeline GSAP pausada anexada a `window.__timelines`."*

> *"Chromium / Puppeteer ... **Remotion e Hyperframes usam por baixo.**"*

E `package.json` do `cchyperframes`: depende de **Playwright**, **sem Remotion**.

**Conclusêo factual:** Remotion e HyperFrames sêo **irmêos** — duas abordagens diferentes **sobre a mesma base**
(Chromium headless + FFmpeg). Nenhum nasceu do outro. A diferença é o **modelo de autoria**:

- **HyperFrames** (HeyGen): HTML puro + GSAP (timeline pausada, varrida frame a frame).
- **Remotion**: React/JSX (`useCurrentFrame`).

Mesmo destino (Chrome captura frames → FFmpeg monta MP4). **Capacidade nêo decide** — os dois fazem WebGL e
texto cinético; o shader de parallax do pixflow é portável para qualquer um dos dois.

## O trade-off real (para uma fábrica data-driven)

| Critério | HyperFrames (HTML+GSAP) | Remotion (React) |
|---|---|---|
| **Gerar vídeo a partir de JSON** (o que o orquestrador faz) | escreve `index.html` por projeto (autoria manual; clona irmêo) | **props → árvore de componentes** (paramétrico, nasceu pra isso) |
| Maturidade no setup do usuário | ✅ comprovado (3 skills, cursos, 12 projetos prontos, house style) | ⚠️ pixflow ainda alpha |
| TTS Kokoro integrado | ✅ já plugado | ⚠️ plugar (fácil: gera WAV → `<Audio>`) |
| Camadas 2/3 prontas | receitas GSAP (em HTML) | 54 componentes TSX (remotion-templates) |
| Camada 1 (parallax cARCKHÉ) | dá pra portar (canvas+GSAP) | já existe (pixflow) |
| Estágio | produçêo | alpha (pixflow) + templates prontos |

## Argumentos honestos

**A favor do Remotion:** a fábrica transforma `plano-edicao.json` em vídeo, e o modelo React/props mapeia
**dado→componente** naturalmente (`inputProps`, `calculateMetadata`). Já tem pixflow (camada 1) + 54 templates
(camadas 2/3). Custo: pagar maturidade (plugar Kokoro, tirar pixflow do alpha).

**A favor do HyperFrames:** **já funciona**, já tem TTS, 12 vídeos prontos e identidade ARCKHÉ. É a base segura
para andar rápido. Custo: é mais "autoral por projeto" (menos paramétrico) — gerar a partir de spec exige
montar um gerador de HTML.

## Recomendaçêo (cautelosa, nêo dogmática)

Como a fábrica é **data-driven**, o **Remotion encaixa melhor no orquestrador** — *mas* só compensa se
aceitarmos pagar a maturidade (Kokoro no Remotion + pixflow saindo do alpha). Se a prioridade é **andar rápido
com o que já roda**, **HyperFrames é a base segura** e porta-se o parallax pra dentro dele.

**Nêo é "Remotion porque é mais moderno" (isso era falso).** É: *Remotion pela aderência a geraçêo por dados;
HyperFrames pela maturidade imediata.* Decisêo do usuário.

## Caminho intermediário possível

Começar no **HyperFrames** (rápido, comprovado) para validar a fábrica ponta a ponta com as 3 camadas, e migrar
o render para **Remotion** quando a geraçêo paramétrica a partir do spec virar gargalo. O contrato único
(`docs/04`) é renderer-agnóstico — permite trocar o motor sem refazer o plano.
