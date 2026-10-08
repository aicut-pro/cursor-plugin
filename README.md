# aicut for Cursor

Generate AI **story episodes, videos, images and audio** on your own aicut account, and publish them
to TikTok, YouTube and Instagram, without leaving Cursor.

This plugin adds one remote MCP server, `https://mcp.aicut.pro/mcp`. It runs on aicut's side, so
there is nothing to install locally and nothing to keep running.

## Installation

### Cursor Directory

In Cursor, type `/add-plugin` in chat, search for **aicut**, and install it. The listing lives on
[cursor.directory](https://cursor.directory), Cursor's plugin directory.

### One-click install link

[Add aicut to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=aicut&config=eyJ1cmwiOiJodHRwczovL21jcC5haWN1dC5wcm8vbWNwIn0=)

Cursor asks you to confirm before anything is added. The same button is on
[aicut.pro/mcp](https://www.aicut.pro/mcp).

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
- **Generate videos, images and audio** - create new generations, spending tokens just like the app
  does.

Disconnect any time from **Connected apps** in your aicut account settings. That revokes access
immediately, on the connection's very next request.

## What it can do

54 tools, plus nine step-by-step recipes (`get_recipe`), all operating on the signed-in aicut
account. Everything you make lands in your normal aicut library, ready to edit, animate or reuse on
the site.

### Catalog and account

| Tool | What it does |
| --- | --- |
| `list_models` | The curated video, image and audio catalog with the exact cost of every settings combination. Call this first. |
| `get_balance` | Tokens left on the account, and its plan tier. |
| `list_voices` | The whole voice catalogue, ElevenLabs and OpenAI, including this account's cloned voices. |
| `list_characters` | The account's uploaded characters and generated story cast members. |
| `list_series` / `list_series_ideas` / `browse_series` | The AI Video Story catalog: which series an episode can be made in, with prices and curated episode ideas. |
| `get_recipe` | A step-by-step recipe for a flow: a first video, image or audio, a story episode, a talking avatar, motion control. |

### Video, image and audio

| Tool | What it does |
| --- | --- |
| `generate_video` / `get_video` / `list_videos` / `delete_video` | Start a video on any catalog model, read one back, or browse the library. |
| `generate_image` / `get_image` / `list_images` | Generate an image (usually finished in the same call), read one back, or browse. |
| `generate_audio` / `get_audio` / `list_audio` | Speech, music or a sound effect, chosen by `model`. |
| `wait_for_generation` | Waits server-side and answers whether a job is finished. |
| `show_generation` | Shows an earlier generation again. |

### Transforms on media you already have

| Tool | What it does |
| --- | --- |
| `upscale_video` / `upscale_image` | 2x or 4x a video; more pixels in an image from three upscalers. |
| `extend_video` | Continues an existing video by a chosen number of seconds. |
| `motion_control` | A character picture plus a reference clip, and the character performs that motion. |
| `generate_lipsync` | A character picture plus audio from this account, lip-synced. |
| `edit_video` | A 3-10 second clip plus a description of what to change: same camera move and timing, different cast, clothes or setting. |

### Video analysis

| Tool | What it does |
| --- | --- |
| `analyze_video` / `get_analysis` / `list_analyses` | Analyse a public YouTube, TikTok or Instagram video, or one you uploaded. Free, capped per day. |

### AI Video Story, the staged episode flow

An episode is made in stages and each stage has its own price: the cast is written free and its
portraits are bought, the start frames are charged and park for review, firing buys the scene
videos, rendering buys the final file.

| Tool | What it does |
| --- | --- |
| `generate_cast` | FREE. Writes a story cast for a series. |
| `generate_cast_portraits` / `regenerate_cast_portrait` / `describe_cast_member` | Buy the portraits, redraw one, or change what a cast member is. |
| `generate_story_video` | Stage 1: writes the episode, generates the start frames, parks for review. |
| `regenerate_story_frame` / `change_story_scene` / `remove_story_scene` | Adjust the parked episode before any video is bought. |
| `fire_story_video` | Stage 2: generates the scene videos. Irreversible. |
| `render_story_video` | Stage 3: the final render. |

### One-call formats

| Tool | What it does |
| --- | --- |
| `generate_fake_text_video` | The fake-text chat-story format, written, spoken and rendered in one call. |
| `generate_image_story` / `list_image_story_styles` | The AI image story format, with aicut's authored looks. |
| `list_niches` / `generate_from_niche` | aicut's one-shot trending formats, each made from a few answers at one price. |

### Publishing to social

| Tool | What it does |
| --- | --- |
| `list_social_accounts` | The TikTok, YouTube and Instagram accounts this user has connected. |
| `prepare_post` / `review_post` / `publish_post` / `get_post_status` | Stage a post of a finished video, review it on a consent card, publish or schedule it, and read back what the platform said. |

### Trends and uploads

| Tool | What it does |
| --- | --- |
| `list_trends` / `get_recreate_brief` | aicut's published trend feed, and how to recreate one trending video. |
| `upload_media_widget` / `upload_media` / `confirm_upload` | Use your own footage and images: an in-card file picker, or a signed upload target plus its confirmation. |

## Cost

Adding the plugin is free. Generating spends tokens from your own aicut balance, at the same prices
you pay in the app. Video analysis is free.

Every tool that spends is marked as a spending tool, so Cursor asks before running it, and every
`generate_*` tool takes `estimate_only: true` to get the exact price without creating anything.
Asking for an estimate first is the safe habit.

## Links

- Connect instructions for every client: [aicut.pro/mcp](https://www.aicut.pro/mcp)
- Server metadata and the full tool reference: [aicut-pro/aicut-mcp](https://github.com/aicut-pro/aicut-mcp)
- Account and billing: [aicut.pro](https://www.aicut.pro)
- Support: support@aicut.pro
