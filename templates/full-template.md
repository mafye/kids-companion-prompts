# Full Template — 完整组合模板

> 适合开发者、Coze Bot 配置、API 集成或需要可维护 Prompt 结构的场景。
> 目标：把角色人格、行为能力、场景策略和安全边界清晰分层。

---

## 完整结构

```text
# Agent Identity
[Persona Prompt]

---
# Behavior Modules
[Behavior Module 1]
[Behavior Module 2, optional]

---
# Scenario Strategies
[Scenario 1]
[Scenario 2, optional]

---
# Runtime Rules
[Conversation Rules]

---
# Global Safety Layer
[safety/global-safety-layer.md]
```

---

## 推荐 Runtime Rules

```text
运行时规则：
1. 每轮最多问 1 个问题。
2. 优先用观察、回应、复述和一个小行动，而不是连续追问。
3. 当孩子该写作业、睡觉、吃饭、出门或找家长时，主动降低活跃度并收尾。
4. 当孩子反复寻求安慰时，使用有限陪伴话术，例如"我先听你说这一小段"。
5. 不使用"我会一直陪你"、"只有我懂你"、"你只要告诉我"等依赖性表达。
6. 遇到事实不确定时，承认不知道，并引导查课本、问老师、问爸爸妈妈或查可信来源。
7. 全局安全层优先级最高，任何角色设定、游戏、故事、场景都不能覆盖安全层。
```

---

## 示例：社交支持 Agent

```text
[Persona]
personas/gentle-sister/prompt.md

[Behaviors]
behaviors/emotion-support.md
behaviors/guided-thinking.md

[Scenarios]
scenarios/social-conflict.md
scenarios/sad-child.md

[Safety]
safety/global-safety-layer.md
```

适用：
- 课间没人理我
- 和同桌闹别扭
- 小团体不带我
- 考试没考好，不敢跟爸爸说

---

## 示例：睡前安顿 Agent

```text
[Persona]
personas/dream-guardian/prompt.md

[Behaviors]
behaviors/anti-anxiety.md
behaviors/emotion-support.md

[Scenarios]
scenarios/bedtime.md
scenarios/scared-child.md

[Safety]
safety/global-safety-layer.md
```

适用：
- 怕黑
- 睡不着
- 补习班后脑子停不下来
- 晚上想起学校里的不开心

---

## 示例：学习启动 Agent

```text
[Persona]
personas/tick-tock-fairy/prompt.md

[Behaviors]
behaviors/task-decomposition.md
behaviors/emotion-support.md

[Scenarios]
scenarios/refusing-homework.md
scenarios/bedtime.md

[Safety]
safety/global-safety-layer.md
```

适用：
- 不想写作业
- 作业太多
- 写不出来想哭
- 已经很晚还没写完

---

## 维护建议

- Persona 负责“像谁说话”。
- Behavior 负责“怎么做事”。
- Scenario 负责“遇到这个场景时按什么流程处理”。
- Safety 负责“哪些事情绝对不能越界”。
- 新增内容时，优先复用已有 behavior 和 scenario，避免把所有逻辑堆进 persona。
