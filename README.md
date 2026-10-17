# 国内使用 Claude Code 指南（2026）

> 本指南由 [TeamoRouter](https://teamorouter.com/zh) 维护，文中会提到我们，但各种方案的利弊都如实列出，你可以自己选。

Claude Code 是 Anthropic 官方的命令行编程助手。工具本身免费，要花钱的是背后调用的 Claude 模型。国内用户主要卡在三件事上：**账号**（Anthropic 的支持地区不含中国大陆）、**付款**（官方只收海外信用卡）、**网络**。下面按顺序说清楚。

## 一、三种用法对比

| 方式 | 要 Claude 账号吗 | 要海外卡吗 | 主要风险 | 适合谁 |
|---|---|---|---|---|
| 官方订阅 Pro / Max | 要 | 要 | 大陆 IP 登录易被封号，封号后月费一般不退 | 本来就在海外的人 |
| 虚拟卡订阅官方 | 要 | 虚拟卡 | 要实名、有手续费，卡段可能被拒，平台可能停服（如 2025 年 7 月的野卡） | 一定要用官方网页版的人 |
| API 网关按量付费 | 不要 | 不要 | 要挑真走官方模型的网关 | 写代码、用量不稳定、人在国内 |

## 二、安装 Claude Code

需要 Node.js 18 或以上：

```bash
npm install -g @anthropic-ai/claude-code
claude --version
```

## 三、用 API 网关接入（不需要 Claude 账号）

以 TeamoRouter 为例：

1. 注册，在控制台充值（支付宝或刷卡，最低 5 美元；手上有 USDT 的也可以直接付，见 [USDT 充值步骤](https://teamorouter.com/zh/blogs/pay-claude-with-usdt)），创建 API Key。
2. 按[接入文档](https://teamorouter.com/zh/docs/install-claude-code)设置两个环境变量：`ANTHROPIC_BASE_URL` 和 `ANTHROPIC_AUTH_TOKEN`。
3. 在项目目录里运行 `claude`，模型 ID 和官方一致，比如 `claude-sonnet-5-5`、`claude-opus-5-5`。

想在 Claude Code、Codex、Gemini CLI 之间一键切换配置，可以用 [CC Switch](https://teamorouter.com/zh/docs/install-cc-switch)。桌面端见 [Claude Desktop 接入](https://teamorouter.com/zh/docs/install-claude-desktop)。

## 四、怎么判断网关靠不靠谱

不管用哪家，都建议当场验这三件事：

1. **模型是不是真的**：请求 `claude-opus-5-5`，看回包里的 `model` 字段是不是它，思考过程是不是完整。
2. **缓存有没有正常计费**：Claude Code 一个会话里七成以上的输入是重复发送的上下文，走缓存价。账单里缓存读写一直是 0 的平台，同样的活会贵好几倍。
3. **能不能小额试**：先充几美元跑一天，看账单明细再决定。

## 五、怎么省钱

- **模型分级**：日常用 Sonnet，难题再切 Opus，最难的任务才用 Fable。
- **订阅还是按量**：先按量用一周，日均超过 3 到 7 美元（Max 100 / 200 美元折算到每天），订阅更划算；低于这个数，按量更省。
- **别让会话无限变长**：上下文越长，每轮花得越多，任务换了就开新会话。

## 六、常见问题

**提示 403 或地区不支持？** 用官方账号时，通常是当前 IP 落在不支持的地区；用 API 网关不涉及这个问题。

**官方账号被封了怎么办？** 可以在 Anthropic 官方帮助中心申诉，但不保证解封；别马上用同一张卡、同一个网络环境注册新号。

**能用 Codex 吗？** 同一个 Key 也能用 GPT 系列，见 [Codex CLI 安装教程](https://teamorouter.com/zh/blogs/codex-cli-install-guide)。

## 相关阅读

- [Claude 国内怎么用](https://teamorouter.com/zh/blogs/claude-guonei-zenme-yong)
- [Claude API 中转](https://teamorouter.com/zh/claude-api-zhongzhuan)
