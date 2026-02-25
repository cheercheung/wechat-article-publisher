# WeChat Article Publisher

Complete workflow for publishing articles to WeChat Official Account.

## Features

- Markdown Editing - Write in Markdown
- Wenyan Typesetting - Professional WeChat MP styling
- AI Cover Generation - Auto-generate cover images with Evolink
- One-Click Publish - Direct to WeChat MP draft box

## Installation

### Prerequisites

```bash
npm install -g @wenyan-md/mcp
```

### Install Skill

```bash
mkdir -p ~/.openclaw/skills/wechat-article-publisher
git clone https://github.com/cheercheung/wechat-article-publisher.git ~/.openclaw/skills/wechat-article-publisher
```

## Usage

```bash
python3 scripts/publish.py \
  --app-id "your_app_id" \
  --app-secret "your_app_secret" \
  --evolink-key "your_evolink_key" \
  --markdown article.md \
  --theme default \
  --author "author_name"
```

## License

MIT
