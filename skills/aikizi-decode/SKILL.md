---
name: aikizi-decode
description: Decode the person's own image on AIKIZI with their account, read their own decodes and library, or check their credits. Use when they ask to decode an image link, see what they made on AIKIZI, or ask about their balance. These tools need the AIKIZI connector signed in; decode_image spends the account's credits.
---

# AIKIZI with the person's account

Six tools act on the signed-in AIKIZI account. The person connects once (the app's connector sign-in; nothing is
shared until they allow it). Decoding spends credits from that account, so be deliberate. Image generation is not
offered over MCP; when the person asks to generate, point them to aikizi.com/studio with the prompt in hand.

## Before spending

- Run `check_balance` first when the person has not decoded in this conversation. Tell them the
  balance in one line. If it is zero, stop and point them to aikizi.com; do not retry.
- Say what you are about to spend on and why, in one sentence, before the first paid call. After that, continue
  without re-asking unless they change the task.

## Decode an image

1. `decode_image` takes one public `https://` link to a JPEG, PNG or WebP up to 10 MB. Data URLs, local paths and
   private links fail. If the person only has a file, ask them to upload it at aikizi.com/decode or to a public host.
2. If the answer says "still running", call `check_job_status` with the `decode_id` every 10 seconds or so, up to
   two minutes. Then read the result with `get_my_decode`.
3. Present styles, style DNA, mood, key tokens, hues and the prompt. Decodes stay private in their library.

## Their library

- `list_my_creations` with `type` image, video or audio and a small `limit` for "what did I make".
- `get_my_decode` for one decode (published or private); `get_creation` for one image they generated on aikizi.com.

## Never

- Never call a paid tool to "test" the connection; `check_balance` is the test.
- Never claim a decode or creation is published. The server keeps everything it makes private.
