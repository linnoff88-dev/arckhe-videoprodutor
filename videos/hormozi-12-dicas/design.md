# House style — dark premium (padrêo do usuário)

Copie isto como `design.md` na raiz do projeto de vídeo e ajuste só se o usuário pedir outro mood.

## Paleta (dark / premium)
- `--bg`: `#0D1321` (azul-noite, nunca #000 puro)
- `--bg2`: `#1D2D44` (painéis/cards)
- `--bg3`: `#3E5C76` (bordas/divisores)
- `--fg`: `#F0EBD8` (texto, branco-creme quente)
- `--muted`: `#748CAB` (secundário)
- `--accent`: `#FFC300` (âmbar — destaque ÚNICO dominante)
- `--accent2`: `#FCA311` (âmbar quente p/ gradientes)
- `--code`: `#2EC4B6` (verde-água, só código/valores)

Regra: UM accent dominante (âmbar). Fundo idêntico em todas as cenas.

## Tipografia
- Títulos: **Sora** 700–800 (geométrica), 72–172px (16:9) / 104–118px (9:16).
- Corpo/legenda: **Inter** 400–600, 28–40px.
- Código/URL/labels: **JetBrains Mono**.
- Sempre embutir `.woff2` local (subset latin cobre PT-BR). Nunca CDN.

## Composiçêo de vídeo (nêo é web!)
- 8–10 elementos por cena; nunca fundo chapado.
- Camada de fundo persistente (`data-layout-ignore`): glow radial âmbar respirando, ghost text gigante driftando, grid hairline, grêo.
- Escala grande: headline 64–172px, corpo 28–42px, decorativos 12–25% opacidade, bordas 2–4px.
- Movimento: entradas 0.4–0.6s, eases variados, combinar transform+opacity, stagger 0.08–0.14s. Toda decoraçêo tem motion ambiente.
- Captions no rodapé (Inter 600, fundo translúcido). Barra de progresso âmbar no rodapé.

## Formatos
- 16:9 → 1920×1080. 9:16 → 1080×1920 (overrides via `body.v` no gerador).
- Sempre gerar AS DUAS versões por padrêo.

## CTA final (ARCKHÉ AI)
"CONTINUA EM" + **ARCKHÉ AI** (ARCKHÉ `--fg`, ".CLUB" `--accent`, glow drop-shadow) + `🌐 ARCKHÉ AI` (mono). Narraçêo: "Isso é conteúdo do ARCKHÉ ponto CLUB. Acesse: ARCKHÉ ponto club."
