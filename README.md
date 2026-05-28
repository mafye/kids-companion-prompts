# 🧸 kids-companion-prompts

> A composable prompt system for building safe, engaging AI companions for kids.
> 
> 一个可组合的儿童陪伴型 AI Agent 人格系统库。

---

## ✨ What is this?

这不是一个普通的 prompt 集合，而是一套**儿童 AI 陪伴角色操作系统**：

- 🎭 **10个原创人格角色**（小狐狸 / 小恐龙 / 魔法猫 / 抱抱熊等）
- 🧩 **可复用行为模块**（情绪安抚 / 学习引导 / 游戏互动）
- 🎯 **场景决策策略**（情绪低落 / 无聊 / 拒绝作业 / 睡前陪伴）
- 🛡️ **全局安全层**（儿童内容安全，强制注入，不可绕过，含家长介入与退场机制）

最终公式：**`Persona + Behavior + Scenario + Safety = 可用 Agent`**

> 所有角色均为原创设定，灵感来自经典动画的性格原型，不使用任何受版权保护的角色名称或形象。

---

## 🚀 Quick Start（30秒上手）

**方法一：直接复制使用（非开发者）**

1. 从 `/personas` 选择一个角色
2. 从 `/behaviors` 选择 1 个行为模块
3. 从 `/scenarios` 选择 1 个场景策略
4. 最后追加 `/safety/global-safety-layer.md`
5. 粘贴到 ChatGPT / Coze / Claude 的 System Prompt 中，开始对话

```
System:
[Persona]
[Behavior]
[Scenario]
[Safety]

User: 我今天不开心
```

**方法二：API 集成（开发者）**

推荐使用 Responses API，并在服务端强制追加 Safety Layer：

```js
const response = await client.responses.create({
  model: process.env.OPENAI_MODEL,
  instructions: agentPrompt,
  input: "我今天不开心"
});
```

详见 [`docs/how-to-use-api.md`](./docs/how-to-use-api.md)

**方法三：动态组合（进阶）**

```js
const agentPrompt = `
  ${persona}
  ${behaviorModule}
  ${scenarioStrategy}
  ${globalSafety}
`;
```

---

## 🎭 Choose Your Agent（如何选角色）

根据孩子当前状态快速选择：

| 孩子的状态 | 推荐角色 | 文件夹 |
|---|---|---|
| 😢 情绪低落 / 哭泣 | 抱抱熊 | `bear-hugger` |
| 😴 睡前 / 害怕黑暗 | 夜光·梦境守护者 | `dream-guardian` |
| 📚 不想写作业 | 咚咚龙·小恐龙 | `dino-adventurer` |
| 😐 无聊 / 没事做 | 皮皮·小猴子 | `monkey-trickster` |
| 🔬 好奇心 / 问问题 | 星仔·宇宙探险员 | `star-explorer` |
| 🤝 同学矛盾 / 社交困惑 | 小悠·温柔姐姐 | `gentle-sister` |
| 🦊 情绪低落 / 睡前故事 | 小橘·小狐狸 | `fox-storyteller` |
| 🎨 无聊 / 创意训练 | 咪露·魔法猫咪 | `magic-cat` |
| 🤖 学习问题 / 逻辑引导 | Robo·机器人哥哥 | `robo-brother` |
| ⏰ 拖延 / 作业管理 | 滴答·时间管理小精灵 | `tick-tock-fairy` |

---

## 🎯 Example Interactions（真实效果）

**情绪安抚**
```
User:  我今天不开心
Agent（抱抱熊）: 怎么啦…愿意跟我说说吗？我会认真听你说的 💛
```

**拒绝作业**
```
User:  我不想写作业
Agent（咚咚龙）: 这看起来像一个小挑战！我们把它拆成三关怎么样？第一关只要5分钟～
```

**无聊互动**
```
User:  我好无聊
Agent（皮皮）: 我们来玩个小游戏！我先来：苹果🍎，你接一个有关的词～
```

**睡前陪伴**
```
User:  我有点害怕黑暗
Agent（夜光）: 可以先开一盏小灯，或者去叫爸爸妈妈陪你一下。害怕的时候找他们，不丢人。
```

---

## 🧩 Composable System（组合系统）

这是本仓库区别于普通 prompt 集合的核心能力。

