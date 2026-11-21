# videoprodutor â€” o Produtor ðŸŽ¬

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


> **Norte:** entra um **link / assunto** â†’ sai o **vÃ­deo profissional** (propaganda ou explicativo), ponta a ponta. Uma coisa sÃ³.

Orquestrador do ecossistema de vÃ­deo: nÃ£o reinventa render nem geraÃ§Ã£o â€” **coordena as peÃ§as que jÃ¡ existem**
(plano, roteiro, revisÃ£o, voz, imagem, render) numa linha de montagem Ãºnica. Tudo roda **local, sem chave de API**.
PadrÃ£o: PT-BR, dark premium Ã¢mbar, 16:9 **e** 9:16, CTA INEMA.CLUB.

ðŸ“– **[Guia de uso completo â†’](https://inematds.github.io/videoprodutor/guia/)**

## A skill (fonte Ãºnica)

A skill vive em **[`skills/videoprodutor/`](skills/videoprodutor/)** â€” Ã© a **fonte Ãºnica** do projeto.
Ela veio do repo `skill-videoprodutor`, que **serÃ¡ aposentado**; nÃ£o edite cÃ³pias fora daqui.

```
skills/videoprodutor/
â”œâ”€â”€ SKILL.md                      # o orquestrador (v0.2.0)
â”œâ”€â”€ CHANGELOG.md
â”œâ”€â”€ references/
â”‚   â”œâ”€â”€ revisao-texto.md          # acentuaÃ§Ã£o PT-BR + pronÃºncia de inglÃªs (tela Ã— fala)
â”‚   â”œâ”€â”€ pipeline.md               # passo a passo detalhado + dependÃªncias
â”‚   â”œâ”€â”€ mapa-libs-motion.md       # qual lib por tarefa (GSAP/D3/Three/Lottie/SVG)
â”‚   â”œâ”€â”€ safe-zones.md             # layout 9:16 para redes
â”‚   â””â”€â”€ fallback-svg.md           # imagem padrÃ£o, SVG fallback
â””â”€â”€ scripts/
    â”œâ”€â”€ composition-template.mjs  # gerador das 3 camadas (auto imagemâ†’SVG, safe zones)
    â”œâ”€â”€ gen-imgs.mjs              # ilustraÃ§Ãµes no flux2-klein (seeds fixos)
    â”œâ”€â”€ svg-icons.mjs             # Ã­cones SVG animados (fallback vetorial)
    â”œâ”€â”€ fetch-fonts.mjs           # baixa as .woff2 (Sora/Inter/JetBrains)
    â””â”€â”€ assets/fonts/             # fontes jÃ¡ baixadas
```

## As 3 camadas

1. **Cinema** â€” fundo com profundidade: imagem (flux2-klein) com vÃ©u + parallax/ken-burns.
2. **Texto cinÃ©tico** â€” nÃºmero/tÃ­tulo/barra/Ãªnfase animados com GSAP.
3. **IlustraÃ§Ã£o do tÃ³pico** â€” Ã­cone/diagrama/contador que MOSTRA o que se narra.

## A linha de montagem

```
LINK/ASSUNTO
 â†’ PLANO        vpe (video-plan-editor) â†’ plano-edicao.json
 â†’ ROTEIRO      SCRIPT.md + assets/txt/sN.txt
 â†’ REVISÃƒO      tela (PT-BR acentuado) Ã— fala (inglÃªs foneticamente)
 â†’ VOZ+TIMING   Kokoro pf_dora â†’ assets/audio/sN.wav ; ffprobe â†’ AUDIO[]
 â†’ ARTE         AUTO: servidor de imagem up â†’ flux2-klein ; fora â†’ SVG
 â†’ COMPOR       composition-template.mjs (3 camadas, timing do AUDIO[])
 â†’ VALIDAR      hyperframes lint + inspect + frames de draft
 â†’ RENDER       hyperframes render --quality high â†’ 16:9 e 9:16
```

## Estrutura do repo

| Pasta | O que Ã© |
|---|---|
| `skills/videoprodutor/` | **a skill** â€” fonte Ãºnica (SKILL.md + references + scripts). |
| `guia/` | pÃ¡gina landing + guia de uso (GitHub Pages). |
| `docs/` | a anÃ¡lise de arquitetura que originou o projeto (00â€“09). |
| `videos/hormozi-12-dicas/` | o caso de referÃªncia funcional de onde a skill foi destilada. |
| `experiments/remotion-ab/` | teste A/B (nÃ­vel de cÃ³digo) da skill `remotion-best-practices`. |
| `capa/` | capa oficial do catÃ¡logo. |

## PrÃ©-flight

```bash
npx hyperframes doctor                      # motor de render (Chrome+FFmpeg)
curl -s localhost:8000/health               # servidor de imagem â€” OPCIONAL, tem fallback SVG
python3 -c "import kokoro_onnx, soundfile"  # TTS local
node -v ; ffmpeg -version | head -1 ; which vpe
```

MÃ­nimo para um vÃ­deo (modo SVG): Node 22+ Â· FFmpeg Â· HyperFrames Â· internet no render (GSAP via CDN) Â· Kokoro/GPU (voz).

## Documentos de arquitetura

- [`docs/00-norte-e-proposito.md`](docs/00-norte-e-proposito.md) â€” objetivo e propÃ³sito.
- [`docs/01-mapa-ecossistema-skills.md`](docs/01-mapa-ecossistema-skills.md) â€” skills, motores, sobreposiÃ§Ãµes, lacunas.
- [`docs/02-deep-dive-6-projetos.md`](docs/02-deep-dive-6-projetos.md) â€” ativos reaproveitÃ¡veis.
- [`docs/03-camadas-de-movimento.md`](docs/03-camadas-de-movimento.md) â€” as 3 camadas e onde jÃ¡ existem.
- [`docs/04-arquitetura-fabrica.md`](docs/04-arquitetura-fabrica.md) â€” a fÃ¡brica e o contrato Ãºnico.
- [`docs/05-decisao-motor.md`](docs/05-decisao-motor.md) â€” Remotion Ã— HyperFrames.
- [`docs/06-decisoes-pendentes-e-backlog.md`](docs/06-decisoes-pendentes-e-backlog.md) â€” o que falta decidir/construir.
- [`docs/07-caso-pipeline-funcional.md`](docs/07-caso-pipeline-funcional.md) â€” o caso Hormozi 12 e como repetir.
- [`docs/08-mapa-libs-motion.md`](docs/08-mapa-libs-motion.md) â€” mapa bibliotecaâ†’tarefa.
- [`docs/09-base-conhecimento-edicao-camera.md`](docs/09-base-conhecimento-edicao-camera.md) â€” base de ediÃ§Ã£o e cÃ¢mera.

## Estado

Skill **v0.2.0**, funcional: produz o vÃ­deo ponta a ponta com o molde testado. Motor de render hoje: **HyperFrames**.
Backlog e decisÃµes em aberto (motor a longo prazo, timing por palavra, voz padrÃ£o): `docs/06`.

---

[INEMA.CLUB](https://inema.club)

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>