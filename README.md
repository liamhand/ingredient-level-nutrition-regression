# Ingredient-Level Nutrient Regression

Code and ingredient-level segmentation annotations for the paper **"Effect of segmentation granularity on nutrient prediction from real-world food images"**.

<!-- Add once available: -->
<!-- 📄 **Paper:** [DOI link] -->

## Overview

This repository accompanies a controlled study of **segmentation granularity** affects nutrient regression from overhead RGB food images. Using a subset of the [Nutrition5K](https://github.com/google-research-datasets/Nutrition5k) dataset, we compare three input representations under an identical regression model:

1. **Unsegmented** — regression directly from the original RGB image.
2. **Binary segmentation** — regression from binary food-region masks (background removed).
3. **Ingredient-level segmentation** — regression from fine-grained per-ingredient masks, with predictions aggregated to the dish level.

Each condition predicts five nutritional values: **mass, calories, fat, carbohydrate, and protein**.

**Key finding:** finer segmentation did not improve overall performance. The unsegmented baseline was strongest and ingredient-level segmentation weakest, with errors accumulating as dish complexity increased. The primary limitation lies in estimating ingredient *quantity*, not in identifying or isolating ingredients.

## What's included

- **Ingredient-level annotations** — 2,922 ingredient segmentation masks across 40 nutritionally grouped categories, covering a 1,056-image subset of Nutrition5K.
- **Training and evaluation code** — the regression pipeline for all three segmentation conditions and preprocessing variants.
- **Evaluation protocol** — scripts to reproduce the reported metrics (PMAE, MAE, macronutrient-ratio MAE, and cosine similarity).
- **Ingredient grouping map** — the mapping from the original 145 ingredient labels to the 40 coarse categories.

> **Note on data:** This repository does **not** redistribute the Nutrition5K images or original metadata, which remain the property of their authors. The annotations here are provided as an *addition* to Nutrition5K; you will need to obtain the base dataset separately (see below).

## Repository structure

<!-- TODO: update to match your actual layout -->
```
.
├── annotations/        # Ingredient-level segmentation masks + grouping map
├── data/               # Instructions/scripts for obtaining Nutrition5K
├── src/                # Training, evaluation, and preprocessing code
├── configs/            # Experiment configurations
├── requirements.txt
└── README.md
```

## Requirements

- Python 3.7
- PyTorch 1.13

<!-- TODO: confirm and pin the rest in requirements.txt -->
```bash
pip install -r requirements.txt
```

## Getting the data

1. Obtain the Nutrition5K dataset from the [official repository](https://github.com/google-research-datasets/Nutrition5k) and follow their access terms.
2. Place the overhead RGB images where the config expects them (see `configs/`).
3. The ingredient-level masks in `annotations/` are keyed to Nutrition5K dish IDs.

## Reproducing the results

<!-- TODO: replace with your actual commands -->
```bash
# Example — adjust to your entry points
python src/train.py --config configs/unsegmented.yaml
python src/train.py --config configs/binary.yaml
python src/train.py --config configs/ingredient.yaml

python src/evaluate.py --config configs/ingredient.yaml
```

Training used the Adam optimizer (initial learning rate 1e-4, exponential decay 0.99/epoch), batch size 8, for 300 epochs, with a fixed random seed (42) for reproducibility.

## Citation

If you use this code or the annotations, please cite:

<!-- TODO: update once the paper has full publication details / DOI -->
```bibtex
@article{YOURKEY,
  title   = {Effect of segmentation granularity on nutrient prediction from real-world food images},
  author  = {[]},
  journal = {},
  year    = {2026},
  doi     = {[DOI]}
}
```

Please also cite the original **Nutrition5K** dataset (Thames et al., CVPR 2021), on which these annotations are built.

## License

This repository uses two licenses, one for the code and one for the annotations:

- **Code** — released under the [MIT License](LICENSE).
- **Ingredient-level annotations** — released under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE-annotations), consistent with the [Nutrition5K](https://github.com/google-research-datasets/Nutrition5k) dataset on which they are built.

If you use the annotations, please provide attribution as described below and cite both this work and the original Nutrition5K dataset.

## Acknowledgements

These annotations extend the Nutrition5K dataset. We thank its authors for making it publicly available.
