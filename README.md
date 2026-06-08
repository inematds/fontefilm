# fontefilm

**Um diretor de cinema de IA que transforma texto em filme de quadrinhos — rodando na sua máquina.**

🌐 **Site / guia de uso:** https://inematds.github.io/fontefilm/

Você escreve um **texto base** (a história ou o assunto), escolhe um **estilo visual**, e o fontefilm faz o resto: roteiro → cenas → personagens → imagens → narração → montagem → **vídeo final**.

A maioria das ferramentas só *gera* imagem ou vídeo. O fontefilm tenta **dirigir** de verdade — como um diretor: que plano usar (close, geral, over-the-shoulder), composição, luz, ritmo, transições entre quadros (teoria do Scott McCloud) e estrutura de história (3 atos). Esse "cérebro de direção" é o diferencial.

## O caminho

```
texto + estilo
  → roteiro (3 atos)
  → bíblia (personagens / locações / paleta)
  → decupagem (plano + câmera de cada painel)
  → painéis de quadrinho (imagem)
  → movimento (parallax 2.5D / Ken Burns)
  → narração + som
  → montagem
  → 🎥 filme.mp4
```

## Princípios

- **Local-first.** Roda na sua máquina com modelos locais (flux2-klein para imagem, inemavox para voz). APIs pagas (Kling, Runway, Nano Banana) são **opcionais**, ligadas por `.env` / UI.
- **Direção dirigida por conhecimento.** Um *Knowledge Pack* versionado (gramática de cinema + teoria de HQ) alimenta os agentes de direção via RAG.
- **Uma engine, várias portas.** A lógica vive numa engine Python; você aciona por **CLI**, por uma **skill** conversacional (wrapper fino, no padrão `pixflow-motion`) e, na Fase 3, por **UI web** no portal `inema.club`.
- **Projeto reproduzível.** Cada decisão (plano, seed, prompt, provider) fica em arquivos legíveis em disco.

## Fases

| Fase | Entrega |
|------|---------|
| **v1 (Fase 0)** | Motion comic completo: painéis estáticos + câmera + narração. CLI. PT-BR, 16:9 ou 9:16. |
| Fase 1 | Animação leve (LivePortrait / parallax), música/SFX, consistência avançada de personagem. |
| Fase 2 | Vídeo IA híbrido (LTX/Wan local; Kling/Runway API), agendador paralelo (DAG/CPM). |
| Fase 3 | UI web no portal `inema.club` sobre o mesmo engine. |

## Estado atual

> **Em design/prototipagem.** A engine ainda não está construída — o que existe é a fundação.

- ✅ **Pesquisa profunda** — padrões a copiar de pipelines open-source (Forge Film, ViMax, FilmAgent, FilMaster, LivePortrait, MovieLabs OMC). Ver [`docs/research/`](docs/research/).
- ✅ **Spec/design aprovado** — [`docs/superpowers/specs/2026-06-07-fontefilm-design.md`](docs/superpowers/specs/2026-06-07-fontefilm-design.md).
- ✅ **Teste real ponta a ponta** — *"12 Leis do Crescimento"* (dicas do Alex Hormozi): o pipeline rodado "na mão" para provar o conceito. Saiu um motion comic 1080p narrado e sincronizado (106s). Receita reproduzível em [`projetos/hormozi12/`](projetos/hormozi12/).

## Stack

Python 3.11 (engine/CLI) · ComfyUI + flux2-klein (imagem) · inemavox (voz) · pixflow-motion para parallax 2.5D (Depth-Anything-V2 → WebGL → Remotion → FFmpeg) · Claude como LLM diretor (default), modelo local como fallback.

## Estrutura do repo

```
docs/research/      # pesquisa de pipelines de referência
docs/superpowers/   # spec/design da v1
projetos/<nome>/    # projetos de filme (entrada + assets + saída)
```

> Pesquisa / educação / testes. Assets pesados (imagens, áudio, MP4) ficam fora do git.
