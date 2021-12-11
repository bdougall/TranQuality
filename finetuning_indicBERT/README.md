# Fine tuning IndicBERT

## Table of Contents  
- [1. Fine tuning - Search for the best model](#Model-Exploration)  
- [2. Find the best model ](#Find-the-best-model)
- [3. Score and save the logits](#score)
    - [Tamil](#tamil)
    - [Hindi](#hindi) 
    - [Malayalam](#malayalam) 
- [4. Final model](#final)
    - [Tamil](#4tamil)
    - [Hindi](#4hindi) 
    - [Malayalam](#4malayalam)
- [5. Error analysis](#error)
    - [Tamil](#5tamil)
    - [Hindi](#5hindi) 
  

## 1. Fine tuning - Search for the best model <a name="Model-Exploration"></a>
[`1. finetune_paraphrase.ipynb`](1.%20finetune_paraphrase.ipynb) : Search the hyperpameter space and train multiple models.

## 2. Find the best model <a name="Find-the-best-model"></a>
[`2. best-models.ipynb`](2.%20best-models.ipynb) : List the best model from the hyper parameter space for each language.


## 3. Score and save the logits <a name="score"></a>
### Tamil <a name="tamil"></a>
[`3a. scoring-and-saving-logits-tamil.ipynb`](3a.%20scoring-and-saving-logits-tamil.ipynb) : 
This note book has 6 main steps:

* Load the checkpoint
* Score the file created by mBART by translating english to tamil
* Score the file created by IndicTrans by translating english to tamil
* Combine the logits from step 2, step 3, with the original sentence and the translated senences. This is also saved for further analysis
* Apply softmax on the logits from step 2 and 3, resulting in selecting the better translations
* Run sacreblue on the a. mBART translations with reference to original b. IndicTrans translations with reference to original c. selected translations with reference to original
* If our hypothesis worked, we should have sacreblue from step 6c better than 6a or 6b

### Hindi <a name="hindi"></a>
Same as 3a but for Hindi
[`3b. scoring-and-saving-logits-hindi.ipynb`](3b.%20scoring-and-saving-logits-hindi.ipynb) 

### Malayalam <a name="malayalam"></a>
Same as 3a but for Malayalam
[`3c. scoring-and-saving-logits-malayalam.ipynb`](3c.%20scoring-and-saving-logits-malayalam.ipynb) 

## 4. Final model <a name="final"></a> 
This is where we build the final model and save the checkpoints
### Tamil <a name="4tamil"></a>
[`4a. final-model-ta.ipynb`](4a.%20final-model-ta.ipynb)

### Hindi <a name="4hindi"></a>
[`4b. final-model-hi.ipynb`](4b.%20final-model-hi.ipynb)

### Malayalam <a name="4malayalam"></a>
[`4c. final-model-ma.ipynb`](4c.%20final-model-ma.ipynb)


## 5. Error analysis <a name="error"></a>
In these notebook we will explore where the model is misclassifying and provide some thematic reasons for them. We will not delve into detailed scientific analysis though. It for the next chapter of this project ;)

### Tamil <a name="5tamil"></a>
[`5a.error-analysis-ta.ipynb`](5a.error-analysis-ta.ipynb)

### Hindi <a name="5hindi"></a>
[`5b.error-analysis-hi.ipynb`](5b.error-analysis-hi.ipynb)




The checkpoints and other output files can be found [here](https://drive.google.com/drive/folders/1rm0M1_W_WtV51RiV6SiAoqBrAJxSrRYa)
