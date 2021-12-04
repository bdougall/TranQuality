# W266_Project

## Table of Contents  
- [Overview](#overview)  
- [Presentation of Findings](#presentation)
- [Dataset Creation](#dataset-creation)
- [Siamese Models](#siamese-models)
    - [Model Notebooks](#siamese-model-notebooks)
    - [Model Weights and Bias Checkpoints](#siamese-w-b)
    - [Best Siamese Evaluation](#best-siamese-eval)    

## Overview <a name="overview"></a>
In our project, we implement paraphrase-matching to evaluate the translation qualities produced by two transformers (IndicTrans and MBart). We seek to determine if filtering records by the resultant paraphrase scores results in a corpus of improved translation quality.

## Presentation of Findings <a name="presentation"></a>
To see a high level overview of our findings from this project, please go to the [Google Slides Presentation](https://docs.google.com/presentation/d/1DtTs9N8rKzuyIbOM5BIr9Fj5rrlIxkeOUFAeWmrXhq4/edit?usp=sharing).

## Dataset Creation <a name="dataset-creation"></a>
#### `paraphrase_wo_pb_dataset_creation.ipynb`

Concatenates the Hindi, Tamil, and Malayalam training datasets from the Amrita paraphrase corpus to form 1 training data set, shuffling the training data so that multiple languages are present in each training batch. Randomly split the records in each of the Hindi, Tamil, and Malayalam test datasets into half, uses half of each language's test data to form 1 validation dataset, and uses the other half of each language's test dataset for the test dataset used to test paraphrase model final performance.

#### `paraphrase_w_pb_dataset_creation.ipynb`

Takes the Punjabi training and test datasets from the Amrita paraphrase corpus to create Punjabi training, validation, and test datasets, using the same procedure as in `paraphrase_wo_pb_dataset_creation.ipynb` to create the Punjabi validation and test datasets. Add the Punjabi training, validation, and test datasets to a copy of the paraphrase train, validation, and test datasets. Reshuffle the paraphrase training data so that the added Punjabi records are distributed throughout.

## Siamese Models <a name="siamese-models"></a>
### Model Notebooks <a name="siamese-model-notebooks"></a>
#### `layernorm_3dense_Pb_Siamese_BCELogitLoss.ipynb`

The best-performing Siamese neural network model, trained on Punjabi in addition to all of our languages of interest (Hindi, Tamil, and Malayalam).

#### `layernorm_3dense_w_Pb_sep_models.ipynb`

An experiment creating two separate models, an Aryan-only model (trained on Hindi and Punjabi) and a Dravidian-only model (trained on Tamil and Malayalam). This notebook shows that accuracy is diminished for predicting the labels of Dravidian languages in a Dravidian-only model.

#### `layernorm_woPb_Siamese_BCELogitLoss.ipynb`

The original Siamese neural network model, trained on only our languages of interest (Hindi, Tamil, and Malayalam). This notebook shows slightly lower accuracy rates for Tamil and Malayalam compared to the model also trained on Punjabi (`layernorm_3dense_Pb_Siamese_BCELogitLoss.ipynb`)

### Model Weights and Bias Checkpoints <a name="siamese-w-b"></a>
#### `aryan_model_layernorm.pt`

The Aryan-only model created in `layernorm_3dense_w_Pb_sep_models.ipynb`.

#### `drav_model_layernorm.pt`

The Dravidian-only model created in `layernorm_3dense_w_Pb_sep_models.ipynb`.

#### `three_dense_model_wopb_layernorm.pt`

The original model (not trained on Punjabi), created in `layernorm_woPb_Siamese_BCELogitLoss.ipynb`.

#### `three_dense_w_punjabi_model_layernorm.pt`

The best-performing model (trained on Punjabi in addition to Hindi, Tamil, and Malayalam), created in `layernorm_3dense_Pb_Siamese_BCELogitLoss.ipynb`.

### Best Siamese Evaluation <a name="best-siamese-eval"></a>
#### `layernorm_choose_best_record.ipynb`

Finds the best-translation (IndicTrans vs MBart) for each target translation in each language (Hindi, Tamil, and Malayalam), as measured by a higher probability of paraphrase score. This notebook also contains the language-specific SacreBleu scores on the ensemble corpus obtained by filtering the translations for each target record to only retain the one with the highest paraphrase probability score.

#### `layernorm_final_record_quality_eval.ipynb`

Explores the cosine similarity between translation and target and edit distance between translation and target text for each language in our record-filtered corpus, as well as the solo translator translations.

### `layernorm_model_mistakes.ipynb`

Explores classification mistakes that the best-performing Siamese model made on the Amrita paraphrase test set created in `paraphrase_w_pb_dataset_creation.ipynb`.

### `layernorm_siamese_bart_evaluation.ipynb`

Assigns a paraphrase probability score to each record for each language in the corpus of MBart translations. In this notebook, we also find the cosine similarity score between each MBart record and its target text and calculate the rate of translations considered `not paraphrases of the target text (NP)`.

### `layernorm_siamese_indictrans_evaluation.ipynb`

Assigns a paraphrase probability score to each record for each language in the corpus of IndicTrans translations. In this notebook, we also find the cosine similarity score between each IndicTrans record and its target text and calculate the rate of translations considered `not paraphrases of the target text (NP)`.
