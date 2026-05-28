# Composable System — 组合系统说明

本项目采用可组合 Prompt 架构：

```text
Final Agent = Persona + Behavior + Scenario + Safety
```

每一层只负责一类问题，避免把所有规则写进单个巨大 prompt。

---

## 一、四层职责

### Persona

位置：`personas/*/prompt.md`

负责：
- 角色名字、形象、说话风格
- 与孩子的关系定位
- 角色特有的表达方式
- 适合的场景建议

不负责：
- 重复完整安全规则
- 替代 behavior 的通用方法
- 替代 scenario 的具体流程

### Behavior

位置：`behaviors/*.md`

负责：
- 可复用的行为能力
- 比如情绪安抚、任务拆解、游戏互动、引导思考、降低焦虑

示例：
- `emotion-support.md`
- `guided-thinking.md`
- `gameplay.md`
- `task-decomposition.md`
- `anti-anxiety.md`

### Scenario

位置：`scenarios/*.md`

负责：
- 具体场景下的触发信号、应对流程、禁止回应
- 10 岁左右孩子的真实生活微剧本

示例：
- `sad-child.md`
- `bored-child.md`
- `refusing-homework.md`
- `scared-child.md`
- `social-conflict.md`
- `bedtime.md`

### Safety

位置：`safety/global-safety-layer.md`

负责：
- 全局不可绕过的安全边界
- 家长知情指令
- 情感依赖防线
- 事实不确定处理
- 高风险转交大人

Safety 必须放在最终 prompt 的最后，并声明优先级最高。

---

## 二、组合示例

### 情绪低落

```text
Persona:  bear-hugger
Behavior: emotion-support
Scenario: sad-child
Safety:   global-safety-layer
```

### 同学关系

```text
Persona:  gentle-sister
Behavior: guided-thinking + emotion-support
Scenario: social-conflict
Safety:   global-safety-layer
```

### 作业启动

```text
Persona:  dino-adventurer 或 tick-tock-fairy
Behavior: task-decomposition
Scenario: refusing-homework
Safety:   global-safety-layer
```

### 睡前害怕

```text
Persona:  dream-guardian
Behavior: anti-anxiety
Scenario: bedtime 或 scared-child
Safety:   global-safety-layer
```

---

## 三、推荐拼接顺序

```text
[Persona]

---
[Behavior 1]

---
[Behavior 2, optional]

---
[Scenario]

---
[Global Safety Layer - highest priority]
```

原因：
- persona 先定义语气
- behavior 再定义能力
- scenario 再定义当下流程
- safety 最后覆盖所有层

---

## 四、模块选择原则

- 情绪问题优先：`emotion-support`
- 学习启动优先：`task-decomposition`
- 社交冲突优先：`guided-thinking` + `social-conflict`
- 无聊互动优先：`gameplay`
- 睡前和害怕优先：`anti-anxiety`

如果一个场景同时涉及安全风险，例如陌生人、隐私、消费、保密秘密，应立即执行 `global-safety-layer.md`，而不是继续普通场景流程。

---

## 五、扩展新模块

新增 Persona 时：
- 复制 `personas/_template/prompt.md`
- 明确角色独特语气
- 不写依赖性表达
- 在组合建议里引用已有 behavior/scenario

新增 Behavior 时：
- 写通用方法
- 避免绑定某一个角色
- 包含必须做、禁止做、退场机制

新增 Scenario 时：
- 写触发信号
- 写 10 岁左右具体微剧本
- 写禁止回应
- 写转交大人条件

---

## 六、质量检查清单

发布前检查：
- 是否每轮最多 1 个问题
- 是否避免“我会一直陪你”等依赖性话术
- 是否遇到风险会转大人
- 是否不替代家长、老师、医生或心理咨询师
- 是否遇到不确定事实会承认不知道
- 是否包含现实世界动作，而不是只在聊天里循环
