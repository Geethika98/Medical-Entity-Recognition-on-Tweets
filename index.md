# Medical Entity Recognition

## Introduction & Problem Statement
Medical Entity Recognition(MER) is an application of a very famous problem in the field of Information Extraction(IE) i.e. Named Entity Recognition(NER). This project aims at parsing named entities and in this project, we have to recognize and classify medical data into the relevant categories, namely drugs, diseases, symptoms, side-effects, treatment, etc. Twitter data will be the input and based on previous medical data from databases and ontologies, relevant medical terms have to be parsed and classified (medical named entities are recognized and classified based on the category they belong to (ex: drug or a disease or cure etc....)
<br/>
As the name suggests, a Medical Name Entity Recognizer identifies medical entities in text. Medical entities, in the context of our project, are fixed, there are 5 categories as mentioned above. Previously, researchers in the field have used hand crafted features to identify medical entities in medical literature. In this project, we have to extend medical entity recognition on tweets. We would use NLP toolkits designed for processing tweets along with other medical ontologies (or databases) to exploit semantic features for this task. We attempt to push the accuracy beyond what has been obtained so far. As tweets are highly disorganised and prone to inconsistencies, our work includes filtering out all these inconsistencies.


## Dataset
We used the following datasets - 
1) CADEC Dataset : It is a corpus of medical forum posts on patient-reported Adverse Drug Events (ADEs). 
2) TwiMed Dataset
3) Micromed Dataset : This dataset was described in MedInfo 2015 paper from IBM Melbourne Research lab. It 
consists of tweet annotations with medical entities. (three types of entities: Disease (T047 in UMLS), Symptoms (T184), and Pharmacologic Substance (T121) 

<br/>

The above two datasets are already available but these datasets were very small in size, hence not sufficient for training.
We have increased the size of the dataset that is available for training heuristically.

For this, we were given three resources,

R1 : A list of hashtags, which are relevant to the medical domain
R2 : A general tweet corpus (about 40-50 GB in size)
R3 : A list of medical terms and their appropriate categories.

Using the list of hashtags (R1) we obtained a new dataset consisting of a subset of the general tweet corpus (R2) - medical domain related tweets. This new dataset was used both for training as well as testing purpose.
A part of this new dataset can be annotated using R3 and was used for training purposes. The rest of the dataset was used for testing purposes.



## Our Approach
We use more than the traditional Machine Learning and Deep Learning techniques that use bag of words featurizer. We use models that utilize the grammatical structure of a sentence. 
Models omitting the structural semantics of a sentence give an increasing number of false positives. This can be understood by the following example:
1. Humans are not Ni\*gers. `Not Hatespeech`
2. Ni\*gers are not humans. `Hatespeech`
  
Our code can be found [here](https://github.com/yp201/structure-based-hate-speech-detection).

### Dataset Preprocessing 
To use the tweets, we had to clean them:
- Convert tweet to lower case
- Remove 'RT' from every tweet (Keyword that identifies whether a tweet is re-tweet) 
- Remove special characters that don't contribute positively to accuracy (ex hashtags)
- Remove URLs


### Models and Results
We implemented SVM and Logistic Regression as baseline models and a simple LSTM and a tree LSTM to capture the structure of sentences. We also implemented a model based on structured self-attention to extract interpretable sentence embedding.

#### Baseline Models
We trained Gensim Word2Vec model on our twitter corpus and later used the model to obtain word vectors.
Following are the evaluation metrics :

<br/>
<b> SVM </b>
+ Accuracy : 0.814
+ Precision : 0.815
+ Recall : 0.815
+ F1 Score : 0.815

<b> Logistic Regression </b>
+ Accuracy : 0.839
+ Precision : 0.843
+ Recall : 0.843
+ F1 Score : 0.843

#### Structured Self-Attentive Sentence Embedding
We used a model for extracting an interpretable sentence embedding by using self-attention. Instead of using a vector, we use a 2-D matrix to represent the embedding.

Following are the evaluation metrics:
+ Accuracy : 0.885
+ Precision : 0.885
+ Recall : 0.885
+ F1 Score : 0.885

#### LSTM Models
Simple LSTM model in principle does capture the structure of the sentence, but does not incorporate the structural dependencies presnet in the sentence explicitely. 
We also have implemented a Child-Sum Tree-LSTM model on the dependency tree of the sentence, which is better than the Simple LSTM model at preserving semantic information as it incorporates information from multiple child units.
Following are the evaluation metrics :

<br/>
<b> Simple LSTM Model </b>
+ Accuracy : 0.874
+ Precision : 0.861
+ Recall : 0.861
+ F1 Score : 0.861

<b> Tree LSTM Model </b>
+ Accuracy : 0.920
+ Precision : 0.920
+ Recall : 0.920
+ F1 Score : 0.920

## Conclusion
Tree-LSTM model gave the best results.
