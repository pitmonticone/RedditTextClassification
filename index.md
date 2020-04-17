# Reddit Gender Text-Classification

[**Team**](#team)

[**Overview**](#overview)

[**Solution**](#solution)

## Team

* [Monticone Pietro](https://github.com/pitmonticone)
* [Moroni Claudio](https://github.com/claudio20497)
* [Orsenigo Davide](https://github.com/dadorse)

## Overview 

### Description

[Reddit](http://www.reddit.com/) is an entertainment, social networking, and news website where registered community members can submit content, such as text posts or direct links, making it essentially an online bulletin board system. Registered users can then vote submissions up or down to organize the posts and determine their position on the site's pages. Content entries are organized by areas of interest called "subreddits". The subreddit topics include news, gaming, movies, music, books, fitness, food, and photosharing, among many others.

When items (links or text posts) are submitted to a subreddit, users (redditors) can vote for or against them (upvote/downvote). Each subreddit has a front page that shows newer submissions that have been rated highly. Redditors can also post comments about the submission, and respond back and forth in a conversation-tree of comments; the comments themselves can also be upvoted and downvoted. The front page of the site itself shows a combination of the highest-rated posts out of all the subreddits a user is subscribed to.

The Reddit website has an API and its code is [open source](https://github.com/reddit/reddit/#apis). In July 2015, a Reddit user identified as Stuck_In_the_Matrix [made public a dataset of Reddit comments](https://www.reddit.com/r/datasets/comments/3bxlg7/i_have_every_publicly_available_reddit_comment) for research. The dataset has approximately 1.7 billion comments and takes 250 GB compressed. Each entry contains comment, score, author, subreddit, position in comment tree and other fields that are available through Reddit's API.

One of the user attributes that is not natively supported by the Reddit platform is the gender. However, in some subreddits, users can self report their genders as part of the subreddit rules. In the scope of this competition, users that self reported their gender are selected from the dataset, and your goal is to predict the gender of these users.

### Evaluation 

The evaluation metric for this competition is the [Area Under the ROC Curve](https://en.wikipedia.org/wiki/Receiver_operating_characteristic). This metric is used to evaluate binary classification, and in the scope of this competition we are representing the gender of the users as binary classes: the class "female" is represented as 1 and the class "male" as 0. The class prediction for each Reddit author corresponds to your confidence that the author is a female, which is a "score" computed for the author (e.g. estimated probability in logistic regression).

#### Submission Format

**For every author in the dataset**, submission files should contain two columns: author and gender. The column author should be a string. The column gender can be any real value. The higher is your confidence that the author is female, the higher should be the corresponding value in the gender column.

## Data 

We selected a total of 20k users with self reported gender. Among these, we selected 5000 for training, and the remaining 15000 are used for evaluation. 

### File Descriptions

* **train_data.csv.gz**: contains all comments of the users selected for training
* **train_target.csv**: contains the genders of the users selected for training
* **test_data.csv.gz**: contains the comments of the users selected for evaluation
* **sample.csv**: a sample submission file in the correct format

### Data Fields

Each comment has the following structure:

* **author**: contains the username of the author
* **subreddit**: contains the subreddit in which the comment was posted
* **created_utc**: contains the date of submission in unixtime format
* **body**: contains the text of the comment

## Solution 

### Unsuccessful Models

An exploration of [SpaCy](https://github.com/explosion/spaCy) was performed. One may find the relevant notebooks [here](https://github.com/InPhyT/DataMiningChallange/tree/master/unsuccessful-models/spaCy). The model works and has a similar strategy to the one presented below, though its performance is lower (roc = 0.894). The exploration has been concluded with this [Stack Overflow question](https://stackoverflow.com/questions/60821793/text-classification-with-spacy-going-beyond-the-basics-to-improve-performance), this [GitHub Issue](https://github.com/explosion/spaCy/issues/5224) and a comment to a [Feature Request](https://github.com/explosion/spaCy/issues/2253#issuecomment-605502320). 
We've also tried [neural networks](https://github.com/InPhyT/DataMiningChallange/tree/master/unsuccessful-models/keras-neural-networks) with `Keras`.

### Successful Models

The training set has been grouped by author and the resulting texts, as if aggregated with `" ".join`, have been turned into a BOW (see this [brief Kaggle tutorial](https://www.kaggle.com/matleonard/text-classification#Bag-of-Words)). 

1. 80% of the resulting data has been used to train an [XGBoost](https://www.kaggle.com/alexisbcook/xgboost), which was later used to predict the remeining 20%.  
2. A [Document Embedding model](https://medium.com/wisio/a-gentle-introduction-to-doc2vec-db3e8c0cce5e) has been fitted on test and training texts. 80% of training vectors were later used to train a [Multi Layer Perceptron](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html), which then predicted the remaining 20% and the test set.
3. A MLP on the binary countvectorized subreddits has been trained, just like the models above. 
4. The predictions on the 20% of the XGBoost and of the two MLPs were used to train and validate a final logistic regression.  
5. Finally, a new XGBoost and and two new MLPs were trained on all train texts, and the predictions of the two used by the logistic regression to output the final submission.  

![](https://github.com/InPhyT/DataMiningChallange/blob/master/images/flow-chart.png)
