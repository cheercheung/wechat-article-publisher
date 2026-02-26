# WeChat Article Publisher

Complete workflow for publishing articles to WeChat Official Account (微信公众号).

English | [中文](README.zh-CN.md)

## Features

- ✍️ **Markdown Editing** - Write articles in Markdown format
- 🎨 **Wenyan Typesetting** - Professional WeChat MP styling and排版
- 🖼️ **AI Cover Generation** - Auto-generate cover images with Evolink API
- 📤 **One-Click Publish** - Direct publish to WeChat MP draft box

## Workflow

```
Markdown File → Wenyan Typesetting → Evolink Cover → WeChat Draft Box
```

## Installation

### Prerequisites

```bash
# Install Wenyan MCP for professional typesetting
npm install -g @wenyan-md/mcp
```

### Install This Skill

```bash
mkdir -p ~/.openclaw/skills/wechat-article-publisher
git clone https://github.com/cheercheung/wechat-article-publisher.git ~/.openclaw/skills/wechat-article-publisher
```

## Quick Start

### Step 1: Prepare Required Information

You need to provide:

1. **WeChat App ID** - From WeChat MP backend → Settings → Basic Configuration
2. **WeChat App Secret** - Same location as App ID
3. **Evolink API Key** - Get from https://evolink.ai

### Step 2: Create Your Article

Create a Markdown file with FrontMatter:

```markdown
---
title: My Awesome Article
cover: /path/to/cover.jpg  # Optional - will auto-generate if not provided
---

# Introduction

This is my article content.

## Section 1

- Point 1
- Point 2
- Point 3

## Code Example

```python
print("Hello WeChat!")
```

> This is a quote
```

### Step 3: Publish

```bash
python3 ~/.openclaw/skills/wechat-article-publisher/scripts/publish.py \
  --app-id "wx..." \
  --app-secret "..." \
  --evolink-key "sk-..." \
  --markdown ./my-article.md \
  --theme default \
  --author "Your Name"
```

## Usage Examples

### Example 1: Basic Usage

```bash
export WECHAT_APP_ID="wxa7c34d64a265f9b2"
export WECHAT_APP_SECRET="your_secret"
export EVOLINK_API_KEY="sk-your-key"

python3 scripts/publish.py \
  --app-id "$WECHAT_APP_ID" \
  --app-secret "$WECHAT_APP_SECRET" \
  --evolink-key "$EVOLINK_API_KEY" \
  --markdown ./article.md
```

### Example 2: With Custom Cover Prompt

```bash
python3 scripts/publish.py \
  --app-id "$WECHAT_APP_ID" \
  --app-secret "$WECHAT_APP_SECRET" \
  --evolink-key "$EVOLINK_API_KEY" \
  --markdown ./article.md \
  --cover-prompt "A cute space lobster holding gold coins, digital art style, vibrant colors"
```

### Example 3: Complete Command

```bash
python3 scripts/publish.py \
  --app-id "wxa7c34d64a265f9b2" \
  --app-secret "dcbecfc3f4d1d2ece2ae334955091a92" \
  --evolink-key "your_evolink_api_key" \
  --markdown ./openclaw-money-article.md \
  --theme default \
  --author "AI Observer" \
  --cover-prompt "A professional cover about AI making money, modern digital art, 16:9"
```

## Command Line Options

| Option | Required | Description |
|--------|----------|-------------|
| `--app-id` | Yes | WeChat App ID |
| `--app-secret` | Yes | WeChat App Secret |
| `--evolink-key` | Yes | Evolink API Key for cover generation |
| `--markdown` | Yes | Path to Markdown file |
| `--theme` | No | Wenyan theme (default: default) |
| `--author` | No | Article author name |
| `--cover-prompt` | No | Custom prompt for AI cover generation |

## Available Themes

Wenyan supports multiple themes for different styles:

- `default` - Clean and classic
- `orangeheart` - Warm orange tones
- `phycat` - Physics cat theme
- And more...

## Markdown Format

### FrontMatter (Optional)

```yaml
---
title: Article Title        # Article title (required in frontmatter)
cover: /path/to/cover.jpg   # Cover image path (optional)
---
```

### Supported Markdown Syntax

| Markdown | Result |
|----------|--------|
| `# Title` | H1 Heading |
| `## Title` | H2 Heading |
| `**bold**` | **Bold** |
| `*italic*` | *Italic* |
| `- item` | Bullet list |
| `1. item` | Numbered list |
| `` `code` `` | Inline code |
| ````code```` | Code block |
| `> quote` | Blockquote |
| `![alt](url)` | Image |
| `[text](url)` | Link |

## Complete Workflow Example

### Scenario: Publish an Article about OpenClaw

**User**: I want to publish an article about OpenClaw making money

**AI**: Sure! Please provide:
1. Your WeChat App ID
2. Your WeChat App Secret
3. Your Evolink API Key

**User**: [Provides credentials]

**AI**: Great! Let me create the article for you...

[AI writes Markdown content]

```markdown
---
title: How to Make Money with OpenClaw
cover: /tmp/auto-generated-cover.jpg
---

# How to Make Money with OpenClaw

OpenClaw is an amazing AI agent tool...

## Real Cases

- Case 1: $43,000/month
- Case 2: $8,200/month
- Case 3: $127,000 in 2 months

## How to Start

```bash
git clone https://github.com/openclaw/openclaw
```

> Start your journey today!
```

**AI**: Publishing now...

```bash
python3 scripts/publish.py \
  --app-id "wx..." \
  --app-secret "..." \
  --evolink-key "sk-..." \
  --markdown ./openclaw-article.md \
  --author "Tech Blogger"
```

**Output**:
```
Step 1: Rendering Markdown with Wenyan...
✓ Rendered: How to Make Money with OpenClaw
Step 2: Generating cover with Evolink...
✓ Cover generated: /tmp/cover_1234567890.jpg
Step 3: Getting WeChat access token...
✓ Token obtained
Step 4: Uploading cover to WeChat...
✓ Cover uploaded: XYz5Fiw6o6F3vnz77zkTH...
Step 5: Publishing to WeChat...

✅ SUCCESS!
Draft ID: XYz5Fiw6o6F3vnz77zkTHlCisnDL_mzOE7ey_2RWITX-di4c44q77r8tcunXxBdh
Title: How to Make Money with OpenClaw

Check your WeChat MP backend -> Drafts
```

**AI**: ✅ Article published! Check your WeChat MP backend → Drafts

## Troubleshooting

### Error: "wenyan-mcp not found"

**Solution**: Install Wenyan MCP
```bash
npm install -g @wenyan-md/mcp
```

### Error: "invalid media_id"

**Solution**: Make sure you're using permanent material upload (the script handles this automatically)

### Error: "api unauthorized"

**Solution**: Check your WeChat account type and permissions. Some APIs require verified service account.

### Error: "access_token expired"

**Solution**: The script automatically refreshes tokens. If persists, check your App ID and Secret.

## Requirements

- Python 3.6+
- Node.js 14+ (for Wenyan MCP)
- WeChat Official Account (微信公众号)
- Evolink API Key

## References

- [Wenyan Guide](references/wenyan-guide.md) - Wenyan MCP documentation
- [API Guide](references/api-guide.md) - WeChat API details

## License

MIT
