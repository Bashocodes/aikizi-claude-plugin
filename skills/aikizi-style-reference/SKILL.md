---
name: aikizi-style-reference
description: Find and explain image styles with AIKIZI. Use when the person wants a visual reference, a style breakdown, a colour palette, a mood, "how was this made", or a prompt to start an image from. Uses the public search_styles and get_style_decode tools; no sign-in needed.
---

# AIKIZI style reference

AIKIZI (aikizi.com) decodes images the way an art director reads them: styles, style DNA, subjects, moods,
key tokens, colour hues and a generation prompt. The two public tools read only decodes their owners published.

## Flow

1. `search_styles` with a short query made of style, subject, mood or colour words (2 to 6 words works best).
   Ask for 5 to 8 results. Example: `{"query": "neon noir portrait", "limit": 8}`.
2. Pick the two or three results that fit the ask. Call `get_style_decode` with each `id` for the full breakdown.
   An `aikizi.com/decode/<id>` link the person pastes also works as the id.
3. Answer with what the decode says, in this order: styles and style DNA, mood, key tokens, colour hues, then the
   generation prompt as a fenced block the person can copy.
4. Always give the `aikizi.com/decode/<id>` link for each decode you used, so the person can see the image.

## Rules

- Quote the decode's prompt as given; mark your own edits as yours.
- A search with no good match: try one simpler query (drop the rarest word), then say so. Do not invent styles.
- Decodes belong to the people who published them. Describe the style; do not present the image as the person's own.
- These tools never need the person's account. If they want to decode their own image, use the `aikizi-decode`
  skill, which needs an AIKIZI sign-in. Image generation is not offered over MCP; it lives on aikizi.com.
