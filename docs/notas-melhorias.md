# Notas de melhoria (backlog)

Observações capturadas durante os testes, a tratar no design/implementação da engine.

## Camada de texto (do teste hormozi12, 2026-06-07)

1. **Texto cortado / limite de tamanho.** No lower-third, a largura/box limitou e **cortou títulos longos** (ex.: "06 — Una vendas e marketing"). 
   - Corrigir no render real: **medir a largura do texto** e fazer **auto-fit** (reduzir fontsize) ou **quebra de linha**, com box que se ajusta ao conteúdo. Nada de largura fixa que trunca.
   - No Remotion isso é natural (layout flex/medição); no hack via ffmpeg `drawtext` foi o ponto fraco.

2. **Tipografia a aprimorar.** A fonte/estilo do texto (DejaVu Bold no teste) é básica. 
   - Referência de qualidade: skill **`video-explicativo`** — estudar a fonte, peso, sombra/contorno, espaçamento e **animação de entrada** das captions dela e adotar um tratamento equivalente (premium) no fontefilm.
   - Caminho: `~/.claude/skills/video-explicativo` (ver como ela estiliza/anima legendas e título).

## Layout por formato — safe areas

3. **9:16 (Reels/Shorts): zonas seguras.** No vertical, a UI do Instagram/TikTok **polui o terço inferior** (botões, legenda, perfil). Regra de composição a implementar:
   - **Texto/chamadas no MEIO** (centro vertical), não embaixo.
   - **Movimento/ação na parte SUPERIOR** do quadro.
   - **Evitar o terço inferior** para conteúdo importante.
   - Generalizar: definir **safe-areas por formato** (16:9 vs 9:16) no render, e o Knowledge Pack de direção respeita isso ao posicionar texto e enquadrar a ação.
