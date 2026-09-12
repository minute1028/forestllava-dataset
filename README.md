# Forest-LLaVA Multimodal Tree-Species Dataset

中文版：[README.zh-CN.md](README.zh-CN.md)

This repository provides the split CSV files corresponding to the Forest-LLaVA dataset and the accompanying paper. The approximately 13 GiB collection of Optical, MSI and SAR TIFF images will be released separately through the [Forest-LLaVA Hugging Face dataset repository](https://huggingface.co/datasets/minute1028/forestllava-dataset); this link may remain unavailable until that repository has been created.

## Repository contents

- `splits/us50_formal/`: the formal US-50 split, with 36,312/4,552/4,551 training/validation/test samples, 45,415 samples in total and 50 species.
- `splits/us50_spatial_holdout/`: the US-50 spatial hold-out split, with 35,611/4,806/4,686 training/validation/test samples, 45,103 samples in total; constructed using 0.25° spatial blocks and a 1 km train–evaluation distance buffer.
- `splits/us200_common_oms/`: the US-200 three-modality common-valid split used in the paper, with 138,721/17,248/17,386 training/validation/test samples, 173,355 samples in total and 200 species.

All split files are CSV files. They use `sample_id` as the sample-level join key and retain the four-level GlobalGeoTree taxonomic labels, coordinates, source, observation year and validity fields.

This GitHub repository does not contain TIFF images, label JSON files, Geo files, model weights or local server filesystem links. The current image collection contains 309,599 TIFF files for each of Optical, MSI and SAR. The image files will be released separately through Hugging Face.

Before the images are made public, the redistribution and attribution terms for GlobalGeoTree, NAIP, Sentinel-1 and Sentinel-2 must be confirmed. The Hugging Face repository will then be updated with the final licence, dataset version, checksum files and citation information. The formal split preserves category coverage and approximate within-class balance but does not guarantee spatial independence; the spatial hold-out split is provided to reduce local spatial proximity between training and evaluation samples and should not be interpreted as a strict cross-region generalization benchmark.
