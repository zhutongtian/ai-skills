# 小初高全科题目知识点解析助手 — 各平台部署指南

本文档说明如何将 `skill-knowledge-point-analyzer.md` 部署到不同平台。

---

## 一、SOLO 平台

### 方式1：作为 Custom Skill 使用

1. 打开 SOLO 设置 → Skills → 创建新 Skill
2. **Skill 名称**：`小初高全科题目知识点解析助手`
3. **Skill 描述**：`输入小初高任意学科题目，自动识别学段学科，精准拆解知识点、考点及课本章节，不提供答案`
4. **Skill Prompt**：将 `skill-knowledge-point-analyzer.md` 的全部内容粘贴到 Prompt 输入框
5. 保存即可

### 方式2：作为 System Prompt 使用

在 SOLO 对话的 System Prompt 设置中，将 `skill-knowledge-point-analyzer.md` 全文粘贴即可。

---

## 二、Trae 平台

### 作为自定义规则使用

1. 打开 Trae → 设置 → Custom Rules（自定义规则）
2. 点击「添加规则」
3. **规则名称**：`小初高知识点解析`
4. **规则内容**：将 `skill-knowledge-point-analyzer.md` 全文粘贴
5. **触发条件**（如支持）：添加关键词 `题目、试题、习题、知识点`
6. 保存

### 作为 Project Rule 使用

在项目根目录创建 `.trae/rules/knowledge-analyzer.md`，将 Skill 内容粘贴进去，Trae 会自动加载。

---

## 三、Claude Code 平台

### 方式1：CLAUDE.md 项目指令

在项目根目录创建 `CLAUDE.md` 文件，写入：

```markdown
# 项目规则

当用户发送小初高学科题目时，请按照以下规则响应：

[此处粘贴 skill-knowledge-point-analyzer.md 的全部内容]
```

### 方式2：--system-prompt 参数启动

```bash
claude --system-prompt "$(cat skill-knowledge-point-analyzer.md)"
```

### 方式3：/custom-slash 命令

在 Claude Code 的自定义命令配置中，创建一个 slash command：

1. 打开 Claude Code 设置 → Custom Slash Commands
2. 命令名：`/知识点解析`
3. Prompt 内容：粘贴 `skill-knowledge-point-analyzer.md` 全文
4. 使用时输入 `/知识点解析` + 题目即可

---

## 四、通用 AI 对话平台（ChatGPT / DeepSeek / Kimi 等）

### 使用方法

1. 打开平台的「系统提示词」或「自定义指令」设置
2. 将 `skill-knowledge-point-analyzer.md` 的全部内容粘贴进去
3. 保存后，正常对话即可自动生效

### 平台对应入口

| 平台 | 入口位置 |
|------|----------|
| ChatGPT | Settings → Custom Instructions → System Prompt |
| DeepSeek | 对话设置 → 系统提示词 |
| Kimi | 设置 → 自定义人设 |
| 通义千问 | 设置 → 自定义系统提示词 |
| 文心一言 | 设置 → 自定义指令 |

---

## 五、API 集成（开发者）

若通过 API 调用，将 `skill-knowledge-point-analyzer.md` 内容作为 `system` 角色消息传入：

```json
{
  "model": "your-model",
  "messages": [
    {
      "role": "system",
      "content": "[此处粘贴 skill-knowledge-point-analyzer.md 全文]"
    },
    {
      "role": "user",
      "content": "帮我查这道题知识点：已知函数f(x)=x²-4x+3，求f(x)的最小值"
    }
  ]
}
```

---

## 文件清单

| 文件 | 用途 |
|------|------|
| `skill-knowledge-point-analyzer.md` | **核心 Skill 文件**（System Prompt 全文） |
| `skill-deployment-guide.md` | 本文件 — 各平台部署指南 |
| `小初高全科题目知识点解析Skill配置.md` | 原始配置文档（参考用） |
