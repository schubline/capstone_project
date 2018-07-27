# Natural Language Processing Technical Report

Packages used: https://pypi.org/project/langdetect/


# EDA and Cleaning the data

# Examining our Dataset
- Reviews from 11 Metropolitan Areas.
NV     1041833
AZ      920356
ON      458012
NC      201422
OH      169961
PA      158521
QC      111323
WI       75039
BW       25482
EDH      25250
IL       24174

## Verifying English language
First things first. We need to check which languages these reviews are actually
written in. Yelp's app is freeform  text, and subsequently, we need to ensure that we are dealing with english language reviews since that we want to model. Considered doing it manually, but given size and scope of data, we need to leverage a nice package called `langdetect` which allows us to detect the language of a review.

## Creating a `sentiment_score` feature
The idea behind this was to gain more insight from reviews before running them through the whole NLP regex tokenization rigmarole. I decided to use.

### Vader vs TextBlob
TextBlob is the appropriate tool for this.
- can deal with multiple sentences and give appropriate sentiment score
- Vader is better for when text is broken down by sentence, and analyzing those individually. They have great implementations for emojis, capitalization and word order, but given shape and size of my data, not appropriate, even if I could get that level of precision my breaking down reviews that way, not computationally feasible once I scale up. Will use as precision tool when looking at outliers (extremely bad vs extremely good).
