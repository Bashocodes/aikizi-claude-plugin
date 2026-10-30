---
name: aikizi-decode
description: Decode the person's own image on AIKIZI with their account, read their own decodes and library, place a decode in the AIKIZI Brain, or check their credits. Use when they attach or point to an image to decode, paste an image link, ask what they made on AIKIZI, or ask about their balance. These tools need the AIKIZI connector signed in; a decode spends the account's credits.
---

# AIKIZI with the person's account

These tools act on the signed-in AIKIZI account. The person connects once (the app's connector sign-in; nothing is
shared until they allow it). Decoding spends credits from that account, so be deliberate. Image generation is not
offered over MCP; when the person asks to generate, point them to aikizi.com/studio with the prompt in hand.

## Before spending

- Run `check_balance` first when the person has not decoded in this conversation. Tell them the
  balance in one line. If it is zero, stop and point them to aikizi.com; do not retry.
- Say what you are about to spend on and why, in one sentence, before the first paid call. After that, continue
  without re-asking unless they change the task.

## Decode an image

1. An image attached to the chat or on the person's device cannot reach AIKIZI directly: call `add_image`. Never
   ask them to host it somewhere.
   - In the Claude apps it opens a drop box in the chat. The person drops, picks or pastes the picture and the box
     decodes it there.
   - In Claude Code or any client with a shell, `add_image` also returns a one-time upload address and the exact
     command that sends the file there. Show the person that command before running it, then call `decode_image`
     with `{"image_id": "<image_id>"}`. One image, JPEG, PNG or WebP up to 10 MB; the address closes in 30 minutes.
2. An image on the web: `decode_image` with `{"image_url": "https://..."}`, a public link to a JPEG, PNG or WebP up
   to 10 MB.
3. A picture this account decoded before comes back as `already_decoded` and nothing is spent. Pass
   `decode_again: true` only when the person asks for a new decode of it.
4. If the answer says "still running", call `check_job_status` with the `decode_id` every 10 seconds or so, up to
   two minutes. Then read the result with `get_my_decode`.
5. Present styles, style DNA, mood, key tokens, hues and the prompt. Decodes stay private in their library.

## The Brain

- `place_in_brain` with a `decode_id` shows where one of their decodes would sit in the AIKIZI Brain
  (aikizi.com/brain): the closest public pictures, each with its link. It reads only and never spends; their decode
  stays private.

## Their library

- `list_my_creations` with `type` image, video or audio and a small `limit` for "what did I make".
- `get_my_decode` for one decode (published or private); `get_creation` for one image they generated on aikizi.com.

## Never

- Never call a paid tool to "test" the connection; `check_balance` is the test.
- Never claim a decode or creation is published. The server keeps everything it makes private.
