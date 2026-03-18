# ai-daily

OpenClaw Skill for AI 洞察日报 - 每日自动推送 AI 日报

## 功能

- 从官方 RSS 源抓取每日 AI 日报
- 提取标题 + 分段 + 列表，格式化输出
- 支持推送到多个 webhook 渠道（Bark/企业微信/飞书/钉钉）
- 支持自定义默认获取条数，命令行可覆盖
- 支持 GitHub Actions 定时自动推送

## 配置

### OpenClaw 本地使用

```bash
# 编辑配置
~/.openclaw/skills/ai-daily/config.sh

export AI_DAILY_WEBHOOKS="https://api.day.app/your-token https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=xxx"
export AI_DAILY_DEFAULT_COUNT=1
```

```bash
# 使用
source ~/.openclaw/skills/ai-daily/config.sh
~/.openclaw/skills/ai-daily/scripts/fetch.sh

# 获取 5 条最新
~/.openclaw/skills/ai-daily/scripts/fetch.sh 5
```

### GitHub Actions 定时推送

1. 在 GitHub 仓库 Settings → Secrets and variables → Actions → New repository secret
   - Name: `AI_DAILY_WEBHOOKS`
   - Value: 你的推送地址，多个空格分隔，例如:
     ```
     https://api.day.app/your-token https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=xxx
     ```

2. 定时任务默认每天 **北京时间 早上 8:00** 自动推送当日 AI 日报
   - 如果需要修改时间，编辑 `.github/workflows/daily-push.yml` 修改 cron 表达式

## 输出格式

获取今日日报：

```
**AI 洞察日报 - 2026-03-18日刊**

产品与功能更新
- OpenAI 发布推理速度更快的轻量模型。
- Midjourney 开启 V8 模型社区测试。
- 谷歌 上线 NotebookLM 电影级视频功能。
- Gamma 发布 AI 原生设计工具套件。
- Lightricks 发布物理级写实视频模型。

前沿研究
- DeepMind 扩容蛋白质复合物数据库。
- AI 通过新框架自主进化出社会规则。

> 完整内容：https://ai.hubtoday.app//2026-03/2026-03-18/
```

## 信息来源

- 原 RSS 来源：[AI 洞察日报](https://justlovemaki.github.io/CloudFlare-AI-Insight-Daily/rss.xml) by [justlovemaki](https://github.com/justlovemaki)

## License

MIT
