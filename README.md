# W266_Project

## Table of Contents  
- [Overview](#overview)  
- [Presentation of Findings](#presentation)
- [Dataset_Creation](#dataset-creation)

## Overview <a name="overview"></a>
In our project, we implement paraphrase-matching to evaluate the translation qualities produced by two transformers (IndicTrans and MBart). We seek to determine if filtering records by the resultant paraphrase scores results in a corpus of improved translation quality.

## Presentation of Findings <a name="presentation"></a>
To see a high level overview of our findings from this project, please go to the [Google Slides Presentation](https://docs.google.com/presentation/d/1DtTs9N8rKzuyIbOM5BIr9Fj5rrlIxkeOUFAeWmrXhq4/edit?usp=sharing).

## Dataset Creation <a name="dataset-creation"></a>
#### `paraphrase_wo_pb_dataset_creation.ipynb`

Concatenates the Hindi, Tamil, and Malayalam training datasets from the Amrita paraphrase corpus to form 1 training data set, shuffling the training data so that multiple languages are present in each training batch. Randomly split the records in each of the Hindi, Tamil, and Malayalam test datasets into half, uses half of each language's test data to form 1 validation dataset, and uses the other half of each language's test dataset for the test dataset used to test paraphrase model final performance.

#### `paraphrase_w_pb_dataset_creation.ipynb`

Takes the Punjabi training and test datasets from the Amrita paraphrase corpus to create Punjabi training, validation, and test datasets, using the same procedure as in `paraphrase_wo_pb_dataset_creation.ipynb` to create the Punjabi validation and test datasets. Add the Punjabi training, validation, and test datasets to a copy of the paraphrase train, validation, and test datasets. Reshuffle the paraphrase training data so that the added Punjabi records are distributed throughout.
