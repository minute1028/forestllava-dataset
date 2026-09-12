# Forest-LLaVA 多模态树种数据集

本仓库提供 Forest-LLaVA 数据集与论文对应的划分 CSV。约 13 GiB 的 Optical、MSI 和 SAR TIFF 影像将单独发布到 [Forest-LLaVA Hugging Face 数据集仓库](https://huggingface.co/datasets/minute1028/forestllava-dataset)；该链接可能需要等影像仓库创建完成后才能访问。

## 仓库内容

- `splits/us50_formal/`：US-50 正式划分，训练/验证/测试为 36,312/4,552/4,551，共 45,415 条，50 个物种。
- `splits/us50_spatial_holdout/`：US-50 空间预留划分，训练/验证/测试为 35,611/4,806/4,686，共 45,103 条；由 0.25° 空间分块和 1 km 训练—评价距离缓冲构建。
- `splits/us200_common_oms/`：论文使用的 US-200 三模态共同有效划分，训练/验证/测试为 138,721/17,248/17,386，共 173,355 条，覆盖 200 个物种。

所有划分文件均为 CSV，以 `sample_id` 作为样本关联键，并保留 GlobalGeoTree 的四层级标签、坐标、来源、年份和有效性字段。

本 GitHub 仓库不包含 TIFF、标签 JSON、Geo 文件、模型权重或服务器本地软链接。当前影像目录中 Optical、MSI 和 SAR 各有 309,599 个 TIFF，影像文件将通过 Hugging Face 单独发布。

影像公开发布前仍需确认 GlobalGeoTree、NAIP、Sentinel-1 和 Sentinel-2 的再分发与署名条款，并在 Hugging Face 仓库补充最终许可证、数据版本号、校验文件和引用信息。正式划分保持类别覆盖和类内均衡，但不保证空间独立；空间预留划分用于降低训练—评价样本的局部空间邻近，不应直接解释为严格跨区域泛化基准。
