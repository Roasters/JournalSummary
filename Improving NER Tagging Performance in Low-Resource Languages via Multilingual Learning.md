# Improving NER Tagging Performance in Low-Resource Languages via Multilingual Learning

## Motivations

1. Sparsity of language data
   - Collecting large corpus is a very costly job.
   - Small amount of corpus is easy to get but it arouses **sparsity problem**.
2. NER needs annotated corpus
   - Annotating large amount corpus is something humans should do, so a lot of time and effort are taken.

## Idea

By combining small amount of language features from multiple closely related languages, increase performance of NER tagging for low-resource languages. 



## Target languages: INDIAN LANGUAGES

*Dravian* and *Indo-Aryan* languages share the same set of phonemes and have some level of character similarities. Vocabulary and word order, too.



## cf.) Overview of NER History

1. **2003** First use of neural network for context understanding in NER.

2. **2011** First SUCCESSFUL use of neural network in several NLP tasks. Relied on small amount of hand-crafted language features or large amount of unannotated corpora.

3. **2014-2015** With fixed filters of Convolutional Neural Network, subword feature extraction became possible.

4. **2015** Use of LSTMs and CRFs respectively for word sequence encoding and tag sequence decoding.

5. **2016** Combine word-level CNNs and character-level CNNs on Bi-LSTM models.

6. **2018** Similar with the above models but excluded softmax at the output layer.

7. **Recently** Hierarchical Bi-LSTM: a character-level Bi-LSTM first and then a word level Bi-LSTM.

   ### Then what about multilingual approaches?

   - Multilingual learning is model independent, which means it is a matter of how to adjust input language data so it can be applied to any of above models.