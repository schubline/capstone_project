# Explanatory Notes on things I used

# NLP
## How is sentiment score in TextBlob calculated.

TextBlob's NaiveBayesAnalyzer is apparently based on the Stanford NLTK. The analysis returns two values: polarity and subjectivity. The polarity score is a float within the range [-1.0, 1.0] where 0 indicates neutral, +1 a very positive attitude and -1 a very negative attitude. The subjectivity is a float within the range [0.0, 1.0] where 0.0 is very objective and 1.0 is very subjective.

Certain words will be labeled something like "40% positive / 60% negative" based on how they were used in some body of training data (for the Stanford NLTK, the training data was movie reviews). Then the scores of all words in your sentence get multiplied to produce the sentence score.

Suposedly, if the library returns exactly 0.0, then your sentence didn't contain any words that had a polarity in the NLTK training set. I suspect the researchers didn't include them because 1) they were too rare in the training data or 2) they were known to be meaningless (such as "the", "a", "and", etc.).

In my project, I was was decided to focus on `polarity` as that was the implicit user data I wanted to a certain and build a recsys on.I was also amenable to using TextBlob since it was trained on movie review data, an appropriate corpora.

## Latent Dirichlet Allocation (LDA)
Topic Modeling is a form of unsupervised learning, where the goal is to use a statistical model to attempt to identify topics or categories in a set of documents. One specific method of topic modeling is known as Latent Dirichlet Allocation (LDA, not to be confused with Linear Discriminant Analysis)

Latent Dirichlet allocation (LDA) is a generative statistical model that allows sets of observations to be explained by unobserved groups that explain why some parts of the data are similar.

### How does it work?
Each topic is a combination of words, and each document is a combination of topics.
1) Select a fixed number of topics
2) Radomly assigns a word to each Topic (this is for initialization purposes and has no inherent meaning at this point, hence random)
3) For each document *d*, word *w* and topic *t*, using Bayes' theorem we calculate
$$ P(t|w,d) $$

The probabilistic topic model estimated by LDA consists of two tables (matrices). The first table describes the probability or chance of selecting a particular part when sampling a particular topic (category). The second table describes the chance of selecting a particular topic when sampling a particular document or composite.

This means that:
- For every word in every document, we have a corresponding probability that a given word is a member of one of the topics
- We randomly reassign word `w` to a topic based on these probabilities
- We keep doing this process until we reach "convergence", defined as arriving at the optimal number of word assignment to topics.


### Why LDA
Chose LDA becase, in this case, I believe it was more appropriate to view the number of topics as a proportion of cluster membership. Using LDA would enable me to "soft" cluster the composite parts. This is more preferable to k-means where each element can only be a member of one cluster. I plain English, I wanted to have the same words be able to contribute to different topics instead of having them just contributing to one. This approach is more nuanced.
