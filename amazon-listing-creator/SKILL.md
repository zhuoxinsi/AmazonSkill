---
name: amazon-listing-creator
displayName: 亚马逊 Listing 智能生成器 (A9+COSMO+Rufus)
description: 基于 A9+COSMO+Rufus 三算法的亚马逊 Listing 生成工具，7步流程指导用户准备资料，生成高转化 Listing。支持分阶段对话，自动校验合规性。
version: 1.1.0
type: skill
tags:
  - amazon
  - listing
  - ecommerce
  - a9
  - cosmo
  - rufus
  - aeo
trigger:
  description: "当用户需要创建、生成、优化亚马逊产品 Listing 时触发。包括：新品上架、Listing 优化、关键词埋词、标题/五点/描述生成等场景。"
  keywords:
    - 亚马逊
    - listing
    - 标题
    - 五点描述
    - 产品描述
    - A9
    - COSMO
    - Rufus
    - 关键词
    - Listing生成
    - Listing优化
---

# 亚马逊 Listing 智能生成器

基于亚马逊 **A9 + COSMO + Rufus** 三算法优化的 Listing 生成工具。

## 核心能力

- 分阶段引导用户准备 4 个关键文件
- 生成符合 AEO (Answer Engine Optimization) 逻辑的 Listing
- 自动校验合规黑名单，避免违规词

## 三大算法说明

| 算法 | 解决什么问题 | 核心逻辑 |
|------|------------|---------|
| **A9/A10** | 「搜得到」 | 关键词匹配与权重分配 |
| **COSMO** | 「搜的人是不是对的人」 | 场景+意图理解，人群标签 |
| **Rufus** | 「买不买你」 | 事实数据驱动，拒绝空洞描述 |

## 输入文件要求

用户提供以下 4 份文件：

| 文件 | 作用 | 获取方式 |
|-----|------|---------|
| **本品属性表.txt** | Rufus 事实源 | 1688/供应商产品参数 |
| **竞品意图分析.txt** | COSMO 场景源 | 2-3个头部竞品 Listing + Review |
| **ABA关键词数据.csv** | A9 流量源 | 亚马逊后台或卖家精灵/H10 |
| **竞品出单词报告.csv** | 流量补充 | 反查竞品流量词 |

## 输出内容

- **Title** (标题) - A9 优化，≤200字符
- **Bullet Points** (五点描述) - Rufus + COSMO 驱动
- **Product Description** (产品描述) - AEO 就绪
- **Search Terms** (后台搜索词) - 无重复、无竞品品牌

## 导出格式标准（Excel）

Listing 生成完成后，必须按以下标准格式导出为 `.xlsx` 文件：

### 文件命名规则
```
{Brand}_{Model}_{产品名}_Listing.xlsx
示例: TIMAVEX_JR070_Utensil_Holder_Listing.xlsx
```
> **Brand** 和 **Model** 来自 Phase 3.1 本品属性表的首要确认项。

### Sheet 结构（单 Sheet: "Amazon Listing"）

#### 主标题行（第1行）
```
Amazon Listing - {Model} {产品中文简称}
示例: Amazon Listing - JR070 相思木餐具收纳架
```
> 合并 A1:E1，深蓝色底，白色粗体 14pt

#### 模块 1: Title（5列）
| 列 | 字段名 | 说明 |
|---|--------|------|
| A | 模块 | 固定值 "Title" |
| B | 内容 | 完整英文标题文本 |
| C | 场景词 | *(可为空)* 标题覆盖的主要场景 |
| D | 关键词埋入 | 标题中包含的核心关键词列表 |
| E | 中文翻译 | 标题中文译文 |

#### 模块 2: Bullet Points（5列）
| 列 | 字段名 | 说明 |
|---|--------|------|
| A | # | 序号 1-5 |
| B | Bullet Point | 完整英文五点描述 |
| C | 场景词 | 该条描述覆盖的使用场景词 |
| D | 关键词埋入 | 该条埋入的关键词列表 |
| E | 中文翻译 | 五点中文译文 |

#### 模块 3: Search Terms（3列）
| 列 | 字段名 | 说明 |
|---|--------|------|
| A | 字段 | 固定值 "Search Terms" |
| B | English (英文) | 空格分隔的搜索词串 |
| C | 中文翻译 | 中文译文 |

> **备注行**（紧接 Search Terms 行下方）：字节数统计、已排除词、新增长尾词、排序说明、合规检查

#### 模块 4: 校验汇总 Validation Summary（3列）
| 列 | 字段名 | 说明 |
|---|--------|------|
| A | 项目 | 校验项名称 |
| B | 要求 | 规则要求 |
| C | 状态 | 实际结果 + 通过/失败标记 |

**必检项目**：
- Title 字符数 ≤ 200
- Bullet 1-5 各 ≤ 500 字符
- Search Terms 字节 ≤ 250 bytes
- A9 合规（核心词前置，长尾覆盖）
- COSMO 合规（明确人群词 + 使用场景）
- Rufus 合规（所有卖点有数据支撑）
- 合规黑名单（无 best/premium/guaranteed/eco-friendly 等）

#### 模块 5: 主图设计建议（合并单元格）
从 Listing 提取的核心卖点 → 主图视觉表达建议，每条包含：
- 卖点名称
- 主图展示方式
- 特写/对比/场景图建议

### 样式规范

- **主标题行**: 合并 A1:E1，深蓝色底 (#2E75B6)，白色粗体 14pt
- **模块标题**: 合并行，蓝色底 (#4472C4)，白色粗体 11pt
- **表头行**: 浅蓝底 (#D9E2F3)，黑色粗体 10pt
- **所有单元格**: 细边框，自动换行 (wrap_text)
- **列宽参考**: A=16, B=58, C=22, D=30, E=45
- **行高**: Title=55, Bullet=85, Search Terms=65, 备注=35, 主图建议=280

## 质量标准

每个输出模块通过三重校验：

- ✅ **A9 合规**: 核心词在 Title 出现，五点覆盖长尾词
- ✅ **COSMO 合规**: 明确人群词 + 场景词
- ✅ **Rufus 合规**: 所有卖点有数据/事实支撑，无空洞形容词
- ✅ **合规黑名单**: 未出现违禁词

## 使用方式

直接告诉我你的产品是什么，我会分阶段引导你完成整个流程。

**示例**:
> "帮我生成一个相思木餐具收纳架的亚马逊 Listing"

---

详细交互流程见 `AGENTS.md`，生成 Prompt 见 `prompts/generate_listing.md`。

## 导出工具依赖

- Python 3.x
- openpyxl 库 (`pip install openpyxl`)
- 导出脚本使用 UTF-8 编码，Windows 环境需注意路径处理
