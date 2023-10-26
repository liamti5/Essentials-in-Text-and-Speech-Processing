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

### Model Training
#### Hate Recognition
Inspired by the paper Offensive Language Identification using a German BERT model, it was decided to use the bert-base-german-cased pre-trained model since it is a very popular and trained exclusively with about 12 GB of German texts. More details about training can be found in the hateRecognitionGerman notebook. 
 
#### Review Usefulness Prediciton
To generate a prediction of the usefulness of a review it was decided to fine-tune a pretrained model. As first approach, the bert-base-multilingual-uncased-sentiment was selected since it is a popular Text Classification model used to predict the sentiment of a review on a scale 1 to 5. This model was trained with 137k German reviews which is roughly 20% of the corpus. However, the fine-tuned model performed poorly achieving a 50% accuracy with different training argument configurations using the multi-class classification Bestande data set. One possible explanation for this is that as a multilingual model, it is not only trained with German data, but also with other languages. For this reason it was decided to use again the bert-base-german-cased for the multi-class classification (usefulnessPredictor BERT.ipnyb). The best performance model achieved a 68% training accuracy and 61% training accuracy. The model however failed to generate
predictions for classes 2 and 3. All the code for training and data preprocessing can be found in the code directory. 

## Models on Hugging Face
Both finetuned models can be found on Hugging Face: 
- Review Usefulness Prediction: https://huggingface.co/jorgeortizv/reviewUsefulness-binaryClassification
- Hate Speech Recocnition: https://huggingface.co/jorgeortizv/BERT-hateSpeechRecognition-German
