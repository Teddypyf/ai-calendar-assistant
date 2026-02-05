# AI Calendar Assistant

通过邮件转发自动解读日程内容，同步到 Google Calendar，支持多邮箱账户。

## 功能特性

- 📧 **邮件转发处理**：通过将日程邮件转发到指定地址
- 🤖 **AI 解析**：使用 Claude API 自动识别日程信息（日期、时间、地点、参与人等）
- 📅 **Google Calendar 同步**：自动创建日历事件
- 🔗 **回复确认链接**：生成可点击的事件添加链接，发送回邮件
- 🌍 **多账户支持**：支持多个不同的邮件地址
- ☁️ **云端运行**：使用 GitHub Actions 定时执行，无需本地计算机运行

## 架构

```
邮件转发 → GitHub Actions → Claude AI 解析 → Google Calendar API → 生成回复链接 → 发送邮件
```

## 工作流程

1. 用户将日程邮件转发至特定邮箱（由系统配置）
2. GitHub Actions 定期检查邮件（基于 Webhook 或定时任务）
3. AI 解析邮件内容，提取日程信息
4. 自动创建 Google Calendar 事件
5. 生成 Google Calendar 添加链接
6. 向用户回邮件，包含可点击的事件确认链接

## 配置要求

### 1. Gmail API 设置
- Google Cloud 项目
- Gmail API 启用
- OAuth 2.0 凭证

### 2. Google Calendar API
- Calendar API 启用
- 服务账户或 OAuth 凭证

### 3. Claude API
- Anthropic API key

### 4. GitHub Secrets
- `GMAIL_CREDENTIALS`: Gmail OAuth 凭证 JSON
- `GOOGLE_CALENDAR_CREDENTIALS`: Calendar API 凭证
- `ANTHROPIC_API_KEY`: Claude API key
- `GMAIL_ADDRESS`: 接收邮件的 Gmail 地址
- `REPLY_EMAIL_PASSWORD`: 邮件回复密码或应用密码

## 部署

### GitHub Actions 配置
编辑 `.github/workflows/process-calendar-emails.yml` 配置工作流参数。

### 邮件转发设置
在你的邮件客户端设置规则，自动转发日程邮件到配置的邮箱。

## 环境变量

```bash
ANTHROPIC_API_KEY=<your-claude-api-key>
GMAIL_ADDRESS=<your-gmail-address>
```

## 使用示例

1. 转发日程邮件到配置的邮箱
2. GitHub Actions 自动处理（或手动触发）
3. 收到回邮，包含 Google Calendar 事件确认链接
4. 点击链接添加事件到日历

## 项目结构

```
.
├── .github/workflows/
│   └── process-calendar-emails.yml      # GitHub Actions 工作流
├── src/
│   ├── email_handler.py                 # 邮件读取和解析
│   ├── ai_parser.py                     # Claude AI 日程解析
│   ├── calendar_sync.py                 # Google Calendar 同步
│   ├── email_sender.py                  # 邮件回复发送
│   └── main.py                          # 主程序入口
├── requirements.txt                      # Python 依赖
├── README.md                             # 本文件
└── config.example.json                   # 配置示例
```

## 许可证

MIT
