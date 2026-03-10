---
name: nano-banana-images
description: Generate hyper-realistic, highly controlled images using Nano Banana 2 (Gemini 3.1 Flash) via parameterized JSON prompting.
status: active
applies_to: all
domain: general
consumer: cursor
---

# Nano Banana 2 image generation

**Use when** the user asks for a highly detailed, realistic, or complex image and the generation should follow a strict schema to avoid "AI look" (over-smoothing, plastic skin, etc.).

## Summary

- **Model:** Nano Banana 2 (e.g. via Kie.ai API or `generate_image` tool).
- **Method:** Structured JSON prompt (task, output, subject, environment, image_quality_simulation, explicit_restrictions, negative_prompt, etc.).
- **Kie.ai:** JSON prompt file → `~/.cursor/skills/nano-banana-images/scripts/generate_kie.py` (or project script). Requires `KIE_API_KEY` in .env.

## Full instructions

For Cursor agents: use the **Nano Banana 2 Image Generation Master** skill. Full schema, dense narrative format, and best practices are in:

`~/.cursor/skills/nano-banana-images/SKILL.md`  
`~/.cursor/skills/nano-banana-images/master_prompt_reference.md`
