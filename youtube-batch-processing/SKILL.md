---
name: youtube-batch-processing
description: "Batch process YouTube transcripts safely. Avoid IP bans."
version: 1.0.0
author: Hermes Agent
license: MIT
metadata:
  hermes:
    tags: [YouTube, Batch, Ingestion, Scripts]
    related_skills: [youtube-content]
---

# YouTube Batch Processing

## When to use
Use this skill when writing scripts, cronjobs, or background routines that ingest multiple YouTube videos from a playlist or list. 

## The Procedure

When setting up a pipeline to process playlists:
1. **Maintain State:** Use a local cache file (e.g., `~/.hermes/cache/playlist_processed.txt`) to track which Video IDs have already been processed.
2. **Read the RSS Feed:** YouTube playlists have native RSS feeds at `https://www.youtube.com/feeds/videos.xml?playlist_id=ID`. Use this instead of scraping the HTML.
3. **Chunk the Workload:** Never process the whole backlog at once. Pick the oldest 2 unseen videos, process them, and exit.

## Pitfalls

- **Do not fetch transcripts in a fast loop:** Fetching more than 3-5 transcripts in a short window using `youtube-transcript-api` (used by the `youtube-content` skill) will trigger a hard HTTP 429 (Too Many Requests) IP ban from YouTube, blocking all further extraction.
- **Limit to 2 videos per execution tick:** When catching up on a long playlist, limit the script to process exactly 2 videos per cron tick, saving state after each. Let the cronjob naturally drain the backlog over several hours.
- **Do not rely on browser fallbacks for background jobs:** If the IP gets banned, falling back to CDP/browser extraction in a cronjob will fail if the user's primary browser profile is currently locked by their foreground usage. Stick to the 2-video limit to keep the API path open.