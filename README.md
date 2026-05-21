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
- 🛡️ **全局安全层**（儿童内容安全，强制注入，不可绕过）

最终公式：**`Persona + Behavior + Scenario + Safety = 可用 Agent`**

> 所有角色均为原创设定，灵感来自经典动画的性格原型，不使用任何受版权保护的角色名称或形象。

---

## 🚀 Quick Start（30秒上手）

**方法一：直接复制使用（非开发者）**

1. 进入 `/personas` 选择一个角色文件夹
2. 打开 `prompt.md`，复制全部内容
3. 粘贴到 ChatGPT / Coze / Claude 的 System Prompt 中，开始对话

```
System: [粘贴角色 prompt]

User: 我今天不开心
```

**方法二：API 集成（开发者）**

```js
const response = await openai.chat.completions.create({
  model: "gpt-4o",
  messages: [
    { role: "system", content: bearHuggerPrompt },
    { role: "user", content: "我今天不开心" }
  ]
});
```

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
Agent（夜光）: 我就在你旁边，哪儿也不去。我们来想象一个很软很软的云朵床好不好…
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
├── templates/       # 组合模板（新手入口）
└── docs/            # 使用教程
```

详细结构说明见 [`docs/composable-system.md`](./docs/composable-system.md)

---

## 🛡️ Safety First

所有 Agent **默认强制包含**全局安全层，不可绕过：

- ✅ 不提供任何危险行为建议
- ✅ 不涉及成人内容
- ✅ 不替代家长 / 医生 / 心理咨询师角色
- ✅ 遇到风险信号 → 立即引导寻求大人帮助
- ✅ 不对孩子的情绪或行为做评判

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
- 与记忆系统结合（如 Coze 的 USER.md 机制）

详见 [`docs/composable-system.md`](./docs/composable-system.md)

---

## 🤝 Contributing

欢迎贡献新角色、新场景模块或行为模块！

请参考：
- [`personas/_template.md`](./personas/_template.md) — 人物设定标准模板
- [`CONTRIBUTING.md`](./CONTRIBUTING.md) — 贡献规范

**贡献原则：**
- 角色必须为原创设定，不得使用受版权保护的角色名称或形象
- 所有内容必须通过儿童安全审查
- Prompt 必须包含示例对话

---

## 📄 License

[CC BY-NC-SA 4.0](./LICENSE) — 署名 · 非商业 · 相同方式共享

你可以自由使用、修改和分发，但不可用于商业目的，且须保持相同协议。

---

## 🪄 Vision

> 这不仅是一个 prompt 库，  
> 而是**儿童 AI Companion 的人格操作系统**。

每个孩子都值得一个懂他的 AI 小伙伴。

---

