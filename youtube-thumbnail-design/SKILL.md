---
name: youtube-thumbnail-design
description: Use when designing YouTube thumbnails (Tech/AI niche).
---

# YouTube Thumbnail Design (Tech/AI Niche)

This skill dictates how to produce thumbnails and thumbnail-generation pipelines for the user, conforming to their specific high-end "Anti-AI Slop" aesthetic inspired by channels like @ddiasmatt.

## 🔴 CRITICAL USER PREFERENCE: NO PROGRAMMATIC RENDER
Do **NOT** attempt to write Python scripts (using Pillow, `rembg`, OpenCV) to compose or render the final thumbnail image directly. The user explicitly rejected programmatic generation ("você não cria mais thumbnails caralho, você só gera o prompt pra eu colocar no gpt").

**The Output Deliverable:**
The deliverable for a thumbnail request is a **Highly Detailed GPT-Vision Prompt** in Portuguese. The user will manually copy this prompt and paste it into ChatGPT Vision, attaching their own selfie and a reference thumbnail.

## The Aesthetic Rules & Prompt Architecture
Whenever you generate a prompt for the user to use in ChatGPT Vision, you MUST use the exact architectural structure below. 

### Output JSON Shape
Your response (or the script you are writing, like `motor_copy.py`) must output exactly this JSON schema, without markdown blocks:
```json
{
    "referencia_canal_usada": "link_da_referencia_ou_descricao_do_canal",
    "titulo_thumbnail": "...",
    "post_ou_roteiro": "...",
    "prompt_gpt_vision": "O Prompt mega detalhado com base na estrutura abaixo..."
}
```

### The "prompt_gpt_vision" Architecture
The prompt text you generate inside the JSON must follow this exact sectioned template. **CRITICAL: The prompt must be in ENGLISH and use bracketed tags to command the AI generator. DALL-E 3 and Midjourney respond drastically better to structured English commands.**

```text
[IMAGE-TO-IMAGE REBUILD COMMAND]
Rebuild the provided reference image in ultra high resolution, preserving the exact composition, camera angle, pose, and lighting.

[IDENTITY SWAP - SUBJECT]
Replace the subject in the reference image with this exact physical identity: A young adult man with medium warm olive skin. Dense, curly hair (type 3C) with dark roots and frosted blonde tips (ombré). Thick dark chevron mustache and light jawline stubble. Dark straight eyebrows. Small silver hoop earrings, a silver helix hoop, a nose stud, and a silver chain necklace. He is NOT wearing glasses.

[SCENE AND LIGHTING LOCK]
Keep the setting strictly identical to the reference: [DYNAMIC SCENE IN ENGLISH. Ex: sitting in a dark minimalist studio, holding a glowing green smartphone]. The lighting MUST be identical: [DYNAMIC LIGHTING IN ENGLISH. Ex: a harsh rim light highlighting the skin texture, mustache, and curls against the pure black background]. Deep cinematic shadows.

[TECHNICAL FINISH]
Do NOT change the framing. Maintain the space in the top/left/right for text. Add the text "[TÍTULO DA THUMBNAIL]" in bold 3D typography. Photorealistic documentary finish, DSLR 50mm lens, visible skin pores, highly dramatic and moody atmosphere.

[ANTI-AI SLOP INSTRUCTIONS (CRITICAL)]
ABSOLUTELY NO 3D render, NO CGI, NO digital illustration, NO smooth skin, NO plastic look, NO cartoon. This MUST be a RAW, unedited, gritty DSLR photograph. Imperfect skin texture, visible pores, harsh shadows, real human anatomy. If it looks like a video game or Pixar, you failed. Use a 35mm lens, high ISO film grain, and natural studio lighting.
```

**Note on Identity Swap:** The `[IDENTITY SWAP - SUBJECT]` block must remain static exactly as written above to preserve the user's specific morphology. Only adapt the `[SCENE AND LIGHTING LOCK]` and the text in the `[TECHNICAL FINISH]` block.

### Workflow for Finding References
When generating a new post/thumbnail idea, **do not recycle pre-downloaded reference images from your local cache.**
1. **Live YouTube Search:** Perform a live search using `yt-dlp` for high-retention viral videos related to the EXACT generated topic (e.g., `yt-dlp "ytsearch10: [Topic Keywords]" --dump-json | jq -c '{id, title, views}'`).
2. **Download & Present:** Download the max-resolution thumbnail of the most relevant/viral match (`curl -o ref.jpg "https://img.youtube.com/vi/[ID]/maxresdefault.jpg"`) and present it to the user in chat using `MEDIA:/absolute/path/to/ref.jpg`.
3. **Build the Prompt:** Build the prompt meticulously around that newly sourced reference's composition, outputting the JSON.