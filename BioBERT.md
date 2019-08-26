# BioBERT: a pre-trained biomedical language representation model for biomedical text mining



## Why is it on demand?

1. Increasing need for biomedical information.
2. Using general models is not effective when the field is specified.

## What makes it hard?

1. Collecting biomedical information is a costly job.
   - It requires expert knowledges.
2. Biomedical texts have high probabilities of including unseen domain-specific terms.

## What are BERT and BioBERT?

1. BERT(Bidirectional Encoder Representation from Transformers)
   - A present language model that is pre-trained on general language corpus(Wikipedia, BooksCorpus).
   - Instead of using two unidirectional language models, it used a masked language model which predicts randomly masked words, resulting in better representations.
   - BioBERT is based on BERT, contextualized for biomedical texts.

2. BioBERT
   - The model that is proposed in this journal.
   - Domain-specific(biomedical) language representation model.

## How to construct BioBERT

1. Pre-training BioBERT
   - As biomedical information contains domain specific terms, training Word2Vec on biomedical corpora leads to better results. 
   - Initialized with BERT pre-trained on Wikipedia and BooksCorpus, BioBERT used biomedical corpora such as PubMed and PMC.
2. Improving performance of BioBERT
   - Use of WordPiece tokenization: a solution for OOV issues.
   - Named Entity Recognition: helpful for recognizing domain specific terms. Built upon LSTMs. Learned from WordPiece embeddings (not from PubMed or PMC)
   - Relation Extraction: Classification of relations between named entities. 
   - Question Answering

## Results



