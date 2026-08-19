# aicut for Cursor

Generate AI video, images and voice-over on your own aicut account, and analyse any video, without
leaving Cursor.

This plugin adds one remote MCP server, `https://mcp.aicut.pro/mcp`. It runs on aicut's side, so
there is nothing to install locally and nothing to keep running.

## Installation

### Cursor Marketplace

In Cursor, type `/add-plugin` in chat, search for **aicut**, and install it.

You can also install directly from [Cursor Marketplace](https://cursor.com/marketplace/aicut).

### One-click install link

[Add aicut to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=aicut&config=eyJ1cmwiOiJodHRwczovL21jcC5haWN1dC5wcm8vbWNwIn0=)

Cursor asks you to confirm before anything is added.

### By hand

In Cursor open **Customize**, then **MCPs**, then **New MCP Server**. Name it `aicut` and paste:

```
https://mcp.aicut.pro/mcp
```

### From source (local development)

Cursor scans `~/.cursor/plugins/local/<plugin-name>/` for local plugins. Copy this repo into that
directory:

```bash
git clone https://github.com/aicut-pro/cursor-plugin.git
mkdir -p ~/.cursor/plugins/local
rsync -a --delete --exclude='.git' cursor-plugin/ ~/.cursor/plugins/local/aicut/
```

Reload Cursor: `Cmd-Shift-P` then `Developer: Reload Window`.

Verify:

- `Cursor Settings` then `Plugins` lists **aicut**.
- `Cursor Settings` then `Tools & MCPs` shows `aicut` with a green dot.

Use a real directory copy; symlinks may not load.

## Authentication

You need an [aicut](https://www.aicut.pro) account. There is no API key to paste and nothing to
configure.

Cursor lists aicut under **Needs attention** on first use. Hit **Authenticate**, sign in with your
aicut account in the browser tab that opens, and choose **Allow**. Cursor registers itself
automatically over OAuth 2.1 with PKCE and stores the credentials itself.

The consent screen asks for two permissions:

- **See your library and token balance** - your videos, images, audio and analyses, the available
  models, and your balance.
- **Generate videos, images and audio** - create new generations and video analyses, spending tokens
  just like the app does.

Disconnect any time from **Connected apps** in your aicut account settings. That revokes access
immediately, on the connection's very next request.

## What it can do

Sixteen tools, all operating on the signed-in aicut account.

| Tool | What it does |
| --- | --- |
| `list_models` | The published models with their parameters and exact prices. |
| `get_balance` | Token balance and plan tier. |
| `generate_video` | Start a video on any of 20 video models, with start frames, end frames and reference images. |
| `get_video` / `list_videos` | Read one video job, or the account's video library. |
| `generate_image` | Start an image on any of 8 image models, including edits and multi-image references. |
| `get_image` / `list_images` | Read one image job, or the account's image library. |
| `generate_audio` | Speech, music or a sound effect on any of 4 ElevenLabs models. |
| `get_audio` / `list_audio` | Read one audio job, or the account's audio library. |
| `analyze_video` | Analyse a public YouTube, TikTok or Instagram video, or one you uploaded to aicut. Free. |
| `get_analysis` / `list_analyses` | Read one analysis, or the account's analysis history. |
| `wait_for_generation` | Wait server-side for a job to finish, up to 15 seconds per call. |
| `show_generation` | Show an earlier generation again. |

Everything you make lands in your normal aicut library, ready to edit, animate or reuse on the site.

## Cost

Adding the plugin is free. Generating spends tokens from your own aicut balance, at the same prices
you pay in the app. Video analysis is free.

The three `generate_*` tools are marked as spending tools, so Cursor asks before running them, and
each one takes `estimate_only: true` to get the exact price without creating anything. Asking for an
estimate first is the safe habit.

## Links

- Connect instructions for every client: [aicut.pro/mcp](https://www.aicut.pro/mcp)
- Account and billing: [aicut.pro](https://www.aicut.pro)
- Support: support@aicut.pro
