# Medical Entity Recognition on Tweets

## Introduction & Problem Statement
Medical Entity Recognition(MER) is an application of a very famous problem in the field of Information Extraction(IE) i.e. Named Entity Recognition(NER). This project aims at parsing named entities and in this project, we have to recognize and classify medical data into the relevant categories, namely drugs, diseases, symptoms, side-effects, treatment, etc. Twitter data will be the input and based on previous medical data from databases and ontologies, relevant medical terms have to be parsed and classified (medical named entities are recognized and classified based on the category they belong to (ex: drug or a disease or cure etc....)
<br/> <br/>
As the name suggests, a Medical Name Entity Recognizer identifies medical entities in text. Medical entities, in the context of our project, are fixed, there are 5 categories as mentioned above. Previously, researchers in the field have used hand crafted features to identify medical entities in medical literature. In this project, we have to extend medical entity recognition on tweets. We would use NLP toolkits designed for processing tweets along with other medical ontologies (or databases) to exploit semantic features for this task. We attempt to push the accuracy beyond what has been obtained so far. As tweets are highly disorganised and prone to inconsistencies, our work includes filtering out all these inconsistencies.


## Dataset
We used the following datasets - 
<br/>
+ <b> CADEC dataset </b> : It is a corpus of medical forum posts on patient-reported Adverse Drug Events (ADEs). 
+ <b> TwiMed Dataset </b>
+ <b> Micromed Dataset </b> :  This dataset was described in MedInfo 2015 paper from IBM Melbourne Research lab. It 
consists of tweet annotations with medical entities. (three types of entities: Disease (T047 in UMLS), Symptoms (T184), and Pharmacologic Substance (T121) 

<br/>

The above two datasets are already available but these datasets were very small in size, hence not sufficient for training.
We have increased the size of the dataset that is available for training heuristically.

For this, we were given three resources, <br/>

+ R1 : A list of hashtags, which are relevant to the medical domain
+ R2 : A general tweet corpus (about 40-50 GB in size)
+ R3 : A list of medical terms and their appropriate categories. <br/>

Using the list of hashtags (R1) we obtained a new dataset consisting of a subset of the general tweet corpus (R2) - medical domain related tweets. This new dataset was used both for training as well as testing purpose.
A part of this new dataset can be annotated using R3 and was used for training purposes. The rest of the dataset was used for testing purposes.



## Our Approach
<b> Model Preparation : </b> MER can be implemented as a sequence classification task, where every chunk is predicted IOB-style as Drug, Disease, Symptom, Treatment and Test. The IOB format (short for inside, outside, beginning) is a common tagging format for tagging tokens.

We have used Keras to implement a bidirectional multi layer rnn cell (LSTM).  We have used a softmax layer as the last layer of the network to produce the final classification outputs. We tried working with different optimizers and we found that AdamOptimzer produced the best results. To calculate the F1 Scores, Prediction Accuracy and Recall we use seqeval library.

 To improve upon the previous models we tried combining both LSTM and CRF so as to get the benefits of both. LSTM is used to replace the linear scoring function of CRF so as to get a non-linear and more expressive function. CRF on the other hand helps in detecting complicated named entities which is predominant in medial entities. 
 
 Continuing with the model above we have added a CNN architecture along with the character embeddings and before we combine both the word embeddings and character encodings which is then fed to the main Bi-LSTM. Since medical data is sparse, we have to have a model which can predict the labels even with the small amount of data fed to it. 
  
Our code can be found [here](https://github.com/adisarip/medical_entity_recognition).

### Dataset Preprocessing 
+ The datasets available to us did not contain all the desired labels, hence we had to preprocess the datasets availble to us. The specific approaches that we have used to preprocess our datasets is explained in detail in the project report, whose link is provided below.
<br/>

+ Twitter Data Preprocessing : We had to clean up the twitter data and then extract the medical tweets.


## Models and Results
The following results are on CADEC, TwiMed and Micromed Dataset(combined). One of the issues with all these datasets is that these are annotated by different people so a concept in one dataset could be annotated  differently in another. But we have assumed that are concepts are annotated uniformly across datasets. 


## Analysis of results from experiments
The trained model performs reasonably fine although even after applying the CNN-LSTM-CRF model we still get some misclassified words and in some cases the model predicts logically correct labels even though it does not match with the actual label because of the context of the given sentence and the word being multi-label.  Also some words have been categorised under multiple labels by our model due to the presence of the same  in the given dataset. In some instances the model logically extend the label to include other words as well which is not present in the dataset but is logically correct. These statistics are not captured by the above given evaluation metric. 

### Challenges we faced
+ As the rules and features for the medical data was different from that of ordinary data, this problem was more challenging when compared to named-entity-recognition problem on normal data.<br/>
+ Twitter data is user-generated social media text, thus, it was highly disorganized and prone to inconsistencies. They contained a lot of noise apart from the required information. Filtering the noise/inconsistencies out from the tweets was a major challenge for our project as these affected the performance drastically.
<br/>
+ Learning distributed representations for medical tweets. (this can overcome the weaknesses of ‘bag-of-words’ models)
<br/>
+ We had to identify the relevant content from a given tweet. (For example, all tweets containing the keyword ‘morphine’ might not about the drug ‘morphine’)
<br/>

### Practical Applications
+ From the results obtained, we can get the specific details of any disease that has widely spread in a particular area.  <br/>
+ Results could be analysed to find the the patient's feedback/response for a particular drug, the effectiveness of a particular drug (how far it has been successful in treatment and what are the negative points) <br/>
+ Results can be utilised by companies producing medical products for improving their sales. <br/>

## Links 
Our code along with a detailed project report can be found [here](https://github.com/adisarip/medical_entity_recognition). <br/>
A video describing the procedure and results and the dataset used can be found [here](https://drive.google.com/drive/folders/1XLysnpBP7nejFEpv1GwwqYn1u-3I83zK?usp=sharing). <br/>



