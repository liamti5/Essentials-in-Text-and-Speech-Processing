# Essentials in Text and Speech Processing

## The Course
This Repository shows the final project we built for the course Essentials in Text and Speech Processing at the University of Zurich. This course introduces basic concepts in Natural Language Processing. Overall course goal: At the end of the course, students are familiar on a high level with the terminology, tasks and methods fundamental to natural language processing.

## The Project
Bestande was an academic review and rating platform which was very popular within UZH and ETH student communities. The overwhelming volume of reviews makes it challenging for its users to quickly grasp informative feedback from generic, less useful, or even hateful comments. Another challenge is that people can find reviews in different languages due to the big international communities present at the university environment. In this report, we present an application of Natural Language Processing techniques to determine the usefulness and relevance of reviews, where comments not originally in German were translated, amplifying in this way the corpus of reviews. We achieved an accuracy of 65% in tagging useful reviews using text classification models and a 90% in banning nonconstructive comments using automatic
hate speech recognition. 

### Datasets
Two major datasets are used in this project: Bestande backend ratings and reviews collection and the HASOC dataset,
1. Bestande terminated its service in 2022 and with the hope of someone taking over, the founder disclosed the database over 2016 and 2022 on Bestande.ch. Therefore, we took it without any data scraping and built our project on it. The corpus can be found in the data folder. 
2. The HASOC (Hate Speech and Offensive Content) German data set contains publications from different social networks that are classified according to two tasks. Task A handles a binary classification, where NOT label means Non Hate Offensive and HOF means Hate and Offensive. As per the second task, it performs a more detailed classification of the HOF samples, such as HATE for Hate Speech, OFFN for offensive, PRFN for profane, or NONE if the classification in Task A was NOT. The corpus can be found in the /data/HateSpeechRecognition folder

The original datasets, as well as the preprocessed datasets and their respective divisions into training, testing, and validation datasets can be found under data/<nlp_task>

### Data Preprocessing
All the data preprocessing scripts can be found under code/.
- dataCleaning.ipynb : Created datasets for each language. Prepared the dataset for machine translation.
- dataPreprocessing_binary_ternary_usefulnessPredictor.ipynb : Labelling for binary classification
- dataPreprocessing_usefulnessPredictor.ipynb : Labelling for multiclass classification
  
### Model Training
#### Hate Recognition
Inspired by the paper Offensive Language Identification using a German BERT model, it was decided to use the bert-base-german-cased pre-trained model since it is a very popular and trained exclusively with about 12 GB of German texts. More details about training can be found in the hateRecognitionGerman notebook. 
 
#### Review Usefulness Prediciton
Different models were fine-tunned to evaluate automatically if a review would be useful for another person or not.
- usefulnessPredictor_BERT.ipynb : fine-tunning of bert-base-cased-german and bert-base-multilingual-uncased-sentiment for multiclass classification.
- usefulnessPredictor_binaryClassification.ipynb : fine-tunning of bert-base-cased-german for binary classification.
- usefulnessPredictor_distilbert-base-german-cased.ipynb : fine-tunning for multiclass classification
- usefulnessPredictor_distilbert-base-german-cased_binary.ipynb : fine-tunning for binary classification.

All the code for training and data preprocessing can be found in the code directory. 

## Models on Hugging Face
Both finetuned models can be found on Hugging Face: 
- Review Usefulness Prediction, binary classification: https://huggingface.co/jorgeortizv/reviewUsefulness-binaryClassification
- Hate Speech Recocnition: https://huggingface.co/jorgeortizv/BERT-hateSpeechRecognition-German
- Review Usefulness Prediction, Multiclass classification: https://huggingface.co/jorgeortizv/reviewUsefulness-multiclassClassification
