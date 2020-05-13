# Entity Resolution Problem Statement

Journalists, academics, and businesses work hard to get big masses of data to learn about what people or organizations are doing. Unfortunately, once we get the data, we often can’t answer our questions because we can’t tell who is who.

In much real-world data, we do not have a way of absolutely deciding whether two records, say David Guy-Brizan and D Guy-Brizan are referring to the same person. If these were records of Professors at the University of San Francisco data, did a David Guy-Brizan give two lectures on two separate topics or did Desmond Guy-Brizan give the lecture on the second topic? Perhaps it could even be on completely separate topics.

People are pretty good at making these calls, if they have enough information. For example, I would be pretty confident that the following two records are the about the same person.


| first name | last name | Topic                   | hours   |
| --- | --- | --- | --- |
| David      | Guy-Brizan   | Machine Learning   | 2pm - 4pm Thurs |
| D          | Guy-Brizan   | Algorithms |   2pm - 4pm Tuesdays|

If we have to decide which records in our data are about the same person or organization, then we could just go through by hand, compare every record, and decide which records are about the same entity.

This is very, very boring and can take a long time. 

## What is Entity Resolution

Entity Resolution is the task of disambiguating manifestations of real world entities in various records or mentions by linking and grouping. For example, there could be different ways of addressing the same person in text, different addresses for businesses, or photos of a particular object. 

## What is the problem statement?

What is an entity? An entity as a unique thing (a person, a business, a product) with a set of attributes that describe it (a name, an address, a shape, a title, a price, etc.). 

That single entity may have multiple references across data sources, such as a person with two different email addresses, a company with two different phone numbers, or a product listed on two different websites.

If we want to ask questions about all the unique people, or businesses, or products in a dataset, we must find a method for producing an annotated version of that dataset that contains unique entities.

## Applications

This clearly has many applications, particularly in government and public health data, web search, comparison shopping, law enforcement, and more.

Entity Resolution can reduce the complexity by proposing canonicalized references to particular entities and deduplicating and linking entities. Deduplication significantly reduced the complexity of the network from a ninth order graph to a much simpler fourth order graph, of significantly less size.

## Challenges

Challenges to the ER discipline, least of which is the fact that there is no unified theory and, ironically, ER itself goes by many names! Other challenges like language ambiguity, poor data entry, missing values, changing attributes and formatting, as well as abbreviations and truncation mean that ER is a discipline that includes not just databases and information retrieval, but also natural language processing and machine learning.

Entity resolution is not a new problem, but thanks to Python and new machine learning libraries, it is an increasingly achievable objective.

## Entity Resolution Tasks

The three primary tasks involved in entity resolution are deduplication, record linkage, and canonicalization:

1. **Deduplication:** eliminating duplicate (exact) copies of repeated data.
2. **Record linkage:** identifying records that reference the same entity across different sources OR match records from one deduplicated data store to another.
3. **Canonicalization:** converting data with more than one possible representation into a standard form.

## Evaluating Entity Resolution Tasks

For pairwise metrics we consider Precision and Recall (e.g. F1 scores), as well as the cardinality of the number of predicted matching pairs.

## How to work with data in Entity Resolution

1. Data Preparation - VERY IMPORTANT
1. The first tasks are schema and data normalization. 
2. Schema attributes are matched (e.g. contact number vs phone number), and compound attributes like addresses are normalized.
3. Data normalization involves converting all strings to upper or lower case and removing whitespace. Data cleaning and dictionary lookups are also important.

The goal: 
1. To construct, for a pair of records, a “comparison vector” of similarity scores of each component attribute.
2.  Similarity scores can simply be Boolean (match or non-match) or they can be real values with distance functions.
3. Pairwise-Matching 
1. After we have constructed a vector of component-wise similarities for a pair of records, we must compute the probability that the pair of records is a match.
2. Two simple proposals are to use a weighted sum or average of component similarity scores, and to use thresholds.


# Scope of work

## Research: Understand existing SOTA systems for Entity Resolution and Record Linkage

Papers & Resources: 
- https://www.researchgate.net/publication/222669271_Entity_identification_for_heterogeneous_database_integration_-_A_multiple_classifier_system_approach_and_empirical_evaluation
- https://www.youtube.com/watch?v=2Drw9plALIM
- https://arxiv.org/pdf/1710.00597.pdf
- https://www.semanticscholar.org/paper/A-Machine-Learning-approach-to-Generic-Entity-in-of-Moir-Dean/6b1aa95d366cf692945361c66588ab80c5801880
- https://pathmind.com/wiki/word2vec
- https://www.slideshare.net/BenjaminBengfort/a-primer-on-entity-resolution
- https://source.opennews.org/articles/introducing-cvsdedupe/
- https://www.cs.utexas.edu/~ml/papers/marlin-dissertation-06.pdf

## Implementation: Create multiple models for Entity Resolution / Record Linkage
- https://pypi.org/project/fuzzywuzzy/
- https://dedupe.io/developers/
- word2Vec https://github.com/maxoodf/word2vec
- GloVe https://nlp.stanford.edu/projects/glove/
- fastText https://fasttext.cc/

