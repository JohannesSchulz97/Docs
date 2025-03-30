semi-supervised learning: model is trained on a **small** amount of labelled data and a **large** amount of unlabeled data. 
The labelled data helps to learn the task, the unlabelled data helps to generalize to new examples. 

Large Language Models are a subset of Deep Learning.
Generative AI is a subset of Deep Learning. 

Gen AI is a type of AI that creates new content based on what it has learned from existing content.

ML models can be divided into two types: 
- generative models: 
    - learns $P(X,Y)$
    - learns to generate new data instances based on the learned probability distribution of the training dataset.
- discriminative models: 
    - used to predict outputs for new data
    - learns $P(Y|X)$
    - learns to predict labels or continuous output values (regression and classification)

The power of Gen AI comes from the use of Transformers.
Transformers consist of: 
- Encoder
- Decoder
Hallucinations can happen due to:
- not enough data
- dirty data
- not enough context
- not enough constraints

There are spcific LLMs, such as Text-to-Text, Text-to-Image, Text-to-Task, ...
Additionally, there are Foundation models. 
They are trained on a wide range of data (text, image, speech, structured data, 3D signals).



# DeepLearning AI: How Transformer LLMs Work

## Approaches to represent language numerically

### Bag of Words

- represents words as large sparse vectors, based on a vocabulary. So each word in the vocabulary is represented by a certain position in the vector.
- simply encode the presence of a word

### Word2Vec

- capture the meaning of words in the context of a few neighboring words

### Transformers

- capter the meaning of words in the context of sentences and paragraphs

Encoder-only models are great at representing language numerically. 
Decoder-only models are generative, generating text
There are also combinations.

 






