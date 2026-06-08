---
name: biomed-papers
description: Search and recommend top biomedical journal papers (Nature, Cell, Science, Circulation, JACC) matching your research interests like myocardial injury, single-cell analysis, etc.
---

# biomed-papers

在生物医学顶级期刊中搜索符合你研究方向的最新文献，并自动生成双语笔记。

## 使用方法

```bash
/biomed-papers
/biomed-papers --keyword "myocardial injury single cell"
/biomed-papers --journal "Circulation"
```

## 支持的顶级期刊池

- **CNS**: Nature, Cell, Science, Nature Medicine, Nature Cardiovascular Research
- **Cardiology Top**: Circulation, Journal of the American College of Cardiology (JACC), European Heart Journal (EHJ), Cardiovascular Research
- **General Top**: The Lancet, JAMA, NEJM

## 默认关键词池 (自动结合)

- myocardial injury / cardiac injury / heart failure
- high altitude / hypoxia
- single cell / scRNA-seq / snRNA-seq
- exercise / overload / mechanotransduction
- macrophage / immune / metabolism

## 执行步骤

1. **PubMed 检索** — 使用忽略SSL证书验证的 Python 脚本通过 PubMed E-utilities API 获取最新相关文献。
2. **过滤期刊** — 只保留发表在我们指定顶级期刊上的文献。
3. **元数据提取** — 提取标题、年份、期刊和完整摘要。
4. **生成双语笔记** — 翻译标题和摘要为中文。
5. **保存笔记** — 在 `E:/paper-reading/20_Papers/` 下生成 `YYYYMMDD-biomed-papers.md`。

## 默认运行逻辑

如果用户只运行 `/biomed-papers` 而不加参数，系统将自动使用以下 Python 脚本从 PubMed 抓取包含 "myocardial injury" 和 "single cell" 相关的顶级期刊文章，并生成笔记：

```python
# 核心搜索逻辑已内置，系统会自动结合 "myocardial", "single cell", "hypoxia" 等词在 PubMed 进行检索
# 注意：这台电脑需要使用 ssl.create_default_context() 并设置 check_hostname=False, verify_mode=ssl.CERT_NONE 来解决证书报错。
```
