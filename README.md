# Stable Diffusion Notes

Notes distilled from an `/sdg/` (Stable Diffusion General, 4chan `/g/`-style)
thread — UIs, current model releases, and where models/LoRAs actually live.

See [LINKS.md](LINKS.md) for the full raw link list, organized by section.

## Picking a UI

- **EasyDiffusion** — beginner UI, simplest on-ramp, least configurable.
- **SwarmUI** — modular web UI with both a beginner "Generate" tab and an
  advanced ComfyUI-workflow tab, so it doubles as a stepping stone into
  ComfyUI later. Natively supports images (SD/Flux/Krea 2), video (MiniMax
  H3, Wan, LTX-2), and some audio models. Supports multi-GPU generation (the
  "Swarm" in the name). MIT-licensed, "almost-release" maturity.
- **ComfyUI** — the advanced, node-graph engine everything else in this
  space is converging toward (SwarmUI's advanced tab *is* a Comfy workflow
  tab). Broadest model support (SD, FLUX, Qwen, video/audio/3D), smart memory
  management, API endpoints for production use, fully offline-capable unless
  you opt into paid API nodes. Steeper learning curve — visual node graph
  instead of a form.
- **Forge Classic** — a maintained fork/continuation of the older
  Automatic1111/Forge-style UI, for people who prefer that interaction model
  over Comfy's node graph.
- **Stability Matrix** — not a generation UI itself but a package
  manager/launcher: one-click install/update for A1111, ComfyUI, Fooocus,
  InvokeAI, etc., plus a shared model checkpoint manager (so you're not
  duplicating multi-GB files across installs) and a built-in CivitAI/HF model
  browser with resumable downloads. Good starting point if you're not sure
  which UI you'll end up preferring.

**Practical takeaway**: if you're just starting, SwarmUI is the pragmatic
middle ground (simple tab now, Comfy workflows later without switching
tools). If you already know you want maximum control, go straight to
ComfyUI. Stability Matrix is worth it specifically if you expect to try
multiple UIs/packages rather than commit to one.

## Current models mentioned in the thread (09/2026 snapshot — expect this to age fast)

- **MiniMax H3** (video) — text-to-video, image-to-video, and
  reference-to-video generation. Ships as a repackaged bundle for ComfyUI:
  diffusion weights in several quantizations (bf16/int8/fp8), a Qwen3-VL text
  encoder, LoRAs for faster inference, audio+video VAEs, and 10 style
  embeddings. Heavily used already (~19M monthly HF downloads, 46 community
  Spaces built on it) — this is the current default video model to reach for.
- **Krea 2** — 12B-parameter text-to-image Diffusion Transformer from
  Krea.ai. Two checkpoints: **Raw** (base, best for fine-tuning) and
  **Turbo** (post-trained, faster). Open-weight under Krea's own community
  license; supports Diffusers/SGLang/their own codebase.
- **Z-Image (Turbo)** — a fast *distilled* diffusion model — the whole
  selling point is generation speed over raw quality/flexibility. Needs a
  Qwen 3 4B text encoder + its own diffusion weights + a VAE, all placed in
  ComfyUI's standard model folders.
- **Flux.2 (Dev/Klein)** — state-of-the-art image diffusion, notable for
  accepting multiple reference images as optional input (useful for
  style/character consistency across generations). Ships in a memory-
  efficient fp8 variant and a full-size one; needs a Mistral-based text
  encoder.
- **Chroma** — an architectural modification of Flux (not a from-scratch
  model) — think "Flux variant with tweaks," not a competitor architecture.
  Uses a t5xxl text encoder (fp16 normally, fp8_scaled if memory-constrained).
- **Anima** — 2B-parameter model *specifically* for anime/illustration
  (non-photorealistic) work, trained mostly on anime images plus ~800K other
  art. Three variants: **Base** (for custom LoRA training), **Aesthetic**
  (tuned for consistent quality), **Turbo** (8-12 step fast inference). Uses
  Danbooru-style tags plus natural language, `@`-prefixed artist tags.
  Non-commercial license: you can sell *images* you generate, but can't
  resell/host the model itself as a paid service without a separate license.

**Which one for what**: general realistic/flexible images → Krea 2 or
Flux.2; speed-first iteration → Z-Image Turbo; anime/illustration → Anima;
video → MiniMax H3; if you're modifying/fine-tuning Flux specifically →
Chroma is the community's modified base to look at.

## Where models/LoRAs actually live

- **CivitAI** and **Hugging Face** are the two default hubs.
- The rest of the list (tungsten.run, yodayo.com/models, diffusionarc.com,
  miyukiai.com, civitaiarchive.com, civitasbay.org, stablebay.org,
  openmodeldb.info) are smaller/alternative/archive hosts — several of these
  exist specifically because CivitAI periodically removes NSFW or
  otherwise-flagged content, so the "archive"/"bay" naming pattern is
  functioning as a mirror/backup layer for models at risk of removal there.
  `openmodeldb.info` is specifically an upscaling-model index, not a general
  model host.

## The rentry link index (`rentry.org/sdg-link`)

This is the actual comprehensive resource — worth bookmarking over any
single model/UI link above, since it's kept current by the community and
covers: install guides per GPU vendor (Nvidia/AMD/Intel/Apple
Silicon)/CPU-only, cloud options (Colab/Paperspace), "try online" sites for
zero-install experimentation, technique guides (ControlNet, LoRA training,
Dreambooth, textual inversion, model merging), video-generation tool links
(Hunyuan/Wan family), plugins for Krita/Photoshop/Blender/GIMP, and
community resources (artist style references, prompt databases,
benchmarks).

## Related boards (if this general doesn't cover your use case)

The thread cross-links sibling generals for adjacent boards — furry
(`/aco/csdg/`), degenerate/NSFW-general (`/b/degen`), hentai/adult
(`/d/ddg`, `/e/edg`, `/h/hdg`), video (`/gif/vdg`), toys/figures-adjacent
(`/tg/slop`), yuri (`/u/udg`), pony (`/vp/napt`), and vtuber-AI (`/vt/vtai`).
Same tools/models, different community focus/content norms — listed here
for completeness, not summarized individually.
