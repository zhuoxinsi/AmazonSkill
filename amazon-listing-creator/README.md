# Amazon Listing Creator

基于 A9 + COSMO + Rufus 三算法的亚马逊 Listing 智能生成工具。

## 功能特点

- ✅ 三算法全覆盖（A9 + COSMO + Rufus）
- ✅ 分阶段交互引导
- ✅ 合规黑名单自动校验
- ✅ 数据驱动，拒绝空洞描述
- ✅ 支持自定义扩展

## 文件结构

```
amazon-listing-creator/
├── SKILL.md                          # Skill 定义文件
├── .metadata.json                    # 元数据
├── AGENTS.md                         # AI 交互流程指南
├── amazon_compliance_blacklist.txt   # 违禁词黑名单
├── prompts/
│   └── generate_listing.md           # Listing 生成 Prompt
└── README.md                         # 本文件
```

## 使用方法

直接在 OpenClaw 中说：

> "帮我生成一个 [产品名称] 的亚马逊 Listing"

AI 会自动分阶段引导你完成整个流程。

## 输入文件

用户提供以下 4 份文件：

| 文件 | 作用 | 获取方式 |
|-----|------|---------|
| 本品属性表.txt | Rufus 事实源 | 1688/供应商产品参数 |
| 竞品意图分析.txt | COSMO 场景源 | 竞品 Listing + Review |
| ABA关键词数据.csv | A9 流量源 | 亚马逊后台/卖家精灵 |
| 竞品出单词报告.csv | 流量补充 | 反查竞品流量词 |

## 输出内容

- **Title** - A9 优化标题
- **Bullet Points** - 五点描述
- **Product Description** - 产品描述
- **Search Terms** - 后台搜索词

## 版本

v1.1.0
