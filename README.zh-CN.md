# Forest-LLaVA 多模态树种数据集

English version: [README.md](README.md)

Forest-LLaVA 是一个面向树种识别和结构化视觉语言研究的多模态遥感数据集。本仓库提供论文使用的划分 CSV。约 13 GiB 的 Optical、MSI 和 SAR 影像将在影像发布准备完成后，单独发布到 [Forest-LLaVA Hugging Face 数据集仓库](https://huggingface.co/datasets/minute1028/forestllava-dataset)。在该仓库创建完成前，上述链接可能暂时无法访问。

## 仓库内容

```text
splits/
  us50_formal/             # US-50 正式、按类别分层的划分
  us50_spatial_holdout/    # US-50 0.25° 分块 + 1 km 训练/评价距离缓冲划分
  us200_common_oms/        # V4 使用的 US-200 三模态共同有效划分
preview/
  figure_3_2_multimodal_patch_example.png
```

划分文件均为 CSV，以 `sample_id` 作为样本级关联键，并保留 GlobalGeoTree 的四层级标签、坐标、来源、观测年份和有效性字段。影像文件名可通过其开头的数字 `sample_id` 与 CSV 记录对应。

## 数据来源与模态

样本索引和分类学记录来自 GlobalGeoTree 的美国子集。每条记录均关联三个公开遥感产品形成的同一块 60 m × 60 m 地面 patch：

- Optical：NAIP 航空影像；
- MSI：Sentinel-2 Level-2A 影像；
- SAR：Sentinel-1 GRD 影像。

处理后的数据面向科研使用。下方预览图展示三种对齐模态的一个示例；模态专用显示增强仅用于可视化，不会改变模型输入数值。

## 数据划分协议

### US-50 正式划分

正式基准包含训练 36,312 条、验证 4,552 条和测试 4,551 条样本，共 45,415 条；三个集合均包含相同的 50 个物种。样本按物种分层，以保持类别覆盖和近似的类内均衡。正式划分用于可比的模型评价，不保证空间独立性。

### US-50 空间预留划分

空间预留划分从相同的 45,415 条 US-50 共同有效记录开始。样本按 0.25° 空间分块分配，并在训练集与验证/测试样本之间设置 1 km 中心点距离缓冲。发布的划分包含训练 35,611 条、验证 4,806 条和测试 4,686 条，共 45,103 条；三个集合均覆盖 50 个物种。该划分用于降低训练集与评价集之间的局部空间邻近并支持空间敏感性分析，不用于宣称严格跨区域或跨生态区泛化能力。

### US-200 共同有效划分

V4 实验使用的 US-200 划分包含训练 138,721 条、验证 17,248 条和测试 17,386 条，共 173,355 条；三个集合均覆盖 200 个物种。200,000 条文件表示计划候选记录，本仓库中的 CSV 是论文最终使用的共同有效划分。

## 数据预览

![对齐的 Optical、MSI 和 SAR patch 示例](preview/figure_3_2_multimodal_patch_example.png)

## 影像获取

处理后的 TIFF 影像总量和文件数量不适合放入普通 Git 仓库，因此将单独发布。影像文件、清单和下载说明将在 Hugging Face 仓库提供：

[https://huggingface.co/datasets/minute1028/forestllava-dataset](https://huggingface.co/datasets/minute1028/forestllava-dataset)

## 来源、许可证与局限

本数据集将 GlobalGeoTree 观测记录与 NAIP、Sentinel-1 和 Sentinel-2 派生影像结合。使用或再分发数据时，应保留各上游来源的署名并遵守其使用条款。影像仓库将提供适用的第三方声明以及所发布文件的许可证。

由于记录来自开放观测，数据集继承其地理采样格局。正式划分优先保证类别均衡比较，而不是空间独立性；空间预留划分降低了训练集与评价集之间的局部邻近，但不构成严格的地理独立性。除非另行定义明确的地理泛化协议，否则不应将任一划分直接解释为模型在未见大陆或生态区上的性能估计。

## 引用

使用本数据集时，请引用 Forest-LLaVA 论文、GlobalGeoTree 原始数据集以及相关 NAIP、Sentinel-1 和 Sentinel-2 数据产品。影像发布后，将在 Hugging Face 记录中补充带版本号的数据集引用。
