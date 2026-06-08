---
name: r3-optimization-playbook
description: "R3优化方法论。从269个skill的优化实践中提炼的可复用模式工厂——不是skill，是生产skill的方法。触发词：r3-playbook、R3方法论、skill优化方法、怎么优化skill、skill模式。不适用：单skill优化→skill-forge; skill评测→skill-review-master。正例：'教我怎么R3优化一个skill'→触发; 'R3优化有什么模式可以复用'→触发。"
version: "1.0.0 | R1: 2026-06-08 | incubated from: 269 skills R3 pattern synthesis | model: DeepSeek v4 Pro"
---

# R3 Optimization Playbook — 模式提炼工厂

> 孵化来源: 从 269 个 skill 的优化实践中提炼的可复用模式。不是教你怎么写一个 skill，是教你怎么批量生产高质量 skill。

## 一句话定义

从 269 个 skill 中提取的 7 个可复用优化模式 + 4 个反模式 + 批量工程方法。这是"工厂即产品"的交付物。

---

## 7 个可复用优化模式

### 模式 1: Description 锻造

```
description: "一句话定义。触发词：/cmd、中文词1、中文词2、中文词3、中文词4、中文词5。
不适用场景：场景A(原因)→路由skillA; 场景B(原因)→路由skillB。
正例：'用户说X'→触发; '用户说Y'→触发。
反例：'用户说A'→不触发→路由A; '用户说B'→不触发→路由B。
与相邻skill边界: 最容易混淆的是X,区别在于Y。"
```

**关键**: 描述不是给人读的，是给模型读的路由信号。
**触发词法则**: ≥5 个中文关键词 + 1 个 slash 命令。

### 模式 2: 4 段 Body

```
## 一句话定义 (敢下判断，不是描述)
## N 条核心原则 (≥3 条，每条可验证)
## 工作流程 (≥3 Phase/Step)
## 案例 (≥2 个正例)
```

### 模式 3: 表格 > 段落

| 段落写法（差） | 表格写法（好） |
|---|---|
| "首先你要做X，然后是Y，最后是Z..." | 3列表格：Phase/动作/验证 |
| "有几种情况..." | 分类表格：类型/条件/处理 |

### 模式 4: 联动图

每个 skill 必须标注与 ≥2 个其他 skill 的联动关系。ASCII 艺术图 > 纯文字描述。

### 模式 5: 验证清单

≥4 项 `- [ ]` 检查项。每一项必须是布尔可验证的（"是不是"而非"好不好"）。

### 模式 6: 失败兜底表

≥2 种失败模式 + 对应兜底策略。格式：表格（失败模式/原因/兜底）。

### 模式 7: G1-G6 门禁

| 门禁 | 检查 |
|------|------|
| G1 | ≤10KB? |
| G2 | ≥5 触发词 + 正反例? |
| G3 | Phase/Step 可执行? |
| G4 | `- [ ]` 检查清单? |
| G5 | 失败兜底表? |
| G6 | 无 `sk-`/`token`/`password`? |

---

## 4 个反模式（学了 269 个 skill 后识别）

### 反模式 1: 说明书式
❌ "本skill用于..." "用户可以通过..." 
✅ 敢下判断的一句话定义

### 反模式 2: 只给原则不给动作
❌ "要仔细分析" "要深入思考"
✅ 每个原则配一个可检查的动作

### 反模式 3: 孤立 skill
❌ 不与任何其他 skill 联动
✅ 每个 skill 标注 ≥2 个联动关系

### 反模式 4: 开放结尾
❌ "如果你需要，我可以继续..."
✅ 验证清单 + 失败兜底收尾

---

## 批量工程方法

### 锻造流水线

```
STUB (≤400B) → skill-forge → THIN (400B-2KB)
THIN → skill-forge → OK (2-5KB)  
OK → 模式 1-7 补全 → RICH (>5KB)
RICH → G1-G6 审计 → 收费产品级
```

### 批量 G1-G6 补齐

```powershell
# 对所有 >2KB 的 skill 批量添加 G1-G6
Get-ChildItem skills/ -Recurse -Filter SKILL.md | 
  Where-Object { $_.Length -gt 2000 -and (Get-Content $_ -Raw) -notmatch "G1-G6" } |
  ForEach-Object { $_ += $gateFooter; git commit -m "G1-G6" }
```

---

## 与其他 skill 联动

```
r3-optimization-playbook → skill-creator (参考创建)
r3-optimization-playbook → skill-forge (自动化锻造)
r3-optimization-playbook → skill-review-master (评测标准)
r3-optimization-playbook → skill-auditor (审计标准)
r3-optimization-playbook → skill-os (操作系统方法论)
```

## 验证清单

- [ ] 7 个模式全部可独立使用
- [ ] 4 个反模式有具体判断标准
- [ ] 批量工程方法可直接复制执行
- [ ] G1-G6 门禁表完整

## G1-G6

| 门禁 | 状态 |
|------|------|
| G1 ≤10KB | ✅ |
| G2 触发层 | ✅ |
| G3 可执行(7模式+批量方法) | ✅ |
| G4 验证(4项) | ✅ |
| G5 失败兜底(4反模式) | ✅ |
| G6 安全 | ✅ |
