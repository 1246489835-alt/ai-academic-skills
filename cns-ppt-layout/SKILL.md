---
name: CNS-PPT-排版
description: >-
  将已命名好的科研图片（tif/png/jpg）自动排版为Nature/CNS级别PPT。
  适用场景：用户整理好某个Result的主图和/或附图文件夹，按【letter-number】命名规则，
  调用本skill自动生成纵向A4排版的PPTX（每页=1个Figure，panel标签自动加）。
  支持主图+附图分页、智能高度分配、宽高比保持、多种panel组合布局。
  当用户说"排版"、"出PPT"、"Figure排版"、"CNS排版"时触发。
---

# CNS-PPT-排版 Skill

## 功能定位
将按命名规则整理好的科研图片，一键生成Nature/Cell/Science投稿级别的PPT排版。

**不负责出图**（出图用 `/nature-figure`），只负责**已有图片的Figure级排版组装**。

## 触发条件
用户提到以下关键词时触发：
- "排版"、"PPT排版"、"Figure排版"
- "CNS排版"、"Nature排版"
- "把图片排成PPT"
- 提供了包含【letter-number】命名图片的文件夹路径

## 图片命名规则（用户须遵守）

```
【letter-number】描述.tif
【letter】描述.tif          （无编号=该panel只有1张图）
```

示例：
```
【a-1】celltype_umap.tif        → Panel a, 第1张
【a-2】cell_proportion.tif      → Panel a, 第2张
【b】qc_violin.tif              → Panel b, 单张
【c-1】GO_heatmap_up.tif        → Panel c, 第1张
【c-2】GO_heatmap_down.tif      → Panel c, 第2张
```

## 文件夹结构约定

### 方式一：单文件夹（只有主图或只有附图）
```
指定路径/
  【a-1】xxx.tif
  【a-2】xxx.tif
  【b】xxx.tif
  ...
```
→ 生成1页PPT

### 方式二：主图+附图分文件夹
```
指定路径/
  【1】主图/
    【a】xxx.tif
    【b】xxx.tif
    ...
  【2】附图/
    【a-1】xxx.tif
    【b-1】xxx.tif
    ...
```
→ 生成2页PPT（Slide 1=主图，Slide 2=附图）

## 执行流程

### Step 1：确认输入
- 确认图片文件夹路径
- 确认输出路径和文件名（默认：同级目录，`日期-Result名-Figure-Layout.pptx`）
- 扫描文件夹，列出发现的panels和图片数量/宽高比

### Step 2：生成排版脚本
使用Python + python-pptx，基于以下模板生成排版脚本：

```python
# 核心参数（V5，2026-05-28确认版）
SLIDE_W = Inches(7.5)      # 纵向A4
SLIDE_H = Inches(10.0)
M_LEFT = M_RIGHT = Cm(0.7) # 页面边距
M_TOP = Cm(0.7)
M_BOT = Cm(0.4)
PANEL_VGAP = Cm(0.45)      # panel间垂直间距
IMG_HGAP = Cm(0.2)         # panel内图片水平间距
LABEL_SIZE = Pt(12)         # panel标签字号
LABEL_FONT = "Arial"        # Nature标准字体
LABEL_H = Cm(0.45)          # 标签行高度
```

### Step 3：布局策略

#### 高度分配算法
每个panel的理想高度 = 该panel图片以全宽排列时的自然高度。
所有panel的理想高度按比例缩放，填满页面可用区域。

#### 布局规则（基础）
| 图片数 | 默认布局 |
|--------|---------|
| 1张(AR>2) | 独占一行，占满页面宽度 |
| 1张(AR≈1) | 必须和相邻panel并排，不能独占一行留两侧空白 |
| 1张(AR<0.8) | 竖向图，必须和相邻panel并排 |
| 2张 | 并排（自动识别方形+宽幅组合） |
| 3张 | 三等分并排 |
| 4张 | 四等分并排（单行），AR差异大时可2x2网格 |
| 5张+ | 3+2或2+3排列，根据AR自适应 |

#### V3排版核心原则（2026-05-28，用户确认版）

##### 原则1：矩形填充（最高优先级）
所有panel组合后的最终布局必须形成一个**紧凑矩形**——可以是A4等比缩放的竖长方形、宽高接近的正方形、或高>宽的矩形。**绝不允许**出现多处散落留白。1-2个小留白可接受，4个以上绝对不行。

