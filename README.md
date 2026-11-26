ï»¿# videoprodutor ê¢â¬â o Produtor ê°Å¸Å½Â¬

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


> **Norte:** entra um **link / assunto** ê¢â â sai o **vêÂ­deo profissional** (propaganda ou explicativo), ponta a ponta. Uma coisa sêÂ³.

Orquestrador do ecossistema de vêÂ­deo: nêÂ£o reinventa render nem geraêÂ§êÂ£o ê¢â¬â **coordena as peêÂ§as que jêÂ¡ existem**
(plano, roteiro, revisêÂ£o, voz, imagem, render) numa linha de montagem êÂºnica. Tudo roda **local, sem chave de API**.
PadrêÂ£o: PT-BR, dark premium êÂ¢mbar, 16:9 **e** 9:16, CTA ARCKHÉ AI.

ê°Å¸ââ **[Guia de uso completo ê¢â â](https://linnoff88-dev.github.io/arckhe-/guia/)**

## A skill (fonte êÂºnica)

A skill vive em **[`skills/videoprodutor/`](skills/videoprodutor/)** ê¢â¬â êÂ© a **fonte êÂºnica** do projeto.
Ela veio do repo `skill-videoprodutor`, que **serêÂ¡ aposentado**; nêÂ£o edite cêÂ³pias fora daqui.

```
skills/videoprodutor/
ê¢âÅê¢ââ¬ê¢ââ¬ SKILL.md                      # o orquestrador (v0.2.0)
ê¢âÅê¢ââ¬ê¢ââ¬ CHANGELOG.md
ê¢âÅê¢ââ¬ê¢ââ¬ references/
ê¢ââ   ê¢âÅê¢ââ¬ê¢ââ¬ revisao-texto.md          # acentuaêÂ§êÂ£o PT-BR + pronêÂºncia de inglêÂªs (tela êâ fala)
ê¢ââ   ê¢âÅê¢ââ¬ê¢ââ¬ pipeline.md               # passo a passo detalhado + dependêÂªncias
ê¢ââ   ê¢âÅê¢ââ¬ê¢ââ¬ mapa-libs-motion.md       # qual lib por tarefa (GSAP/D3/Three/Lottie/SVG)
ê¢ââ   ê¢âÅê¢ââ¬ê¢ââ¬ safe-zones.md             # layout 9:16 para redes
ê¢ââ   ê¢ââê¢ââ¬ê¢ââ¬ fallback-svg.md           # imagem padrêÂ£o, SVG fallback
ê¢ââê¢ââ¬ê¢ââ¬ scripts/
    ê¢âÅê¢ââ¬ê¢ââ¬ composition-template.mjs  # gerador das 3 camadas (auto imagemê¢â âSVG, safe zones)
    ê¢âÅê¢ââ¬ê¢ââ¬ gen-imgs.mjs              # ilustraêÂ§êÂµes no flux2-klein (seeds fixos)
    ê¢âÅê¢ââ¬ê¢ââ¬ svg-icons.mjs             # êÂ­cones SVG animados (fallback vetorial)
    ê¢âÅê¢ââ¬ê¢ââ¬ fetch-fonts.mjs           # baixa as .woff2 (Sora/Inter/JetBrains)
    ê¢ââê¢ââ¬ê¢ââ¬ assets/fonts/             # fontes jêÂ¡ baixadas
```

## As 3 camadas

1. **CARCKHÉ** ê¢â¬â fundo com profundidade: imagem (flux2-klein) com vêÂ©u + parallax/ken-burns.
2. **Texto cinêÂ©tico** ê¢â¬â nêÂºmero/têÂ­tulo/barra/êÂªnfase animados com GSAP.
3. **IlustraêÂ§êÂ£o do têÂ³pico** ê¢â¬â êÂ­cone/diagrama/contador que MOSTRA o que se narra.

## A linha de montagem

```
LINK/ASSUNTO
 ê¢â â PLANO        vpe (video-plan-editor) ê¢â â plano-edicao.json
 ê¢â â ROTEIRO      SCRIPT.md + assets/txt/sN.txt
 ê¢â â REVISêÆO      tela (PT-BR acentuado) êâ fala (inglêÂªs foneticamente)
 ê¢â â VOZ+TIMING   Kokoro pf_dora ê¢â â assets/audio/sN.wav ; ffprobe ê¢â â AUDIO[]
 ê¢â â ARTE         AUTO: servidor de imagem up ê¢â â flux2-klein ; fora ê¢â â SVG
 ê¢â â COMPOR       composition-template.mjs (3 camadas, timing do AUDIO[])
 ê¢â â VALIDAR      hyperframes lint + inspect + frames de draft
 ê¢â â RENDER       hyperframes render --quality high ê¢â â 16:9 e 9:16
```

## Estrutura do repo

| Pasta | O que êÂ© |
|---|---|
| `skills/videoprodutor/` | **a skill** ê¢â¬â fonte êÂºnica (SKILL.md + references + scripts). |
| `guia/` | pêÂ¡gina landing + guia de uso (GitHub Pages). |
| `docs/` | a anêÂ¡lise de arquitetura que originou o projeto (00ê¢â¬â09). |
| `videos/hormozi-12-dicas/` | o caso de referêÂªncia funcional de onde a skill foi destilada. |
| `experiments/remotion-ab/` | teste A/B (nêÂ­vel de cêÂ³digo) da skill `remotion-best-practices`. |
| `capa/` | capa oficial do catêÂ¡logo. |

## PrêÂ©-flight

```bash
npx hyperframes doctor                      # motor de render (Chrome+FFmpeg)
curl -s localhost:8000/health               # servidor de imagem ê¢â¬â OPCIONAL, tem fallback SVG
python3 -c "import kokoro_onnx, soundfile"  # TTS local
node -v ; ffmpeg -version | head -1 ; which vpe
```

MêÂ­nimo para um vêÂ­deo (modo SVG): Node 22+ êÂ· FFmpeg êÂ· HyperFrames êÂ· internet no render (GSAP via CDN) êÂ· Kokoro/GPU (voz).

## Documentos de arquitetura

- [`docs/00-norte-e-proposito.md`](docs/00-norte-e-proposito.md) ê¢â¬â objetivo e propêÂ³sito.
- [`docs/01-mapa-ecossistema-skills.md`](docs/01-mapa-ecossistema-skills.md) ê¢â¬â skills, motores, sobreposiêÂ§êÂµes, lacunas.
- [`docs/02-deep-dive-6-projetos.md`](docs/02-deep-dive-6-projetos.md) ê¢â¬â ativos reaproveitêÂ¡veis.
- [`docs/03-camadas-de-movimento.md`](docs/03-camadas-de-movimento.md) ê¢â¬â as 3 camadas e onde jêÂ¡ existem.
- [`docs/04-arquitetura-fabrica.md`](docs/04-arquitetura-fabrica.md) ê¢â¬â a fêÂ¡brica e o contrato êÂºnico.
- [`docs/05-decisao-motor.md`](docs/05-decisao-motor.md) ê¢â¬â Remotion êâ HyperFrames.
- [`docs/06-decisoes-pendentes-e-backlog.md`](docs/06-decisoes-pendentes-e-backlog.md) ê¢â¬â o que falta decidir/construir.
- [`docs/07-caso-pipeline-funcional.md`](docs/07-caso-pipeline-funcional.md) ê¢â¬â o caso Hormozi 12 e como repetir.
- [`docs/08-mapa-libs-motion.md`](docs/08-mapa-libs-motion.md) ê¢â¬â mapa bibliotecaê¢â âtarefa.
- [`docs/09-base-conhecimento-edicao-camera.md`](docs/09-base-conhecimento-edicao-camera.md) ê¢â¬â base de ediêÂ§êÂ£o e cêÂ¢mera.

## Estado

Skill **v0.2.0**, funcional: produz o vêÂ­deo ponta a ponta com o molde testado. Motor de render hoje: **HyperFrames**.
Backlog e decisêÂµes em aberto (motor a longo prazo, timing por palavra, voz padrêÂ£o): `docs/06`.

---

[ARCKHÉ AI](https://ARCKHÉ AI)

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>