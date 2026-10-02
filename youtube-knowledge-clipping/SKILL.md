---
name: youtube-knowledge-clipping
description: Ingest YouTube or Instagram videos into structured Obsidian vault notes.
---

# Video Knowledge Clipping (YouTube + Instagram)

Use this workflow to ingest, transcribe, and format social videos (YouTube, Instagram Reels/DMs) into highly structured Markdown notes for a knowledge base like Obsidian. Same class of task regardless of platform: get transcript + metadata, write one clipping note per video, never silently keep or drop media.

## Media retention — ask before assuming

- Default assumption for 'ingest/transcreva os vídeos igual do YouTube': **transcript only**. Do not download a video into a permanent location (vault, media/ folder) unless the user explicitly says to keep the file. A request to 'ingest like X' is about the note, not the media.
- If persistence is genuinely ambiguous, ask once before writing any pipeline code — building the wrong default (e.g. auto-copying downloaded video into the vault) wastes disk and gets immediately reverted.
- When a video must be downloaded to extract audio (yt-dlp + ffmpeg), download to a `/tmp` working dir and delete it (video, audio, info-json) in a `finally` block right after transcription — never leave it in `~/.hermes/cache/scratch` or the vault.

## Space-constrained Mac batches

- Before any batch of media downloads on a Mac with limited free disk, check `df -h /` first and set a hard abort threshold (e.g. stop if free space drops below ~2 GiB) inside the batch script itself, not just as a manual check — batches run unattended in the background and a full disk mid-run corrupts partial writes.
- Run background batches with `terminal(background=true, notify=true)`, not `nohup`/`disown` in a foreground command — the tool rejects shell-level backgrounding wrappers.

## Workflow

1. **Extract Transcript**: Use the `youtube-content` skill tools (e.g. `uv run python ~/.hermes/skills/media/youtube-content/scripts/fetch_transcript.py "<url>" --text-only`) to get the raw text.
2. **Format as Premium Clipping**: Act as a Senior Technical Analyst. Read the transcript deeply and generate a highly detailed note in Portuguese using the template below.
3. **Save to Vault**: Save the note to the appropriate folder in the knowledge base (e.g., `~/mega-brain/02 - Base de Conhecimento/YouTube/<Topic>/`).
4. **Drive Real-World Application**: Never stop at the static Obsidian dump. Generate an architectural visual map (e.g., Mermaid mindmap) of the video's system and explicitly map out how to execute that system *today* using Hermes' currently installed skills. Static notes without execution steps are considered "knowledge cemeteries" by the user.

## Template (Premium Knowledge Base Clipping)

```markdown
---
tipo: clipping
tags:
  - youtube
  - ai
  - ingestion
---
# 🎬 [Exact Video Title]

**🔗 Link do Vídeo:** [URL]

## 📌 Resumo da Ópera
[Dense 2-3 paragraph summary of the core thesis, problem solved, and general context.]

## 🛠️ Ferramentas & Tecnologias Citadas
[Bulleted list of all tools/frameworks mentioned and exactly how they were used in the video.]
- **[Tool Name]**: [Usage context]

## 💡 Insights e Viabilidade Prática
[Real-world applications. How this changes workflows or processes.]
- **[Insight]**: [Deep explanation]

## 📖 Vocabulário e Novos Conceitos
[Definitions for technical terms/jargon used]
- **[Term]**: [Definition]

## 🎯 Próximos Passos (Action Items)
[2-3 actionable tests or next steps based on the video]
- [ ] [Action 1]
- [ ] [Action 2]
```

## Pitfalls & Rate Limits

- **YouTube IP Bans (HTTP 429)**: When processing multiple videos (e.g., in a cronjob or batch scraping script), strictly limit extraction to 2-3 videos per run. Processing ~15+ videos back-to-back from the same IP reliably triggers a temporary IP ban from YouTube (Too Many Requests). Throttle batch jobs accordingly.