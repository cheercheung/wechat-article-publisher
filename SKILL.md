---
name: wechat-article-publisher
description: Complete WeChat Official Account article publishing workflow. Integrates Markdown editing, Wenyan typesetting, Evolink cover generation, and WeChat MP publishing. Use when user wants to publish articles to their WeChat public account. Requires WeChat AppID, AppSecret, and Evolink API Key.
---

# WeChat Article Publisher

Complete workflow for publishing articles to WeChat Official Account.

## What This Skill Does

This skill provides a **one-command solution** for publishing to WeChat MP:

```
Markdown File → Wenyan Typesetting → Evolink Cover → WeChat Draft
```

## Installation

### Prerequisites

```bash
# Install Wenyan MCP (for professional typesetting)
npm install -g @wenyan-md/mcp
```

### Install This Skill

```bash
mkdir -p ~/.openclaw/skills/wechat-article-publisher
unzip wechat-article-publisher.skill -d ~/.openclaw/skills/wechat-article-publisher
```

## Required Credentials

**You MUST ask user for:**
1. WeChat App ID (`wx...`)
2. WeChat App Secret
3. Evolink API Key (for cover generation)

## Usage

### Step 1: Create Markdown File

```markdown
---
title: 文章标题
cover: /path/to/cover.jpg  # optional - will auto-generate if not provided
---

# 正文标题

文章内容支持：

- **粗体**
- *斜体*
- `代码`
- 列表

## 代码示例

```python
print("Hello")
```
```

### Step 2: Publish

```bash
python3 scripts/publish.py \
  --app-id "wx..." \
  --app-secret "..." \
  --evolink-key "sk-..." \
  --markdown article.md \
  --theme default \
  --author "作者名"
```

## Workflow

```
User: 我要发一篇文章
You:  请提供：1) WeChat AppID 2) AppSecret 3) Evolink Key
User: [provides credentials]
You:  请写Markdown内容，或告诉我主题我来写
User: [provides markdown file or topic]
You:  [runs publish.py]
      ✓ Markdown rendered with Wenyan
      ✓ Cover generated with Evolink  
      ✓ Published to WeChat draft box
```

## Features

| Feature | Tool | Description |
|---------|------|-------------|
| Markdown Typesetting | Wenyan MCP | Professional WeChat MP styling |
| Cover Generation | Evolink API | AI-generated 16:9 cover images |
| Image Upload | WeChat API | Permanent material upload |
| Draft Publishing | WeChat API | Direct to MP draft box |

## Themes

Wenyan supports multiple themes:
- `default` - 简洁经典
- `orangeheart` - 暖橙色调
- `phycat` - 物理猫主题
- And more...

## Content Format

### FrontMatter (Optional)
```yaml
---
title: 文章标题        # Required - article title
cover: /path/cover.jpg # Optional - auto-generated if not provided
---
```

### Markdown Syntax
- `#` H1, `##` H2, `###` H3
- `**bold**`, `*italic*`
- `- list`, `1. ordered list`
- `> quote`
- `` `code` ``, ````code block````
- `![alt](url)` images
- `[text](url)` links

## Error Handling

| Error | Solution |
|-------|----------|
| Wenyan not found | Run `npm install -g @wenyan-md/mcp` |
| Invalid media_id | Cover uploaded as permanent material |
| API unauthorized | Check WeChat account permissions |
| Cover generation failed | Check Evolink API key |

## References

- [references/wenyan-guide.md](references/wenyan-guide.md) - Wenyan MCP documentation
- [references/api-guide.md](references/api-guide.md) - WeChat API details
