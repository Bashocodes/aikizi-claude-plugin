---
name: aikizi-decode-and-generate
description: Decode the person's own image or generate an image on AIKIZI with their account. Use when they ask to decode an image link, read their own AIKIZI decodes or library, check credits, or generate an image from a prompt. These tools need the AIKIZI connector signed in and spend the account's credits.
---

# AIKIZI with the person's account

Seven tools act on the signed-in AIKIZI account. The person connects once (Claude's connector sign-in; nothing is
shared until they allow it). Decoding and generating spend credits from that account, so be deliberate.

## Before spending

- Run `check_balance` first when the person has not generated or decoded in this conversation. Tell them the
  balance in one line. If it is zero, stop and point them to aikizi.com; do not retry.
- Say what you are about to spend on and why, in one sentence, before the first paid call. After that, continue
  without re-asking unless they change the task.

## Decode an image

1. `decode_image` takes one public `https://` link to a JPEG, PNG or WebP up to 10 MB. Data URLs, local paths and
   private links fail. If the person only has a file, ask them to upload it at aikizi.com/decode or to a public host.
2. If the answer says "still running", call `check_job_status` with the `decode_id` every 10 seconds or so, up to
   two minutes. Then read the result with `get_my_decode`.
3. Present styles, style DNA, mood, key tokens, hues and the prompt. Decodes stay private in their library.

## Generate an image

- `generate_image` takes `prompt` plus optional `aspect_ratio`, `resolution` and `model`. Use the model the
  person names; otherwise leave `model` out so the server picks the default.
- Write the prompt from a decode's prompt and key tokens when the ask is "make something like this".
- The answer carries the creation id and an aikizi.com link; `get_creation` reads it back later.
- One generation per ask. Do not loop or batch generations unless the person asks for a number.

## Their library

- `list_my_creations` with `type` image, video or audio and a small `limit` for "what did I make".
- `get_my_decode` for one decode (published or private); `get_creation` for one generated image.

## Never

- Never call a paid tool to "test" the connection; `check_balance` is the test.
- Never claim a decode or creation is published. The server keeps everything it makes private.
