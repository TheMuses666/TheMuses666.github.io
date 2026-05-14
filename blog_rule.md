# Blog 写作规则

## 文件名格式

```
YYYY-MM-DD-slug.md
```

- 文件放在 `_posts/` 目录下
- slug 使用小写字母和连字符
- 示例：`2026-05-09-nmap-service-enumeration.md`

---

## Front Matter

每篇文章顶部必须包含 `---` 包裹的 front matter 块。

**必填字段：**

| 字段 | 说明 |
|------|------|
| `title` | 文章标题 |

**建议填写的字段：**

| 字段 | 说明 | 示例 |
|------|------|------|
| `description` | 一句话描述，用于 SEO 和链接预览 | `A practical checklist for service enumeration.` |
| `subtitle` | 全大写副标题，显示在标题下方 | `DISCOVER. FINGERPRINT. DOCUMENT.` |
| `excerpt_text` | 两句摘要，显示在文章页标题下方 | |
| `category_label` | 分类标签 | `SERVICE FINGERPRINTING` / `WEB SECURITY` / `AD ATTACK` |
| `image_class` | 封面样式 | `portal` / `neural` / `void` / `gridline` |
| `section_index` | 所属栏目路径 | `/LAB` / `/ENUMERATION` |
| `permalink` | 自定义 URL（不填则自动生成） | `/blog/my-post.html` |

> 不填 `permalink` 时，URL 按 `_config.yml` 规则自动生成为 `/blog/<slug>.html`。

---

## 正文

正文从 front matter 结束的 `---` 之后开始，使用标准 Markdown。

支持：

- `**粗体**`、`` `行内代码` ``、`[链接](url)`
- 代码块（支持语法高亮，指定语言如 `bash`、`python` 等）
- 表格

---

## 正文结构（标准模板）

每篇 lab 类文章按以下顺序组织：

### 1. Summary
一到两段，概括实验目的和最关键的发现。不要列步骤，写观察和结论。

### 2. Enumeration
扫描/侦察阶段，包含实际运行的命令和截图，说明发现了什么。

### 3. Observation
对发现的解读——这个端口/服务意味着什么，为什么值得关注。

### 4. Execution
实际操作步骤，包含命令和截图，记录操作过程和即时结果。

### 5. What is X（知识点）
解释本次实验涉及的核心概念（如 Bind Shell、Reverse Shell 等），包含命令说明表格。

### 6. System Behaviour
描述攻击成功后系统层面发生了什么，从基础设施视角分析影响。

### 7. Defender Perspective
从防守方角度提问或反思，可以预告下一篇内容。

### 8. Architectural Reflection
一到两段，升华到更宏观的安全架构或信任模型层面的思考。

---

## 示例骨架

```markdown
---
title: ...
description: ...
subtitle: WORD · WORD · WORD
category_label: CATEGORY NAME
image_class: neural
section_index: /LAB
---

## Summary
## Enumeration
## Observation
## Execution
## What is X
## System Behaviour
## Defender Perspective
## Architectural Reflection
```

---

## 参考文件

- 模板：`_drafts/post-template.md`
- 配置：`_config.yml`
- 结构参考：`_posts/2026-05-14-first-pintest.md`