##### 原则2：拼合思维（非居中思维）
排版的核心是**拼图/瓷砖**——把不同形状的panel像拼图一样紧密贴合，而非把每个panel居中放在各自区域。

具体规则：
- 窄panel（宽远小于A4宽）→ **必须和相邻panel并排**填满宽度，绝不能居中留两侧空白
- 宽panel（宽≈A4宽）→ 可以独占一行
- 居中仅在panel宽度接近页面宽度时使用（不会产生明显留白时）

**反面案例**：每个panel独占一行或区域内居中 → 大量留白碎片散落版面各处
**正面案例**：相邻panel左右拼合（方形+方形并排、方形+竖向图并排、宽图+窄图拼合）→ 紧凑无缝

##### 原则3：面积均衡
多图组成的panel（如4张小图的2x2网格）其整体视觉面积不应比单图panel小太多。小图不要强行缩得看不清。

##### 原则4：布局决策三要素
对每个panel考虑三个因素决定如何放置：
1. **形状类型**：方形(AR≈1) / 横向长方形(AR>1.5) / 竖向长方形(AR<0.8)
2. **宽高尺寸**：决定它能和谁并排、占多大比例
3. **顺序（a→z）**：保持阅读顺序（从上到下、从左到右），但允许同行内左右调配

##### 原则5：不分页
能放下就**绝不分页**。放不下时优先**适当等比缩放**所有panel使其fit在1页内，而非拆成多页。分页是最后手段。

##### 原则6：布局算法思路
1. 先分析每个panel的形状类型和面积
2. 按顺序将panel分配到"行"中：宽图(AR>2)可以独占一行，窄图/方形必须和相邻panel凑成一行
3. 每行内根据各panel的AR分配宽度比例，确保行内无大面积留白
4. 所有行叠加后的总高度如果超过页面高度 → 等比缩放所有行使其fit
5. 最终布局在页面上形成一个紧凑矩形，边距统一

##### 原则7：标签不可被遮挡（V4补充，2026-05-28）
Panel标签(a, b, c...)必须**完全可见**，绝不能被图片覆盖。实现方式：
- 标签放在panel区域的左上角
- 图片从标签的**右侧偏移**（同行左panel）或**下方偏移**开始放置
- 标签占位宽度约0.5cm，高度约0.35cm
- 图片的x坐标 = 标签x + 标签占位宽度 + 小间距（约0.05cm）
- 或者标签在上方时，图片y坐标 = 标签y + 标签高度

**反面案例**：标签和图片共享同一个x坐标，宽幅图片直接从左边缘开始 → 标签被盖住
**正面案例**：标签在左上角独立可见，图片从标签右侧/下方开始 → 清晰的panel标识

##### 原则8：宽度必须撑满（V4补充，2026-05-28）
同一行内并排的panel，其总宽度+间距必须占满页面可用宽度的**≥97%**。

具体要求：
- 列间gap缩到最小：0.1~0.15cm（不要用百分比算gap，直接用固定小值）
- 两个panel并排时：panel_A_width + gap + panel_B_width ≈ 可用宽度
- 宽度分配基于各panel图片的AR按比例分配，不要拍脑袋写固定百分比
- 宽度分配公式：对于同行两个panel（AR分别为ar_a, ar_b），假设行高为h，则 w_a = h * ar_a, w_b = h * ar_b，按比例分配可用宽度

**反面案例**：a_frac=0.54 + b_frac=0.43 + gap_frac=0.03 = 1.0，但实际图片只占80%宽度 → 两侧大量空白
**正面案例**：两个panel几乎贴满页面宽度，中间仅一条细缝

##### 原则9：高度分配基于实际AR计算（V4补充，2026-05-28）
每行的高度应该由该行内panel的实际AR计算得出，**不要用权重/百分比拍脑袋**。

计算方法：
1. 对于并排的panel A和B：给定各自宽度w_a和w_b，行高 = max(w_a/ar_a, w_b/ar_b)
2. 对于垂直堆叠的sub-images（如d-1/d-2/d-3）：stack高度 = n × (w/ar) + (n-1) × gap
3. 所有行高度加总 + 行间gap + 标签高度 = 总内容高度
4. 如果总内容高度 > 页面可用高度 → 等比缩放

**缩放因子健康检查**：scale应该 ≥ 0.8。如果scale < 0.8，说明行分配有问题（某行占用了过多高度），应该调整行内panel的宽度比例来平衡行高，而不是暴力缩放全局。

