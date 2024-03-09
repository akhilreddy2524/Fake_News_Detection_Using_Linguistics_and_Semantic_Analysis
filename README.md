# Fake News Detection Using Linguistics and Semantic Analysis
## Project Description
This project investigates the efficacy of logistic regression, semantic analysis, and linguistic analysis in identifying fake news, aiming to develop an automated model for classification. By analyzing linguistic and semantic features, we aim to contribute to the fight against misinformation, protecting individuals and society from its harmful effects. Through rigorous testing and validation using a dataset comprising true and false news articles, we demonstrate the effectiveness of various feature extraction techniques, including n-grams and Named Entity Recognition (NER), with logistic regression models. Our findings underscore the importance of tailored approaches in fake news detection and emphasize the need for continued research to refine methods for combating misinformation effectively.
## Dataset Description
### Source
[https://www.kaggle.com/datasets/jainpooja/fake-news-detection/data]
### Description
The Kaggle dataset ”Fake News Detection” comprises two CSV files: ”fake.csv” and ”true.csv,” each containing approximately 25,000 rows of political news that may be true or fake. To aid in analysis, we added a new column ”label” to each dataset, assigning a value of 1 to true news and 0 to fake news. Afterward, we combined and shuffled the datasets to prepare for further processing. The resultant dataset has the following columns:
* Title: describes the context of the news
* Text: the news which has to be detected as true
or fake
* Date: the date when the news is published
* Label: 0 if the news is fake and 1 if true The link to the datasets has been provided in the references section.
## Methodology
The proposed technique comprises a coarse classifier and a pre-trained Convolutional Neural Network (CNN) consisting of two 2D convolution layers connected to layers of dense neurons. The algorithm for face mask detection is delineated as follows:
### A. Data Processing and Preprocessing
We started the project by cleaning and preprocessing the raw data using pandas and nltk library. First, we have removed the special characters present in the ’Text’ by using regular expressions. The next step is stop-word removal. The words that are generally filtered out before processing a natural language are called stop words. These are actually the most common words in any language (like articles, prepositions, pronouns, conjunctions, etc) and do not add much information to the text. Examples of a few stop words in English are “the”, “a”, “an”, “so”, and “what”. Stop words are available in abundance in any human language. By removing these words, we
remove the low-level information from our text in order to give more focus to the important information. In other words, we can say that the removal of such words does not show any negative consequences on the model we train for our task. Removal of stop words definitely reduces the dataset size and thus reduces the training time due to the fewer number of tokens involved in the training.
<br>After removing stop words, we have tokenized the data using nltk library. Tokenization is a simple pro- cess that takes raw data and converts it into a useful data string. Word tokenization is the most common version of tokenization. It takes natural breaks, like pauses in speech or spaces in the text, and splits the data into its respective words using delimiters (characters like ‘,’ or ‘;’ or ‘“,”’). The last step of preprocessing is POS tagging which means Parts of Speech tagging. This technique identifies to which POS a word belongs. NLTK provides various taggers such as the NLTK POS tagger, the Stanford tagger, and the Brill tagger. POS tagging helps in identifying the grammatical structure of the text, which is useful for tasks such as sentiment analysis, text classification, and information extraction.
### B. Feature Extraction
This is a significant step in our project. In Fake News Detection, Feature Extraction is one of the trivial steps to be followed for a better understanding of the context of what we are dealing with. After the initial text is cleaned, we need to transform it into features to be used for modeling. We need to understand the semantics of each of the news in order to determine if it’s true or fake. We employed different Feature extraction techniques like n-grams, Named Entity Recognition(NER), Sentiment Analysis, and TF-IDF. In addition, we have also used combinations of these techniques for better performance.
#### n-grams
N-grams is the process of extracting contiguous sequences of n words from a text. For example, in the sentence ”The quick brown fox jumps over the lazy dog,” the 2-grams (or bigrams) would be ”The quick”, ”quick brown”, ”brown fox”, ”fox jumps”, ”jumps over”, ”over the”, ”the lazy”, and ”lazy dog”. 3-grams (or trigrams) would be ”The quick brown”, ”quick brown fox”, ”brown fox jumps”, ”fox jumps over”, ”jumps over the”, ”over the lazy”, and ”the lazy dog”.
<br>N-grams are useful in fake news detection because they can capture patterns of language that are common in fake news. The dataset we used contains certain phrases or sequences of words that are often repeated across multiple articles. By analyzing the n-grams present in a text, we tried to identify certain patterns that are more common in fake news articles than in legitimate news articles. We used this in a machine-learning model to help distinguish between real and fake news articles.
#### Named Entity Recognition
Named Entity Recognition (NER) is a natural language processing technique that involves identifying and classifying named entities in text, such as people, organizations, and locations. NER is useful in fake news detection because it can help identify whether a news article is referring to real or fake entities.
<br>For example, a fake news article may refer to a nonexistent organization or person or may use a real name in a misleading or false way. By using NER to identify named entities in the article, it is possible to flag articles that contain fake or misleading information. This can be useful for a wide range of applications, such as information retrieval, question answering, sentiment analysis, and more.NER typically involves a combination of rule-based and machine-learning approaches. Rule-based systems use pre-defined patterns and heuristics to identify named entities based on their context within the text. Machine learning-based approaches, on the other hand, use annotated training data to learn statistical patterns and patterns in the text to identify named entities.
#### TF-IDF(Term Frequency-Inverse Document Frequency)
TF refers to the number of times a term appears in a document, and IDF refers to the inverse document frequency, which is a measure of how important the term is across a corpus of documents. The TF-IDF score for a term in a document is calculated as the product of its TF and IDF scores.
<br>One problem that we encounter in n-grams or other approaches is that it treats every word equally, but in a document, there is a high chance of particular words being repeated more often than others. In a news report about Biden winning the election, the word Biden would be more frequently repeated. We cannot give Biden the same weight as any other word in that document. In the news report, if we take each sentence as a document, we can count the number of documents each time Biden occurs. This method is called document-frequency.
<br>We then divide the term frequency by the document frequency of that word. This helps us with the frequency of occurrence of terms in that document and inverse to the number of documents it appears in. Thus we have the TF-IDF. The idea is to assign particular weights to words that tell us how important they are in the document. We have used this technique in combination with n-grams and NER for better performance.
#### Sentiment Analysis
Sentiment analysis can be used for fake news detection by analyzing the sentiment expressed in a news article and comparing it to the sentiment that would be expected based on the article’s content. For example, our data set contains a political news article that claims a certain candidate has made significant progress in their election campaign. Sentiment analysis of the article reveals that the sentiment is overwhelmingly positive, suggesting that the article is biased in favor of that candidate.
<br>However, further analysis of the article’s content may reveal that the claims are unsubstantiated or misleading, suggesting that the article is fake or misleading. By combining sentiment analysis with other natural language processing techniques, such as fact-checking or named entity recognition, it is possible to identify and flag fake political news articles that are designed to manipulate public opinion or spread false information.
<br>Moreover, articles that trigger emotions by using intense emotive words to attract the audience can be misleading. These articles can be identified by sentiment score and by using NER or fact-checking we can term those articles as fake or true.
### Train, Test, and Validation
After, feature extraction, the next step is to split the dataset for training, testing, and validating. We trained our model using a logistic Regression Classifier.
#### Logistic Regression
Logistic regression is a machine learning algorithm that can be used for fake news detection. The algorithm is typically used for binary classification problems, where the goal is to predict whether a given piece of text is real or fake news based on a set of input features.
<br>The algorithm is first trained on the labeled dataset of real and fake news articles. The input features include various text-based features such as the presence of certain keywords or n-grams, sentiment analysis scores, and named entity recognition results.
<br>Once the logistic regression model has been trained, it is used to predict the label (real or fake) of new news articles. The algorithm takes the input features of the new article as input and generates a probability score for each label. The label with the highest probability is then selected as the final prediction. One advantage of using logistic regression for fake news detection is that it is a simple and interpretable algorithm, which can make it easier to identify the key factors that are driving the classification decision.
#### K-Fold Cross Validation
K-fold cross-validation is a technique used in machine learning for evaluating the performance of a predictive model. The basic idea behind k-fold cross-validation is to split the dataset into k equally sized subsets or folds. The algorithm is then trained on k-1 folds and tested on the remaining fold. This process
is repeated k times, with each fold being used as the test set once, and the average performance across all k-folds is used as the final performance metric.
<br>K-fold cross-validation is used in fake news detection to evaluate the performance of the machine learning model, and logistic regression on the dataset considered. By using k-fold cross-validation, the performance of the model can be estimated more accurately than with a single train-test split because it accounts for the variability in the data and reduces the risk of overfitting.
<br>In practice, k-fold cross-validation is used by first splitting the dataset into k-folds, then training the model on k-1 folds and evaluating its performance on the remaining fold. This process is repeated k times, with each fold being used as the test set once. The performance of the model is then calculated as the average performance across all k-folds.
<br>One of the advantages of using k-fold cross-validation is that it allows for a more robust evaluation of the model’s performance, especially when the dataset is small or when the model is prone to overfitting. Additionally, by using k-fold cross-validation, it is possible to compare the performance of different models and select the best one for fake news detection.
## Result
Our preliminary results indicate that all the feature extraction techniques used have shown a decent performance with the logistic regression model. However, n-grams have the highest accuracy, followed closely by Named Entity Recognition n-grams combi- nation and NER alone. At last, the lowest accuracy is obtained for Sentiment analysis. However, the use of n-grams has given an accuracy of around 98% which is almost impossible in case of fake news detection. This suggests some ambiguity in the data set with regard to n-grams. The quality and characteristics of the dataset used can have a significant impact on model performance. It’s possible that the n-grams in the text column were more informative and relevant for identifying fake news than the named entities identified by the NER algorithm.
### Named Entity Recognition
The results demonstrate that this feature has a moderately strong correlation with the target variable, indicating that it is a relevant predictor for the model. However, there may be other features that have a stronger influence on the outcome. Therefore, it is recommended to keep this feature in the model, but also to explore the potential impact of additional features.
<br><img src="images/ner_results.png" width="300"><br>
### Sentiment Analysis
The analysis shows that this feature has a very low correlation with the target variable, indicating that it has little predictive power. It may be worth considering removing this feature from the model, as it is unlikely to contribute significantly to the overall performance.
<br><img src="images/sentiment_analysis_results.png" width="300"><br>
### N-grams
The results show that this feature significantly con- tributes to the model’s predictive power. The high correlation between this feature and the target variable suggests that it is an important factor in determining the outcome of the model.
<br><img src="images/ngrams_results.png" width="300"><br>
### NER and n-grams combination
The results indicate that this feature plays a crucial role in enhancing the predictive capability of the model. The strong association between this feature and the target variable implies that it holds substantial importance in determining the model’s outcome.
<br><img src="images/ner_ngrams_results.png" width="300"><br>
On the other hand, informal language often includes more colloquialisms, slang, and non-standard grammar, which can be more difficult for sentiment analysis algorithms to interpret. Additionally, informal language can sometimes use sarcasm, irony, or other figurative language that can be challenging for sentiment analysis models to recognize.
<br>Therefore, when creating a sentiment analysis or NER model, it is important to consider the type of language that will be used in the text data and adjust the model accordingly to maximize its performance.
## Conclusion
Based on our findings, it is clear that n-grams are a more effective technique than NER for detecting fake news. However, this finding is contingent on the dataset’s nature and content, as NER may be more useful for datasets that have multiple categories of news. Combining both techniques does not necessarily improve model performance, and sentiment analysis underperformed due to the informal language used in our dataset. Additionally, our study highlights the limitations of using sentiment analysis as a feature extraction technique for fake news detection. This technique may be more effective for datasets that contain formal text news.
<br>In conclusion, our study emphasizes the significance of carefully selecting appropriate feature extraction techniques and machine learning models for fake news detection. By doing so, we can improve our ability to identify fake news and curb the spread of misinformation. Our findings suggest that the size of the dataset used also affects model performance, and future studies could explore this relationship further. Overall, this study serves as a valuable resource for researchers and practitioners in the field of fake news detection.
## References
* Thorne, J., Vlachos, A., Christodoulopoulos, C., Mittal, A. (2020). COVID-19: A text classification approach to detecting fake news. arXiv preprint arXiv:2005.00033.
* Gilda, S. S., Desai, S. S., Patil, A. B. (2021). A Machine Learning Approach for Fake News Detection on Social Media. In 2021 4th International Conference on Intelligent Computing and Control Systems (ICICCS) (pp. 1101-1106). IEEE.
* Potthast, M., Ko ̈psel, S., Stein, B., Hagen, M. (2017). A stylometric inquiry into hyperpartisan and fake news. arXiv preprint arXiv:1702.05638.
* Shu, K., Mahudeswaran, D., Wang, S., Lee, D., Liu, H. (2018). Fake news detection on social media: A data mining perspective. ACM SIGKDD Explorations Newsletter, 20(1), 22-36.
* Castillo, C., Mendoza, M., Poblete, B. (2011, November). Information credibility on Twitter. In Proceedings of the 20th International Conference on World Wide Web (pp. 675-684).
* Wang, Y., Huang, J., Huang, X. (2020). Combining linguistic and network features for detecting online fake news. Information Processing Management, 57(1), 102091.
* ”Fake News Detection Using Logistic Regression and Linguistic Features” by R. Vijayarani and R. Swetha, International Journal of Computer Science and Information Security, vol. 16, no. 1, pp. 132-138, 2018. This paper describes a method for detecting fake news using logistic regression and linguistic features such as sentiment analysis and readability.
* ”Detecting Fake News Using Semantic Analysis” by N. V. Khan and M. A. Basalamah, Journal of Physics: Conference Series, vol. 1361, no. 1, 2019. This paper presents a method for detecting fake news using semantic analysis and logistic regression with features such as lexical similarity and polarity.
* ”Fake News Detection Using Machine Learning: A Review” by N. Elsayed and N. Al-Hassan, International Journal of Computer Applications, vol. 180, no. 40, pp. 36-44, 2018. This paper provides an overview of different methods for detecting fake news, including logistic regression and semantic analysis.
* ”Fake News Detection on Social Media: A Data Mining Perspective” by A. Zubiaga et al., ACM Transactions on Management Information Systems (TMIS), vol. 10, no. 3, pp. 1-22, 2019. This paper presents a method for detecting fake news on social media using data mining techniques such as logistic regression and feature engineering.
