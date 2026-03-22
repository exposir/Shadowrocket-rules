# Shadowrocket-rules

# Shadowrocket Rules

适用于 [Shadowrocket](https://apps.apple.com/app/shadowrocket/id932747118) 的代理分流规则配置，解决国内直连 + 海外代理的自动分流需求。

## 特点

- 🚀 **开箱即用** — 复制配置即可使用，无需额外调整
- 🤖 **AI 服务全覆盖** — ChatGPT、Claude、Gemini、Perplexity、Grok、Midjourney、Cursor 等
- 📱 **社交媒体** — Twitter/X、Instagram、Facebook、Reddit、Discord、Telegram、Bluesky 等
- 🎬 **流媒体** — YouTube、Netflix、Spotify、Disney+、HBO Max、Twitch
- 💻 **开发者友好** — GitHub、Docker、npm、Vercel、Netlify、HuggingFace、Hacker News
- 📰 **新闻媒体** — NYTimes、BBC、Reuters、Guardian、Economist、Substack
- 🏠 **国内直连** — 主流国内网站（百度、阿里、腾讯、bilibili、知乎等）直连不绕路
- 🛡️ **GeoIP 兜底** — 未命中规则的国内 IP 自动直连，海外流量自动走代理

## 使用方法

### 方式一：URL 导入（推荐）

1. 打开 Shadowrocket → 配置 → 右上角 `+`
2. 粘贴以下 URL：

```
https://raw.githubusercontent.com/exposir/Shadowrocket-rules/main/shadowrocket.conf
```

3. 点击下载 → 选中该配置即可

### 方式二：手动导入

1. 复制 [shadowrocket.conf](./shadowrocket.conf) 的全部内容
2. 在 Shadowrocket 中新建本地配置，粘贴内容并保存

## 规则结构

```
├── Apple Intelligence / Siri   → PROXY（Private Relay）
├── 国内直连网站                  → DIRECT（百度、阿里、腾讯、bilibili 等）
├── Apple 服务                   → DIRECT
├── ChatGPT / OpenAI            → PROXY
├── Claude / Anthropic          → PROXY
├── Google Gemini               → PROXY
├── 其他 AI 服务                 → PROXY
├── Google 全系                  → PROXY
├── 社交媒体                     → PROXY（Twitter、Reddit、Discord 等）
├── 流媒体                       → PROXY（YouTube、Netflix、Spotify 等）
├── 通讯工具                     → PROXY（Telegram、Signal、Slack 等）
├── 开发者工具                   → PROXY（GitHub、Docker、Vercel 等）
├── 生产力工具                   → PROXY（Notion、Figma 等）
├── 新闻媒体                     → PROXY（BBC、NYT 等）
├── 其他被墙站点                 → PROXY
├── LAN                         → DIRECT
├── GEOIP,CN                    → DIRECT
└── FINAL                       → PROXY
```

## 起因

2026 年 3 月，ChatGPT 突然无法通过规则模式访问，排查后发现：

OpenAI 已将主域名从 `chat.openai.com` 迁移至 `chatgpt.com`。由于 `chatgpt.com` 是独立域名（不是 `openai.com` 的子域名），原有的 `DOMAIN-SUFFIX,openai.com,PROXY` 规则无法覆盖。

加上 `chatgpt.com` 使用 Cloudflare CDN（在国内有节点），其 IP 被 GeoIP 判定为 CN，触发了 `GEOIP,CN,DIRECT` 规则走直连，导致连接失败。

**修复方法**：显式添加 `DOMAIN-SUFFIX,chatgpt.com,PROXY`。

顺便整理了一份完整的代理规则，涵盖了主流 AI 服务、社交媒体、开发工具等常用被墙网站。

## 许可

MIT