## **Dedupe**

Dedupe is a library that uses machine learning to perform deduplication and entity resolution quickly on structured data.

1. It can remove duplicate entries from within a single dataset
2. It can also do record linkage across disparate datasets. 
3. Dedupe also scales fairly well 

Based on the number of papers I had read, and different strategies to approach ER, I found the Dedupe open source python library most useful in working with my data. 

https://github.com/dedupeio/dedupe
https://apidocs.dedupe.io/en/latest/index.html
https://docs.dedupe.io/en/latest/index.html

### How it works

Rather than treating each record as a single long string, Dedupe cleverly exploits the structure of the input data to instead compare the records field by field. 

The advantage of this approach is more pronounced when certain feature vectors of records are much more likely to assist in identifying matches.

Dedupe lets the user nominate the features they believe will be most useful:

Dedupe scans the data to create tuples of records that it will propose to the user to label as being either matches, not matches, or possible matches. They have a CLI that is easy to work with, a web API to use when customising your solution, and good documentation to learn more about their variable definitions. 

### Features of Dedupe

machine learning - reads in human labeled data to automatically create optimum weights and blocking rules

runs on a laptop - makes intelligent comparisons so you don’t need a powerful server to run it

built as a library - so it can be integrated in to your applications or import scripts

open source - anyone can use, modify or add to it

These uncertainPairs are identified using a combination of **blocking, affine gap distance, and active learning.**

Active learning is the so-called special sauce behind Dedupe. As in most supervised machine learning tasks, the challenge is to get labeled data that the model can learn from.

**Blocking**
1. Blocking is used to reduce the number of overall record comparisons that need to be made.
Dedupe’s method of blocking involves engineering subsets of feature vectors (these are called ‘predicates’) that can be compared across records. For example: 
- the first three digits of the phone number
- the full name
- the first five characters of the name
- a random 4-gram within the city name
2. Records are then grouped, or blocked, by matching predicates so that only records with matching predicates will be compared to each other during the active learning phase. 
3. The blocks are developed by computing the edit distance between predicates across records.
4. This edit distance is called Affine Gap Distance
**Affine Gap Distance**
1. In this algorithm, subsequent consecutive deletions or insertions are cheaper. We assign a value of 1 to insert, delete, and substitution of characters, and assign a value of 0.5 to consecutive insertions. 

**Active Learning**
1. The active learning phase in Dedupe is essentially an extended user-labeling session, which can be short if you have a small dataset and can take longer if your dataset is large.
2. The relative weight of these different feature vectors can be learned during the active learning process and expressed numerically to ensure that features that will be most predictive of matches will be heavier in the overall matching schema.
3. As the user labels more and more tuples, Dedupe gradually relearns the weights, recalculates the edit distances between records, and updates its list of the most uncertain pairs to propose to the user for labeling.


# Traditional Entity Resolution Techniques

**Deterministic, Rule-Based Approaches**

The traditional approach to this problem has been to write a series of rules. For example, if there’s
are records with “Bob” as the first name as well as “Robert,” you could write a rule says “If ​*first_name*
= ‘bob’, then convert to ‘Robert.’”

**OpenRefine vs Dedupe**

Many people use OpenRefine, the former Google Refine. It’s free, and a great tool for normalizing
data. We can use it here but take note of the following:

- OpenRefine doesn’t perform well beyond tens of thousands of records. 
- It doesn’t allow you to consider multiple attributes of a record at a time. And the single
attribute clustering requires human review for every cluster that’s created. 
- OpenRefine destroys the data that you provided, eliminating your ability to trace how a given record got into a cluster. So it’s not auditable. 

Nonetheless, OpenRefine is a great tool for normalizing. 

Use cases of Dedupe.io to:
- Find duplicate rows in a spreadsheet
- Link two or more datasets (as spreadsheets) and find overlapping records
- Continuously match new data to their “golden” datasets

*Entity Resolution with Machine Learning: A Scalable Foundation for Data Quality*

Dedupe lets you use as many attributes as you like simultaneously, getting you to “good” clusters quickly.


# Key Takeaways and Future Work 
- A possible approach to tweak and understand the underlying model in more detail is to to adjust the weights associated with each comparison field. 
- For instance, supposed we have the fields: 
  First name
  Last Name
  Paragraph Number 
  Sentence Number 
  Article Id 
  
  Here we can manually adjust and give increased weights to First Name, Last name, and Article Id, while decreasing the weights for Paragraph and Sentence.
  
 - Note however we really would rather not have to set the weights manually every time and it can be very tricky to know which fields are going to matter. Even if we know that some fields are more important than others, how do we quantify that? Is it 2 times more important or 1.3 times?

- At scale, Dedupe does help us do this already using regularized logistic regression. If we supply pairs of records that we label as either being duplicates or distinct, then Dedupe.io will learn a set of weights such that the record distance can easily be transformed into our best estimate of the probability that a pair of records are duplicates.

- Breaking up the data into more granular entries helps in the String matching and Active learning process immensely
- Human involvement is still very important during the training phase
- Adopt more methods to break up entry fields for a more nuanced comparison
