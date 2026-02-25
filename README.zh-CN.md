# 微信公众号文章发布工具

完整的微信公众号文章发布工作流。

[English](README.md) | 中文

## 功能特性

- ✍️ **Markdown 编辑** - 使用 Markdown 格式编写文章
- 🎨 **文颜排版** - 专业的微信公众号样式排版
- 🖼️ **AI 封面生成** - 使用 Evolink API 自动生成封面图
- 📤 **一键发布** - 直接发布到微信公众号草稿箱

## 工作流程

```
Markdown 文件 → 文颜排版 → Evolink 封面 → 微信草稿箱
```

## 安装

### 前置要求

```bash
# 安装文颜 MCP 用于专业排版
npm install -g @wenyan-md/mcp
```

### 安装本工具

```bash
mkdir -p ~/.openclaw/skills/wechat-article-publisher
git clone https://github.com/cheercheung/wechat-article-publisher.git ~/.openclaw/skills/wechat-article-publisher
```

## 快速开始

### 第一步：准备必要信息

你需要提供：

1. **微信公众号 App ID** - 在公众号后台 → 设置与开发 → 基本配置 中获取
2. **微信公众号 App Secret** - 同上位置获取
3. **Evolink API Key** - 在 https://evolink.io 注册获取

### 第二步：创建文章

创建带有 FrontMatter 的 Markdown 文件：

```markdown
---
title: 我的精彩文章
cover: /path/to/cover.jpg  # 可选 - 如不填写将自动生成
---

# 引言

这是我的文章内容。

## 第一节

- 要点 1
- 要点 2
- 要点 3

## 代码示例

```python
print("Hello 微信!")
```

> 这是一段引用
```

### 第三步：发布

```bash
python3 ~/.openclaw/skills/wechat-article-publisher/scripts/publish.py \
  --app-id "wx..." \
  --app-secret "..." \
  --evolink-key "sk-..." \
  --markdown ./my-article.md \
  --theme default \
  --author "你的名字"
```

## 使用示例

### 示例 1：基础用法

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

### 示例 2：自定义封面提示词

```bash
python3 scripts/publish.py \
  --app-id "$WECHAT_APP_ID" \
  --app-secret "$WECHAT_APP_SECRET" \
  --evolink-key "$EVOLINK_API_KEY" \
  --markdown ./article.md \
  --cover-prompt "一只可爱的太空龙虾拿着金币，数字艺术风格，鲜艳色彩"
```

### 示例 3：完整命令

```bash
python3 scripts/publish.py \
  --app-id "wxa7c34d64a265f9b2" \
  --app-secret "dcbecfc3f4d1d2ece2ae334955091a92" \
  --evolink-key "sk-2gKRdGs0ClOCSHsBIVLhPz6SDKrdYj2eSFwTudnDHnVGRizV" \
  --markdown ./openclaw-money-article.md \
  --theme default \
  --author "AI前沿观察" \
  --cover-prompt "关于AI赚钱的专业封面，现代数字艺术，16:9比例"
```

## 命令行选项

| 选项 | 必需 | 说明 |
|------|------|------|
| `--app-id` | 是 | 微信公众号 App ID |
| `--app-secret` | 是 | 微信公众号 App Secret |
| `--evolink-key` | 是 | Evolink API Key，用于封面生成 |
| `--markdown` | 是 | Markdown 文件路径 |
| `--theme` | 否 | 文颜主题（默认：default） |
| `--author` | 否 | 文章作者名称 |
| `--cover-prompt` | 否 | AI封面生成的自定义提示词 |

## 可用主题

文颜支持多种主题风格：

- `default` - 简洁经典
- `orangeheart` - 暖橙色调
- `phycat` - 物理猫主题
- 更多主题...

## Markdown 格式

### FrontMatter（可选）

```yaml
---
title: 文章标题        # 文章标题（FrontMatter中必需）
cover: /path/to/cover.jpg   # 封面图片路径（可选）
---
```

### 支持的 Markdown 语法

| Markdown | 效果 |
|----------|------|
| `# 标题` | H1 标题 |
| `## 标题` | H2 标题 |
| `**粗体**` | **粗体** |
| `*斜体*` | *斜体* |
| `- 项目` | 无序列表 |
| `1. 项目` | 有序列表 |
| `` `代码` `` | 行内代码 |
| ````代码```` | 代码块 |
| `> 引用` | 引用块 |
| `![描述](链接)` | 图片 |
| `[文字](链接)` | 链接 |

## 完整工作流程示例

### 场景：发布一篇关于 OpenClaw 赚钱的文章

**用户**：我想发一篇关于 OpenClaw 赚钱的文章

**AI**：好的！请提供：
1. 你的微信公众号 App ID
2. 你的微信公众号 App Secret
3. 你的 Evolink API Key

**用户**：[提供凭证]

**AI**：好的！让我为你创建文章...

[AI 编写 Markdown 内容]

```markdown
---
title: 他用一只"太空龙虾"月入4.3万美元
cover: /tmp/auto-generated-cover.jpg
---

# 他用一只"太空龙虾"月入4.3万美元

OpenClaw 是一个神奇的 AI 代理工具...

## 真实案例

- 案例 1：月入 4.3 万美元
- 案例 2：月入 8,200 美元
- 案例 3：2 个月 12.7 万美元

## 如何开始

```bash
git clone https://github.com/openclaw/openclaw
```

> 今天就开始你的旅程！
```

**AI**：正在发布...

```bash
python3 scripts/publish.py \
  --app-id "wx..." \
  --app-secret "..." \
  --evolink-key "sk-..." \
  --markdown ./openclaw-article.md \
  --author "科技博主"
```

**输出**：
```
步骤 1：使用文颜渲染 Markdown...
✓ 已渲染：他用一只"太空龙虾"月入4.3万美元
步骤 2：使用 Evolink 生成封面...
✓ 封面已生成：/tmp/cover_1234567890.jpg
步骤 3：获取微信 access token...
✓ 已获取 token
步骤 4：上传封面到微信...
✓ 封面上传成功：XYz5Fiw6o6F3vnz77zkTH...
步骤 5：发布到微信...

✅ 成功！
草稿 ID：XYz5Fiw6o6F3vnz77zkTHlCisnDL_mzOE7ey_2RWITX-di4c44q77r8tcunXxBdh
标题：他用一只"太空龙虾"月入4.3万美元

请登录微信公众号后台 → 草稿箱查看
```

**AI**：✅ 文章已发布！请登录微信公众号后台 → 草稿箱查看

## 常见问题

### 错误："wenyan-mcp not found"

**解决方案**：安装文颜 MCP
```bash
npm install -g @wenyan-md/mcp
```

### 错误："invalid media_id"

**解决方案**：确保使用永久素材上传（脚本已自动处理）

### 错误："api unauthorized"

**解决方案**：检查你的微信公众号类型和权限。部分接口需要认证服务号。

### 错误："access_token expired"

**解决方案**：脚本会自动刷新 token。如果问题持续，请检查 App ID 和 Secret。

## 环境要求

- Python 3.6+
- Node.js 14+（用于文颜 MCP）
- 微信公众号（订阅号或服务号）
- Evolink API Key

## 参考资料

- [文颜指南](references/wenyan-guide.md) - 文颜 MCP 文档
- [API 指南](references/api-guide.md) - 微信 API 详情

## 许可证

MIT
