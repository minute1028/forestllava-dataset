# Forest-LLaVA multimodal tree-species dataset

中文说明：[README.zh-CN.md](README.zh-CN.md)

This repository provides the paper-aligned split CSVs for the Forest-LLaVA multimodal tree-species dataset. The large Optical, MSI and SAR image collection will be released separately through the [Hugging Face dataset repository](https://huggingface.co/datasets/minute1028/forestllava-dataset) after the image release has been finalized. The link may remain unavailable until that repository is created.

## Repository contents

```text
splits/
  us50_formal/             # US-50 formal, class-stratified split
  us50_spatial_holdout/    # US-50 0.25° blocks + 1 km train/evaluation buffer
  us200_common_oms/        # US-200 three-modality common-valid split used in V4
```

This GitHub repository intentionally contains no TIFF images, labels, model weights or local filesystem links. The current image collection contains 309,599 TIFF files for each modality (approximately 13 GiB in total) and will be distributed separately rather than committed to Git history.

## Data sources and modalities

The sample index and taxonomic records originate from the US subset of GlobalGeoTree. The aligned observations use NAIP aerial imagery (Optical), Sentinel-2 Level-2A imagery (MSI) and Sentinel-1 GRD imagery (SAR). Each sample is identified by `sample_id`; the three modalities represent a common 60 m × 60 m ground patch after the processing described in the paper. The preview image is an example only and is not a substitute for the source products.

Typical image names are:

```text
<sample_id>_<scientific_name>_<local_name>_US_光学.tif
<sample_id>_<scientific_name>_<local_name>_US_多光谱.tif
<sample_id>_<scientific_name>_<local_name>_US_SAR.tif
```

The CSV files retain the GlobalGeoTree fields (`sample_id`, four-level labels, coordinates, source, year and validity flags). The image release will provide a corresponding filename manifest and download instructions.

## Split protocols

### US-50 formal split

The formal split is the paper's main benchmark: 36,312 training, 4,552 validation and 4,551 test samples (45,415 samples total), covering the same 50 species in every split. It is stratified by species to preserve class coverage and approximate within-class balance. It does not guarantee spatial independence.

### US-50 spatial hold-out

The spatial audit split starts from the same 45,415 US-50 common-valid records. Samples are assigned by 0.25° spatial blocks, with a 1 km centre-to-centre buffer between training and validation/test samples. The released selection retains 35,611 training, 4,806 validation and 4,686 test samples (45,103 total); all three splits still cover 50 species. The distance buffer is intended to reduce local train–evaluation spatial proximity, not to claim strict cross-region or cross-ecoregion generalization.

### US-200 common-valid split

The US-200 split used by the V4 experiments contains 138,721 training, 17,248 validation and 17,386 test samples (173,355 total), covering 200 species in each split. The larger planned 200,000-record candidate files are retained in the source data directory but are not labelled as the paper's final common-Optical/MSI/SAR release.

## CSV schema and quality control

Records were linked by `sample_id` and retained only when the required imagery and associated records passed the common-valid checks. The released split files were checked for expected row counts, duplicate IDs, split disjointness and species coverage. The corresponding image manifest and pixel-level file checks will be provided with the Hugging Face image release.

## Provenance, licensing and limitations

Before public image release, confirm the redistribution licence and attribution requirements for GlobalGeoTree, NAIP, Sentinel-1 and Sentinel-2. The final Hugging Face repository will include the applicable third-party notices, a version tag, checksums and a formal dataset citation. Until those terms are finalized, this GitHub repository should be treated as the split-metadata release only.

The records are derived from open observations and therefore inherit their geographic sampling pattern. The formal split is designed for comparable model evaluation rather than spatial independence; the spatial hold-out is provided as a complementary audit split. Users should not interpret either split as a strict estimate of performance in an unseen continent or ecoregion without an explicitly defined geographic generalization protocol.

## Citation

Please cite the Forest-LLaVA paper and the original GlobalGeoTree and satellite/aerial data products after the public repository record and DOI are assigned. The citation block will be completed together with the final licence and repository accession.
