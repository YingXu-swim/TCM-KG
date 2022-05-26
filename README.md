# TCM-KG
Research on Knowledge graaph based on Chinese medicine

## 1 Word embedding training
step 1: Crawl a large number of TCM corpus.      
step 2: Word segmentation of the corpus through [Jiayan](https://github.com/jiaeyan/Jiayan).     
step 3: Train w2v through [gensim](https://github.com/RaRe-Technologies/gensim).      


## 2 Knowledge extraction     
The triples are extracted through pipeline method: NER and RE.      
### 2.1 NER    
Firstly, label the dataset. Set up LAB1 and LAB2 according to the labeling methods.     
Then, compare the result of BiLSTM-CRF model and Lexion model in each LAB.         

### 2.2 RE       
Firstly, obtain all named entities in the document according to the results extracted in LAB1.      
Then arrange and combine every two entities in documents, and  label the relationship between the two entities.    

In this experiment, 3 features are set:    
* Text features: text information, semantic information. And the text is represented in the form of embeddings;    

* Location feature: the location information of the entity.         

    For example, in the following example, the sentence is consists of 11 words, and [NAME],[QUANTITIES], [MEDICINE] and [SYMPTOM] are named entities. As for [QUANTITIES] in this sentence, it is at the position of 0 relative to itself, and the words on the left get smaller as the distance from aimed [QUANTITIES] increases. Similarly, words to the right of [QUANTITIES] will increase with distance.       

    The [NAME] consists of [QUANTITIES] [MEDICINE], can cure [SYMPTOM].     
    -1 0 1 2 3 4 5 6 7 8 9       

* Entity features: named entity information of the entity.     
  
Finally, compare the result of BiLSTM model, BiLSTM-attention model and HAN model.     


## 3 Knowledge graph construction
After knowledge extraction, knowledge can be represented in the form of triples, where triples are stored and trained to represent knowledge.
### 3.1 Knowledge representation
TransE model is used to train the knowledge representation.

### 3.2  Knowledge storage
The triples is constructes in Neo4j through [py2neo](https://github.com/py2neo-org/py2neo).
