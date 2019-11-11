# Structure Based Hate Speech Detection

## Hate Speech
Hate speech is a kind of writing that disparages and is likely to cause harm or danger to the victim. It is a kind of speech that demonstrates a clear intention to be hurtful, to incite harm, or to promote hatred.

<b>Why automated hate speech detection?</b>
<br/>
While manual checking for such comments exists on social media, manual checking can never match to the speed of generation of comments on these sites and hence an automated solution is required.

## Dataset
We used a data-set with a corpus of tweets predominantly having offensive language that can be found [here](https://raw.githubusercontent.com/t-davidson/hate-speech-and-offensive-language/master/data/labeled_data.csv?fbclid=IwAR2h6bXVZA4Zh1EVkeGi5fhbnHChqeXxDRL2SCSix8v0SLdD2jhWTAKAz1U). It consists of a total of 24783 tweets. The data-set is skewed as there are relatively lesser number of data points under the hate-speech category.

Following is the distribution of different classes in the Twitter dataset:

|Type         |Count  |
|:-----------:|:-----:|
|Hate Speech  |1430   |
|Offensive    |19190  |
|Neither      |4163   |
|Total        |24783  |


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
