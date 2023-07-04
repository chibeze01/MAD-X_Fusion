Here is a possible readme for the PDF, based on the current web page context:

# MAD-X Fusion: A Framework for Cross-Lingual Transfer in Low-Resource Languages

This repository contains the code and data for the paper "Enhancing Cross-Lingual Transfer in
 Low-Resource Languages: Leveraging
 Parameter-Efficient Adapters for Multilingual
 Extractive Question Answering" by Chibeze Joseph Nwangwu.

## Abstract

In this paper, we present MAD-X Fusion, a cross-lingual learning framework that leverages parameter-efficient adapters to improve performance on low-resource languages. We focus on the extractive question answering task, which requires language comprehension and contextual inference. Our framework consists of two steps: 1) training language-agnostic, task-specific adapters using the MAD-X framework, which combines language and invertible adapters, and 2) integrating AdapterFusion, a technique that allows for the composition of multiple adapters, to train a fusion layer on a source language dataset. We evaluate our framework on five languages (English, Hindi, Bengali, Swahili, and Icelandic) and show that it outperforms the baseline model (MAD-X) in both zero-shot and few-shot settings. We also analyze the effectiveness of different adapter compositions and provide insights into the benefits of AdapterFusion.

## Requirements

- Python 3.6 or higher
- PyTorch 1.8 or higher
- Transformers 4.5 or higher
- AdapterHub 2.1 or higher
- Datasets 1.6 or higher

## Data

We use the following datasets for our experiments:

- SQuAD v1.1 (Rajpurkar et al., 2016) for English
- iNLTK (Gupta et al., 2019) for Hindi
- BengaliQA (Hasan et al., 2020) for Bengali
- SwahiliQA (Ogueji et al., 2022) for Swahili
- IceQuAD (Steingrímsson et al., 2020) for Icelandic

The datasets can be downloaded from Hugging Face Datasets or from their respective sources.

## Models

We use the following pre-trained multilingual models as our base models:

- mBERT (Devlin et al., 2019)

We use AdapterHub to load and train adapters for these models.

## Usage

To train language adapters, run:

```bash
python train_language_adapters.py --model_name_or_path <model_name_or_path> --languages <languages>
```

where `<model_name_or_path>` is the name or path of the pre-trained multilingual model and `<languages>` is a comma-separated list of languages to train adapters for.

To train task adapters, run:

```bash
python train_task_adapters.py --model_name_or_path <model_name_or_path> --language <language> --dataset <dataset>
```

where `<model_name_or_path>` is the name or path of the pre-trained multilingual model with language adapters loaded, `<language>` is the source language to train task adapters for, and `<dataset>` is the name of the source language dataset.

To train fusion layer, run:

```bash
python train_fusion_layer.py --model_name_or_path <model_name_or_path> --language <language> --dataset <dataset> --adapter_composition <adapter_composition>
```

where `<model_name_or_path>` is the name or path of the pre-trained multilingual model with language and task adapters loaded, `<language>` is the source language to train fusion layer for, `<dataset>` is the name of the source language dataset, and `<adapter_composition>` is one of `fusion`, `stack`, `both`, or `none`, indicating which adapter composition to use.

To evaluate models, run:

```bash
python evaluate_models.py --model_name_or_path <model_name_or_path> --language <language> --dataset <dataset> --adapter_composition <adapter_composition>
```

where `<model_name_or_path>` is the name or path of the pre-trained multilingual model with adapters and fusion layer loaded, `<language>` is the target language to evaluate on, `<dataset>` is the name of the target language dataset, and `<adapter_composition>` is one of `fusion`, `stack`, `both`, or `none`, indicating which adapter composition to use.

## Results

The following table summarizes our main results on F1 scores for different model variants and languages.

| Model | en | hi | bn | sw | is | Average |
|-------|----|----|----|----|----|---------|
| MAD-X (baseline) | 82.39 | 50.73 | 48.90 | 57.85 | 39.83 | 55.94
| Full Fine-Tuning MBERT (baseline)| 89.12 | 55.29 | 56.29 | 60.99 | 41.57 | 60.65
| MAD-X Fusion Zero-Shot | 83.26 | 53.47 | 52.86 | 59.72 | 37.34 | 57.33
| MAD-X Fusion Few-Shot | 83.26 | 60.36 | 60.41 | 76.69 | 56.17 | 67.38

## Citation

If you use our code or data, please cite our paper:

```bibtex
@article{nwangwu2023enhancing,
  title={Enhancing Cross-Lingual Transfer in Low-Resource Languages: Leveraging Parameter-Efficient Adapters for Multilingual Extractive Question Answering},
  author={Nwangwu, Chibeze Joseph},
  journal={The University of Bath},
  year={2023}
}
```