##### 原则10：整体比例协调（V4补充，2026-05-28）
最终内容区域应该是一个协调的**竖长方形**：高 > 宽，但不能是"窄长条"。

具体含义：
- A4纵向页面本身就是高>宽（10:7.5 ≈ 1.33:1），内容区域应接近这个比例
- 内容应该在X方向（宽度）撑满页面，Y方向（高度）自然填充
- **不要**为了让所有panel都占大面积而把Y轴拉得过长导致X轴被压缩
- 如果某行有多张竖图堆叠（如d-1/d-2/d-3），要控制该行的宽度占比足够大，避免它独占过多高度

**判断标准**：用户说"Y轴（高）可以比X轴（宽）大一些"= 高略大于宽是正常的portrait布局，但不能变成窄长条。参考用户手动排版的效果：宽度撑满，高度自然，整体饱满协调。

### Step 4：Nature排版规格

| 参数 | 规格 |
|------|------|
| 页面尺寸 | 7.5 x 10.0 inches（纵向，接近A4） |
| 背景 | 纯白 (#FFFFFF) |
| Panel标签 | Bold lowercase (a, b, c...), Arial 12pt, 黑色 |
| 标签位置 | 各panel图片区域左上角，不可被图片遮挡（图片从标签右侧/下方偏移开始） |
| 图片处理 | 保持原始宽高比，不拉伸 |
| 对齐 | 拼合对齐（非居中），panel紧密贴合形成矩形 |
| 边距 | 左右0.7cm，上0.7cm，下0.4cm |
| 间距 | panel间垂直: 0.45cm；panel内图片水平: 0.2cm |

### Step 4.5：备注生成（Panel Description Notes）

从文件名自动提取或手动指定每个panel的描述，写入PPT幻灯片备注中。

#### 备注排列规则
- 按panel字母排序（a→z），同字母按编号排序（1→N）
- 格式：`(letter-number) 描述`，每行一条
- 单张panel用 `(letter)`，多张panel用 `(letter-number)`
- 备注开头自动加 `Figure RX — Main/Supplementary Figure`

#### 描述来源（优先级）
1. 用户提供的 `desc_map` 字典（手动指定，最优先）
2. AI从文件名自动提取+优化（去掉序号前缀和扩展名，清洁化处理）
3. 直接用原始文件名（兜底）

#### 实现方式
在 `add_figure_slide()` 中调用 `generate_notes()` 函数：

```python
def generate_notes(panels, desc_map):
    lines = []
    for panel_key in sorted(panels.keys()):
        imgs = panels[panel_key]
        if len(imgs) == 1:
            key = panel_key
            desc = desc_map.get(key, imgs[0]['filename'])
            lines.append(f"({key}) {desc}")
        else:
            for img in imgs:
                key = f"{panel_key}-{img['order']}"
                desc = desc_map.get(key, img['filename'])
                lines.append(f"({key}) {desc}")
    return "\n".join(lines)
```

写入备注：
```python
notes_slide = slide.notes_slide
notes_tf = notes_slide.notes_text_frame
notes_tf.text = f"Figure RX — {title_text}\n\n{notes}"
```

### Step 5：输出
- 生成PPTX文件到指定路径
- 生成配套Python脚本（用户可二次调整参数后重新运行）
- 打印布局摘要（panels数量、图片数、宽高比）
- PPT每页备注包含panel描述清单（按字母+序号排序）

## 用户交互示例

```
用户: /CNS-PPT-排版 "C:\...\R3-心肌细胞\【1】主图" 放到 "C:\...\定稿"

AI执行:
1. 扫描文件夹 → 发现 Panel a(3张), b(1张), c(2张)
2. 生成排版脚本
3. 运行脚本 → 输出 2026-XX-XX-R3-Figure-Layout.pptx
4. 报告布局结果
```

## 参数覆盖

用户可在调用时指定覆盖参数：
- `横版` → 切换为16:9 (13.33 x 7.5 in)
- `大标签` → LABEL_SIZE = Pt(14)
- `紧凑` → 减小PANEL_VGAP和IMG_HGAP
- `宽松` → 增大间距

## 依赖
- Python 3.x
- python-pptx
- Pillow (PIL)

## 与其他skill的关系
- `/nature-figure` → 负责单张图的绑定级出图（matplotlib/R）
- `/CNS-PPT-排版` → 负责多张已出好的图的Figure级PPT排版组装
- 典型流程：先用 `/nature-figure` 出图 → 再用 `/CNS-PPT-排版` 排版