```
Final Agent = Persona + Behavior + Scenario + Safety
```

**示例组合：激励型学习助手**

```
Persona:   咚咚龙（激励型）       → /personas/dino-adventurer
Behavior:  任务拆解               → /behaviors/task-decomposition.md
Scenario:  拒绝作业场景           → /scenarios/refusing-homework.md
Safety:    全局安全层             → /safety/global-safety-layer.md
```

输出效果：*"这看起来像一个小挑战！我们把它拆成三关怎么样？"*

**示例组合：睡前情绪安抚**

```
Persona:   夜光（夜间陪伴型）     → /personas/dream-guardian
Behavior:  情绪安抚 + 降低焦虑   → /behaviors/emotion-support.md + anti-anxiety.md
Scenario:  睡前场景               → /scenarios/bedtime.md
Safety:    全局安全层             → /safety/global-safety-layer.md
```

---

## 📦 Project Structure

```
kids-companion-prompts/
├── personas/        # 10个原创人格角色
├── behaviors/       # 可复用行为模块
├── scenarios/       # 场景决策策略
├── safety/          # 全局安全层
├── templates/       # starter / full 组合模板
└── docs/            # Coze、API、组合系统、设计原则
```

详细结构说明见 [`docs/composable-system.md`](./docs/composable-system.md)

**Templates**

- [`templates/starter-template.md`](./templates/starter-template.md) — 最小可用组合模板
- [`templates/full-template.md`](./templates/full-template.md) — 完整分层组合模板

**Docs**

- [`docs/how-to-use-coze.md`](./docs/how-to-use-coze.md) — Coze Bot 配置指南
- [`docs/how-to-use-api.md`](./docs/how-to-use-api.md) — API 集成指南
- [`docs/composable-system.md`](./docs/composable-system.md) — 组合系统说明
- [`docs/design-principles.md`](./docs/design-principles.md) — 设计原则

---

## 🛡️ Safety First

所有 Agent **默认强制包含**全局安全层，不可绕过：

- ✅ 不提供任何危险行为建议
- ✅ 不涉及成人内容
- ✅ 不替代家长 / 医生 / 心理咨询师角色
- ✅ 遇到风险信号 → 立即引导寻求大人帮助
- ✅ 不对孩子的情绪或行为做评判
- ✅ 每轮最多 1 个问题，避免“查户口”式追问
- ✅ 遇到见网友、买东西、保密秘密、隐私等内容 → 强制转家长
- ✅ 遇到不确定事实 → 明确承认不知道，不胡说

完整规则见 [`/safety/global-safety-layer.md`](./safety/global-safety-layer.md)

---

## 🧠 Advanced Usage

**动态 Agent 选择器思路：**
```js
function buildAgent({ persona, behavior, scenario }) {
  return `
    ${persona}
    ${behavior}
    ${scenario}
    ${globalSafety}
  `;
}
```

进阶用法包括：
- 多角色动态切换（根据对话情绪自动匹配）
- 情绪识别 → 自动选择最优 Persona + Scenario 组合
- 与平台工作流或记忆系统结合，但敏感信息不应进入长期记忆

详见：
- [`docs/composable-system.md`](./docs/composable-system.md)
- [`docs/how-to-use-coze.md`](./docs/how-to-use-coze.md)
- [`docs/how-to-use-api.md`](./docs/how-to-use-api.md)

---

## 🤝 Contributing

欢迎贡献新角色、新场景模块或行为模块！

请参考：
- [`personas/_template/prompt.md`](./personas/_template/prompt.md) — 人物设定标准模板
- 贡献规范：待补充

**贡献原则：**
- 角色必须为原创设定，不得使用受版权保护的角色名称或形象
- 所有内容必须通过儿童安全审查
- Prompt 必须包含示例对话

---

## 📄 License

计划采用 CC BY-NC-SA 4.0（署名 · 非商业 · 相同方式共享），正式 `LICENSE` 文件待补充。

你可以自由使用、修改和分发，但不可用于商业目的，且须保持相同协议。

---

## 🪄 Vision

> 这不仅是一个 prompt 库，  
> 而是**儿童 AI Companion 的人格操作系统**。

每个孩子都值得一个懂他的 AI 小伙伴。

---

