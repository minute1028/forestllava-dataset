# Forest-LLaVA Multimodal Tree-Species Dataset

中文版：[README.zh-CN.md](README.zh-CN.md)

Forest-LLaVA is a multimodal remote-sensing dataset for tree-species
recognition and structured vision-language research. This GitHub repository
contains the paper-aligned split CSV files and lightweight preview materials.
The complete processed Optical, MSI and SAR image archives, together with the
labels and Geo records, are available from the [Forest-LLaVA Hugging Face
Dataset repository](https://huggingface.co/datasets/minute1028/forestllava-dataset).

## Repository contents

```text
splits/
  us50_formal/             # US-50 formal, class-stratified split
  us50_spatial_holdout/    # US-50 0.25° blocks + 1 km train/evaluation buffer
  us200_common_oms/        # US-200 common-OMS split
preview/
  figure_3_2_multimodal_patch_example.png
  figure_3_3_valid_sample_spatial_distribution.png
```

The split files are CSV files with `sample_id` as the sample-level join key.
They retain the four-level GlobalGeoTree labels, coordinates, source,
observation year and validity fields. Image filenames can be matched to the
CSV records through their numeric `sample_id` prefix.

## Dataset configurations

| Configuration | Train | Validation | Test | Species | Role |
|---|---:|---:|---:|---:|---|
| US-50 formal | 36,312 | 4,552 | 4,551 | 50 | Main class-stratified benchmark |
| US-50 spatial hold-out | 35,611 | 4,806 | 4,686 | 50 | Spatial-sensitivity protocol |
| US-200 common-OMS | 138,721 | 17,248 | 17,386 | 200 | Expanded-class benchmark |

The formal split prioritizes class coverage and approximate within-class
balance, and does not guarantee spatial independence. The spatial hold-out
uses 0.25° spatial blocks and a 1 km centre-to-centre buffer between training
and validation/test samples. It reuses the US-50 image pool and is not a
strict cross-region or cross-ecoregion generalization benchmark. US-200
contains the US-50 records; the two configurations therefore share some image
patches in the Hugging Face archives so that each configuration can be
downloaded independently.

## Data sources and modalities

Each record is associated with a common 60 m × 60 m ground patch from three
public remote-sensing products:

- **Optical:** USDA Farm Service Agency National Agriculture Imagery Program
  (NAIP) aerial imagery;
- **MSI:** Sentinel-2 Level-2A multispectral imagery;
- **SAR:** Sentinel-1 GRD dual-polarization radar imagery.

The Hugging Face release contains processed TIFF patches rather than the
original provider archives. Optical, MSI and SAR files are organized under
separate `us50/` and `us200/` directories, with per-modality shard manifests
and SHA-256 checksums. The labels and geographic/environmental records are
provided as two compact archives under `annotations/`.

## Preview

The preview images show one aligned three-modality sample and the spatial
distribution of valid US-50 records. Modality-specific display enhancement is
used only for visualization and does not change model input values.

![Example of aligned Optical, MSI and SAR patches](preview/figure_3_2_multimodal_patch_example.png)

![US-50 valid-sample spatial distribution](preview/figure_3_3_valid_sample_spatial_distribution.png)

## Image and annotation access

Download the complete processed images and annotation archives from:

[Hugging Face Dataset: minute1028/forestllava-dataset](https://huggingface.co/datasets/minute1028/forestllava-dataset)

The Hugging Face Dataset Card documents the directory layout, shard sizes,
sample counts, extraction commands, checksums and the relationship between
the three split protocols. Users can download only the configuration and
modality required for their experiment.

## Provenance, licensing and limitations

Sample indices, taxonomic labels and associated geographic records originate
from GlobalGeoTree. GlobalGeoTree is distributed under the Creative Commons
Attribution 4.0 International licence (CC BY 4.0); please cite the original
dataset and paper when using these records.

Optical patches were derived from USDA FSA NAIP imagery. MSI and SAR patches
contain modified Copernicus Sentinel data processed by the Forest-LLaVA
preprocessing pipeline. Please retain the attribution of GlobalGeoTree,
USDA/FSA/NAIP and Copernicus/ESA, and comply with the terms of the particular
upstream product and acquisition year. The detailed notices are maintained in
the [Hugging Face third-party data notice](https://huggingface.co/datasets/minute1028/forestllava-dataset/blob/main/licenses/THIRD_PARTY_NOTICES.md).
The applicable upstream terms control third-party source material; this
repository does not grant broader rights.

Because the records originate from open observations, the dataset inherits
their geographic sampling pattern. The formal split is intended for comparable
class-stratified model evaluation, while the spatial hold-out provides a
complementary local-proximity sensitivity protocol.

## Citation

When using this dataset, please cite the Forest-LLaVA paper, the GlobalGeoTree
source dataset, and the relevant NAIP, Sentinel-1 and Sentinel-2 products. The
Hugging Face Dataset Card contains the current release record and attribution
notices.
