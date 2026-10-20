---
name: style
description: Search AIKIZI for a style and break down the best matches
argument-hint: <style, subject, mood or colour words>
---

Use the aikizi-style-reference skill. Search AIKIZI for "$ARGUMENTS" with `search_styles` (limit 8), pick the three
strongest matches, read each with `get_style_decode`, and answer with: styles and style DNA, mood, key tokens, colour
hues, the generation prompt in a fenced block, and the aikizi.com/decode link for each. If nothing fits, try one
simpler query and say so.
