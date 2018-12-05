## Project Overview
Ever thought the waiting period for your question posted on StackOverflow?
The average response time on StackOverflow is 3.71 days, Too Long!!!
Want your question to be answered earlier, or want an answer to your question immediately until some developer drafts it.
Then this project is for your help.

### StackBot: A bot that answers your question based on StackOverflow answers.

The engineering behind it: It is based on NLP with 2 algorithms:

1. Multi-label classification: Top 20 tags are fetched from the question and based on the probability of the occurrence of tags, it finds the most similar question and returns the answer to that question.

2. Cosine Similarity: After the user enters the question, it finds the most similar question based on cosine similarity, and returns the answer to that question.

Comparing the 2 algorithms, the multi-label classification turns out to be more accurate in answering the question.

Ongoing Work: Convolution Neural Networks for classification: This would make the question invariant to shift due to the max pooling thus giving a good accuracy even when the question is changed in terms of synonyms or tenses or active/passive voice.


## Step by Step Process:

### Data Required:

StackOverflow questions, questions description, answers, best answer, votes, date, tags, subtags, and views.

### Data Collection:

‘Selenium’ to automate the web browser to enter the tag, navigate between questions, navigate between the pages, and navigate to next set of questions dynamically.
‘BeautifulSoup’ to extract the questions, questions description, answers, best answer, votes, date, tags, subtags, and views for every static page of questions.
Data Preprocessing:

Delete all the questions that have not been answered yet. Deleting is a necessary step, else some questions will have a NULL answer.


### Model Training:

We first replace the tags of every question with the top 10 tags to avoid underfitting of the tags. Then use the MultilabelBinarizer to extract the tags and transform the tags into CountVectorizer Sparse Matrix. This step allows faster computation for model fitting.



After transformation, we implement – Naive Bayes, Decision tree, kNN, Multilayer Perceptron, and Support Vector Classifier to perform multi-label classification. F1 Score is calculated to compare the algorithms.
And the best model is used to return the answer.

 
### Demo
To test the utility of our implementation, we compare two scenarios:

1. The time taken for our implementation (question – > classification -> filtered fetching->
cosine similarity within subset -> result)
2. The time taken for a general implementation (question – > general fetching [no
classification] -> result)

To test the scenarios, a question like ‘use of neural networks with python and pandas’ was entered.

anss
The classification model successfully classifies it as [‘python’,’pandas’] and takes a time of
0.059 milliseconds to fetch the similar questions.

When the same question was asked for the second scenario.

The time taken for fetching similar questions was 0.064 milliseconds.

Hence, Multi-label classification increases the speed for fetching similar question. As the dataset for Q&A would scale up, like 1 million samples, this difference would be considerably high.

 

### Conclusion:

In all, I used Selenium to automate the web browser to log in, search, and navigate pages dynamically. And for every static page, we used BeautifulSoup to extract all the questions, question description, tags, best answer, votes, date posted, subtags, and many other features.

Then I built a model which is first trained with multiple algorithms, and the best algorithm is selected to classify the question into its possible tags. Only the top 10 tags are considered for the model training. This best algorithm has given an f1 score of 81%, which is very good in multi-label classification.

And then, cosine similarity is calculated to find the top 3 most similar questions. Based on the question selected, the best answer is returned.

This model is well equipped to be dynamic. The reach for the data can be extended to cross-validated, ExpertExchange, StackExchange, and many other platforms.

 

### Ongoing Work:

Convolution Neural Networks for classification: This would make the question invariant to shift due to the max pooling thus giving a good accuracy even when the question is changed in terms of synonyms or tenses or active/passive voice.

