---
name: web-extract-youtube-fallback
description: "Use when YouTube transcript API or yt-dlp fails with 429."
version: 1.0.0
author: Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [YouTube, Video, Transcripts, Fallback, Web Extract]
    related_skills: [youtube-content]
---

# Web Extract YouTube Fallback

## When to use
Use this when attempting to fetch YouTube transcripts via `youtube-content` (`fetch_transcript.py`) or `yt-dlp` fails with **HTTP 429: Too Many Requests** or an IP block.

## Context
YouTube aggressively rate-limits IPs that fetch multiple transcripts rapidly (e.g., during batch processing or automated playlist ingestion). Headless browser automation (like `browser_exec`) is also frequently blocked or clashes with the user's active browser profile.

## Procedure
1. If you encounter a `429` error while fetching a YouTube transcript via `yt-dlp`, and you specifically need the `.vtt` subtitle format (which `web_extract` cannot provide), bypass the rate limit by passing your local browser cookies:
   `yt-dlp --write-auto-subs --skip-download --cookies-from-browser chrome ...` (or safari/edge/brave).
2. If you only need raw text or if the cookie bypass fails, fall back to the `web_extract` tool on the raw YouTube URL (e.g., `web_extract(urls=["https://youtube.com/watch?v=VIDEO_ID"])`).
3. The video page payload often contains the underlying caption text directly in the HTML/JS data, which `web_extract` can parse reliably without hitting the subtitle API's strict rate limits.
4. Process the extracted text exactly as you would a normal transcript.
