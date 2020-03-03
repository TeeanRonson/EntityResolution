# EntityResolution
Building a Model for Entity Resolution of People, Places, and Organisations

### What is ER?
Entity Resolution refers to the task of finding all mentions of same -real world entity within a knowledge base or across multiple knowledge bases. This can be achieved through linking and grouping.For example, there could be different ways of addressing the same person in text, different addresses for businesses, or photos of a particular object.

The goal of ER is to "resolve" entities, by identifying the records that represent the same entity and reconciling them to obtain one record per entity.

![alt text](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fmiro.medium.com%2Fmax%2F1276%2F1*6Vm_6I9dB3VPZeUrq8QUpQ.jpeg&f=1&nofb=1)

### ER Motivation 
In the modern world, the speed and volume of data has increased exponentially. Thus making inference across networks and semantic relationships between entities a greater challenge to overcome. Entity resolution can reduce the complexity by proposing canonicalised references to entities and deduplicating and linking entities.


### ER Tasks 
- Deduplication: The process of clustering/grouping records or mentions that represent the same real world entity.
- Record Linkage: The process of matching records from one deduplicated knowledge base to another.
- Canonicalisation: The process of converting data with more than one possible representation into a standard form.
- Reference Matching: The process of matching noisy records to clean ones in a deduplicated reference table.


# NLP
Natural language processing (NLP) is the ability of a computer program to understand human language as it is spoken. NLP is a component of artificial intelligence (AI).
The ultimate objective of NLP is to read, decipher, understand, and make sense of the human languages in a manner that is valuable.

Comprehensively understanding the human language requires understanding both the words and how the concepts are connected to deliver the intended message.

### What techniques do we use in NLP?
Syntactic analysis and semantic analysis are the main techniques used to complete Natural Language Processing tasks.

### Syntax
Syntax refers to the arrangement of words in a sentence such that they make grammatical sense.
In NLP, syntactic analysis is used to assess how the natural language aligns with the grammatical rules.
Computer algorithms are used to apply grammatical rules to a group of words and derive meaning from them.

### Semantics
Semantics refers to the meaning that is conveyed by a text. Semantic analysis is one of the difficult aspects of Natural Language Processing that has not been fully resolved yet.
It involves applying computer algorithms to understand the meaning and interpretation of words and how sentences are structured.

#### F measure 
The F1 score is the harmonic mean of the precision and recall, where an F1 score reaches its best value at 1 (perfect precision and recall) and worst at 0.

#### True Positive 

#### False Positive 

#### Precision 
Precision is the fraction of relevant instances among the retrieved instances. p is the number of correct positive results divided by the number of all positive results returned by the classifier

precision is "how useful the search results are", and recall is "how complete the results are".

#### Recall 
is the fraction of the total amount of relevant instances that were actually retrieved.r is the number of correct positive results divided by the number of all relevant samples (all samples that should have been identified as positive)

### V measure 
The V-Measure is defined as the harmonic mean of homogeneity and completeness. of the clustering. Both these measures can be expressed in terms of the mutual information and entropy measures of the information theory. Homogeneity is maximized when each cluster contains elements of as few different classes as possible.

### Entropy


# Neural Network 
Learning in a neural network is allowing the computer to find the right weights and biases for each neuron in the network. 
In a Neural Network, neurons fired up in the first layer will activate other neutrons in the second layer until we arrive at the final layer which is a guess of what the outcome is based on how many choices we have. 

# Papers
https://www.sciencedirect.com/science/article/pii/S1877050916324796



