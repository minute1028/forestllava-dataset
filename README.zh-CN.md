# Forest-LLaVA 多模态树种数据集

English version: [README.md](README.md)

本仓库提供与 Forest-LLaVA 多模态树种数据集及配套论文一致的划分 CSV。约 13 GiB 的 Optical、MSI 和 SAR 影像将在影像发布准备完成后，单独发布到 [Hugging Face 数据集仓库](https://huggingface.co/datasets/minute1028/forestllava-dataset)。在该仓库创建完成前，上述链接可能暂时无法访问。

## 仓库内容

```text
splits/
  us50_formal/             # US-50 正式、按类别分层的划分
  us50_spatial_holdout/    # US-50 0.25° 分块 + 1 km 训练/评价缓冲划分
  us200_common_oms/        # V4 使用的 US-200 三模态共同有效划分
metadata/
  image_manifest.csv.gz    # sample_id 到 Optical/MSI/SAR 文件名的映射
  release_inventory.json   # 数量和来源路径
preview/figure_3_2_multimodal_patch_example.png
data/                      # 指向源 TIFF 目录的本地只读链接
scripts/build_release_staging.py
scripts/verify_release.py
checksums/metadata.sha256
```

当前本地影像集合中，Optical、MSI 和 SAR 三种模态各有 309,599 个 TIFF，总大小约 13 GiB。TIFF 文件未复制到此准备目录。完成许可证核对后，影像应作为带校验和的归档或分片发布到适合大文件的数据仓库；GitHub 仓库通常只托管 README、划分 CSV、元数据、清单和下载脚本，而不直接存放近百万个小文件。

## 数据来源与模态

样本索引和分类学记录来自 GlobalGeoTree 的美国子集。对齐后的观测使用 NAIP 航空影像（Optical）、Sentinel-2 Level-2A 影像（MSI）和 Sentinel-1 GRD 影像（SAR）。每个样本由 `sample_id` 标识，三种模态经过论文所述处理后对应同一块 60 m × 60 m 地面范围。预览图仅用于示例，不能替代原始数据产品。

典型影像文件名如下：

```text
<sample_id>_<scientific_name>_<local_name>_US_光学.tif
<sample_id>_<scientific_name>_<local_name>_US_多光谱.tif
<sample_id>_<scientific_name>_<local_name>_US_SAR.tif
```

CSV 文件保留 GlobalGeoTree 字段（`sample_id`、四层级标签、坐标、来源、年份和有效性标记）。压缩影像清单给出每种模态的准确文件名，并标记三个模态是否全部存在。

## 数据划分协议

### US-50 正式划分

正式划分是论文的主要基准：训练、验证和测试样本分别为 36,312、4,552 和 4,551 条，共 45,415 条；每个集合均覆盖相同的 50 个物种。该划分按物种分层，以保持类别覆盖和近似的类内均衡，但不保证空间独立性。

### US-50 空间预留划分

空间审查划分从相同的 45,415 条 US-50 共同有效记录开始。样本按 0.25° 空间分块分配，并在训练集与验证/测试样本之间设置 1 km 中心点距离缓冲。最终保留训练、验证和测试样本分别为 35,611、4,806 和 4,686 条，共 45,103 条；三个集合仍覆盖 50 个物种。该距离缓冲用于降低训练集与评价集之间的局部空间邻近，不用于宣称严格跨区域或跨生态区泛化能力。

### US-200 共同有效划分

V4 实验使用的 US-200 划分包含训练、验证和测试样本分别为 138,721、17,248 和 17,386 条，共 173,355 条；每个集合覆盖 200 个物种。源数据目录中的 200,000 条计划记录候选文件仍然保留，但不标记为论文最终的 Optical/MSI/SAR 共同有效划分。

## CSV 结构与质量控制

记录通过 `sample_id` 进行关联，仅保留通过所需影像和相关记录共同有效检查的样本。发布的划分文件已检查预期行数、重复 ID、集合间互斥性和物种覆盖情况。对应的影像清单和像元级文件检查将在 Hugging Face 影像发布中提供。

## 数据预览

![三模态影像示例](preview/figure_3_2_multimodal_patch_example.png)

Optical、MSI 和 SAR 产品采用面向可读性的模态专用显示增强方式，图像显示不会改变模型输入数据。

## 来源、许可证与局限

影像公开发布前，需要确认 GlobalGeoTree、NAIP、Sentinel-1 和 Sentinel-2 的再分发与署名要求。此准备包不会自行声明许可证或 DOI。最终公开仓库应包含适用的第三方声明、版本标签、校验和以及正式数据集引用。

这些记录来自开放观测，因此继承其地理采样格局。正式划分用于可比的模型评价，而不是空间独立性评价；空间预留划分作为补充审查划分提供。除非另行定义明确的地理泛化协议，否则不应将任一划分解释为模型在未见大陆或生态区上的严格性能估计。

## 引用

在公开仓库记录和 DOI 分配后，请同时引用 Forest-LLaVA 论文、GlobalGeoTree 原始数据集以及相关卫星/航空数据产品。引用信息将在最终许可证和仓库编号确定后补充。
