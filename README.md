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
To see a high level overview of our findings from this project, please go to the [Google Slides Presentation](https://docs.google.com/presentation/d/1DtTs9N8rKzuyIbOM5BIr9Fj5rrlIxkeOUFAeWmrXhq4/edit?usp=sharing). A pdf copy with speaker notes is also included in this repo as `W266_TranQuality-presentation.pdf`.

## Dataset Creation <a name="dataset-creation"></a>
* `paraphrase_wo_pb_dataset_creation.ipynb`: creates multilingual paraphrase training, validation, and test sets without Punjabi records
* `paraphrase_w_pb_dataset_creation.ipynb`: updates the previously created paraphrase training, validation, and test sets by adding Punjabi records
* `deduplicate_val_test.ipynb`: reforms the paraphrase validation and test sets after the existence of duplicate records were found

## Siamese Models <a name="siamese-models"></a>
### Model Notebooks <a name="siamese-model-notebooks"></a>
* `bestsnn_Pb.ipynb`: the best performing SNN, trained on Hindi, Tamil, Malayalam, and Punjabi
* `snn_w_Pb_sep_models.ipynb`: create an Aryan-only model (Hindi and Punjabi) and a Dravidian-only model (Tamil and Malayalam); shows diminished Dravidian language accuracy
* `snn_woPb.ipynb`: the original SNN, trained on only Hindi, Tamil, and Malayalam

### Model Weights and Bias Checkpoints <a name="siamese-w-b"></a>
Contains the weights and biases for the SNN models created in `Model Notebooks`.

### Best Siamese Evaluation <a name="best-siamese-eval"></a>
* `bestsnn_choose_best_record.ipynb`: finds the best-translation (IndicTrans vs MBart) for each target translation in each language (Hindi, Tamil, and Malayalam), as measured by the highest paraphrase probability assigned by the best SNN model; calculates language-specific SacreBleu scores on the ensemble corpus
* `bestsnn_ensembletranslator_eval.ipynb`: explores the cosine similarity between translation and target and edit distance between translation and target text for each language in our record-filtered corpus, as well as the solo-translator translations.
* `bestsnn_model_mistakes.ipynb`: analysis of best SNN model mistakes on paraphrase test set
* `bestsnn_mbart_trans_eval.ipynb`: assigns a paraphrase probability score to each MBART translation using the best SNN
* `bestsnn_indictrans_trans_eval.ipynb`: assigns a paraphrase probability to each IndicTrans translation using the best SNN
