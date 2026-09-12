# Forest-LLaVA Multimodal Tree-Species Dataset

中文版：[README.zh-CN.md](README.zh-CN.md)

Forest-LLaVA is a multimodal remote-sensing dataset for tree-species recognition and structured vision-language research. This repository provides the split CSV files used in the paper. The approximately 13 GiB collection of Optical, MSI and SAR images will be released separately through the [Forest-LLaVA Hugging Face dataset repository](https://huggingface.co/datasets/minute1028/forestllava-dataset). The link may remain unavailable until that repository is created.

## Repository contents

```text
splits/
  us50_formal/             # US-50 formal, class-stratified split
  us50_spatial_holdout/    # US-50 0.25° blocks + 1 km train/evaluation buffer
  us200_common_oms/        # US-200 three-modality common-valid split used in V4
preview/
  figure_3_2_multimodal_patch_example.png
```

The split files are CSV files with `sample_id` as the sample-level join key. They retain the four-level GlobalGeoTree labels, coordinates, source, observation year and validity fields. Image filenames can be matched to the CSV records by their numeric `sample_id` prefix.

## Data sources and modalities

Sample indices and taxonomic records originate from the US subset of GlobalGeoTree. Each record is associated with a common 60 m × 60 m ground patch from three public remote-sensing products:

- Optical: NAIP aerial imagery;
- MSI: Sentinel-2 Level-2A imagery;
- SAR: Sentinel-1 GRD imagery.

The processed data are intended for research use. The preview below shows one example of the three aligned modalities; modality-specific display enhancement is used only for visualization and does not change model input values.

## Split protocols

### US-50 formal split

The formal benchmark contains 36,312 training, 4,552 validation and 4,551 test samples (45,415 samples in total), with the same 50 species represented in each split. Samples are stratified by species to preserve class coverage and approximate within-class balance. The formal split is designed for comparable model evaluation and does not guarantee spatial independence.

### US-50 spatial hold-out split

The spatial hold-out split starts from the same 45,415 US-50 common-valid records. Samples are assigned by 0.25° spatial blocks, with a 1 km centre-to-centre distance buffer between training and validation/test samples. The released split contains 35,611 training, 4,806 validation and 4,686 test samples (45,103 samples in total), and all three splits cover 50 species. It is provided to reduce local train–evaluation spatial proximity and to support spatial-sensitivity analysis; it is not intended as a strict cross-region or cross-ecoregion generalization benchmark.

### US-200 common-valid split

The US-200 split used in the V4 experiments contains 138,721 training, 17,248 validation and 17,386 test samples (173,355 samples in total), with 200 species represented in each split. The 200,000-record files describe the planned candidate pool; the CSVs in this repository are the final common-valid split used by the paper.

## Preview

![Example of aligned Optical, MSI and SAR patches](preview/figure_3_2_multimodal_patch_example.png)

## Image access

The processed TIFF images are distributed separately because their total size and file count are not suitable for a conventional Git repository. The Hugging Face repository will provide the image files, manifests and download instructions when available:

[https://huggingface.co/datasets/minute1028/forestllava-dataset](https://huggingface.co/datasets/minute1028/forestllava-dataset)

## Provenance, licensing and limitations

The dataset combines GlobalGeoTree observation records with imagery derived from NAIP, Sentinel-1 and Sentinel-2. Users should retain the attribution and comply with the terms of each upstream source when using or redistributing the data. The image repository will provide the applicable third-party notices and the licence for the released files.

Because the records originate from open observations, the dataset inherits their geographic sampling pattern. The formal split prioritizes class-balanced comparison rather than spatial independence; the spatial hold-out split reduces local proximity between training and evaluation samples but does not establish strict geographic independence. Neither split should be interpreted as a direct estimate of performance on an unseen continent or ecoregion without an explicitly defined geographic generalization protocol.

## Citation

When using this dataset, please cite the Forest-LLaVA paper, the GlobalGeoTree source dataset and the relevant NAIP, Sentinel-1 and Sentinel-2 products. A versioned dataset citation will be added to the Hugging Face record when the image release is available.
