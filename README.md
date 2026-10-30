# AIKIZI for Claude

AIKIZI (aikizi.com) reads an image the way an art director does. Each decode names the styles, subjects, moods and
light, pulls the key tokens and colour hues, and writes a prompt you can take to an image model. This plugin gives
Claude the AIKIZI MCP server plus two skills and one command that know how to use it well.

## What you get

| Piece | What it does |
|---|---|
| `aikizi` MCP server | Remote server at `https://aikizi.com/mcp`: public tools, plus tools for your own account (see Tools) |
| Skill `aikizi-style-reference` | Find a style, break it down, find its look-alikes, hand you the prompt and palette. No sign-in |
| Skill `aikizi-decode` | Decode your own image (attached or linked) with your AIKIZI credits, place it in the Brain, read your library |
| Command `/aikizi:style <words>` | Search a style and break down the three best matches |

## Install

From the Claude directory: open **Plugins** in Claude Code or claude.ai, find **AIKIZI**, and install it.

From GitHub, in Claude Code:

```
/plugin marketplace add Bashocodes/aikizi-claude-plugin
/plugin install aikizi@aikizi
```

In Cursor: the same repo is a Cursor plugin (`.cursor-plugin/plugin.json`, `mcp.json`). Or add the server to
Cursor's `mcp.json` directly: `{"mcpServers": {"aikizi": {"url": "https://aikizi.com/mcp"}}}`.

The first time a signed-in tool is needed, Claude asks you to connect AIKIZI. You sign in on aikizi.com and allow
the connection; nothing is shared until you do. Searching styles and reading published decodes work without any
sign-in.

## Try it

- `Find decoded styles with warm film grain and soft window light.`
- `/aikizi:style ink wash landscape`
- `What are the key tokens and colour hues in https://aikizi.com/decode/bc2be49a-ef44-417e-9015-4923febd46ae ?`
- `Find look-alikes of https://aikizi.com/decode/bc2be49a-ef44-417e-9015-4923febd46ae in the AIKIZI Brain.`
- `Decode this picture with my AIKIZI account.` with an image attached (signed in; uses credits)
- `Decode https://example.com/my-photo.jpg with my AIKIZI account.` (signed in; uses credits)
- `List my newest AIKIZI creations and open the latest one.` (signed in)

## Tools

| Tool | Sign-in | Spends credits | What it does |
|---|---|---|---|
| `search_styles` | no | no | Search published decodes by style, subject, mood or colour |
| `get_style_decode` | no | no | Full breakdown of one published decode |
| `find_look_alikes` | no | no | The closest pictures to one published decode in the AIKIZI Brain |
| `check_balance` | yes | no | Your credit balance |
| `add_image` | yes | no | Add an image you have: a drop box in the Claude apps, a one-time upload address in a terminal |
| `decode_image` | yes | yes | Decode an image you added, or one from a public https link |
| `check_job_status` | yes | no | Follow a decode that is still running |
| `get_my_decode` | yes | no | Read one of your own decodes |
| `place_in_brain` | yes | no | Where one of your decodes would sit in the AIKIZI Brain; it stays private |
| `list_my_creations` | yes | no | List your library |
| `get_creation` | yes | no | Open one image you generated on aikizi.com |

Decoding uses the credits of the signed-in account. Credits are given back when a decode fails, and a picture you
decoded before is shown again with nothing spent. Image generation is not offered over MCP; it stays on aikizi.com.
Nothing in this plugin sells anything; plans and credits live on aikizi.com.

## What this plugin runs, sends and fetches

- It runs no local code. There are no scripts, hooks or local servers; the only executable parts are the skill and
  command text files in this repository.
- The MCP server is `https://aikizi.com/mcp`, AIKIZI's own. Claude sends it the tool arguments you see in the
  conversation: a search query, a decode id, an image link, an image id, or a creation id.
- An image you add with `add_image` goes to a one-time upload address on `https://upload.imagedelivery.net`
  (Cloudflare Images, where AIKIZI keeps its images), from the drop box or from an upload command shown to you first. It takes
  one image and closes in 30 minutes.
- Signed-in tools send an OAuth 2.0 token that AIKIZI issues when you connect. The plugin never reads credentials
  from your machine or environment and asks for none.
- `decode_image` makes AIKIZI's server fetch the image link you give it, or read the image you added. The decode is
  stored privately in your AIKIZI library.

## Privacy Policy

AIKIZI's privacy policy: https://aikizi.com/legal/privacy · Terms: https://aikizi.com/legal/terms

- The public tools return only decodes their owners chose to publish. Nothing private or unpublished leaves
  AIKIZI. `place_in_brain` compares your own decode with public ones and never publishes it.
- Signed-in tools act only on the signed-in account and only after you allow the connection. You can revoke it in
  Claude's connector settings or on aikizi.com.
- Images given to `decode_image` or added with `add_image` are stored in your private library and never
  published by the server. The server never publishes, deletes or shares anything on your behalf.
- The plugin itself stores nothing and has no analytics; what it sends goes only to aikizi.com and the one-time
  upload address above.

## Support

hello@aikizi.com · https://aikizi.com/guide/mcp · https://aikizi.com/faq

## License

MIT, see `LICENSE`.
