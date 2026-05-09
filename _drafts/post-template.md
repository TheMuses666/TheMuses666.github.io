---
# ── 必填 ──────────────────────────────────────────
title: 文章标题（英文）
# 文件名格式: YYYY-MM-DD-slug.md  ← slug 用小写连字符

# ── 可选，但建议填 ──────────────────────────────
description: 一句话描述，用于 SEO 和链接预览。
subtitle: TAGLINE · IN · ALL CAPS
excerpt_text: 两句摘要，显示在文章页标题下方。
category_label: CATEGORY / TOPIC   # 例: SERVICE FINGERPRINTING / WEB SECURITY / AD ATTACK
image_class: portal                 # 可选: portal | neural | void | gridline
section_index: /LAB
---

<!-- 正文从这里开始，使用标准 Markdown -->

## Introduction

Write your intro paragraph here.

## Section Heading

Content here. Full Markdown support: **bold**, `inline code`, [links](https://example.com).

```bash
# Code blocks with syntax highlighting
nmap -sV -p- 192.168.1.1
```

## Findings

| Port  | Service | Version    | Notes        |
|-------|---------|------------|--------------|
| 22    | ssh     | OpenSSH 8.9| Default port |
| 80    | http    | nginx 1.24 | No HTTPS     |

## Conclusion

Wrap up and key takeaways.
