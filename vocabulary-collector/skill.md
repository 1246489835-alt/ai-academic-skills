---
name: vocabulary-collector
description: Extract highlighted words/sentences from web content and create vocabulary notes in Obsidian
---

# Vocabulary Collector

从网页内容中提取高亮/标注的单词和句子，创建双语生词本笔记。

## 使用方法

1. 用户粘贴网页内容或URL
2. 自动提取高亮文本
3. 翻译成中文
4. 创建笔记到 `E:/vocabulary-collector/`

## 执行步骤

1. **接收内容** — 用户粘贴单词、短语、句子或文章片段
2. **检查日期文件夹** — 查看 `E:/vocabulary-collector/YYYYMMDD/` 是否存在
3. **提取内容**：
   - **单词/短语** — 关键表达和习语
   - **完整句子** — 有价值的金句、观点、论述
   - **优先提取**：比喻、反直觉观点、作者核心论点
4. **追加或新建笔记**：
   - **同一天内容** → 追加到当天已有笔记
   - **用户标注新关键词** → 创建新笔记 `YYYYMMDD-keyword1-keyword2-keyword3.md`
5. **格式化内容**：
   ```markdown
   ## 1. English word/phrase/sentence
   
   **释义**：中文释义（词性/用法说明）
   > Original English sentence with context
   对应的中文翻译（完整句子双语对照）
   ```
6. **双语翻译规范**：
   - 每条词汇必须包含：**英文原句** + **中文翻译**（`>` 引用块格式）
   - 中文翻译要完整、自然，不是逐字直译
   - 若原句有特别的语气或语境，翻译时需保留

## 文件结构

```
E:/vocabulary-collector/
├── 20260403/
│   ├── 20260403-productivity-books-reading.md
│   └── 20260403-business-strategy-growth.md
├── 20260404/
│   └── 20260404-health-fitness-nutrition.md
```

## 笔记命名规则

- 日期文件夹：`YYYYMMDD/`
- 笔记文件：`YYYYMMDD-keyword1-keyword2-keyword3.md`
- 同一天默认追加到第一个笔记，除非用户明确要求新建
