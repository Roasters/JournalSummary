# Learning Tag Dependencies for Sequence Tagging

## Motivation

- Sequence tagging is one of the most important tasks in NLP.
- Tag sequence dependencies have been less considered compared to token sequence dependencies; contextual information is used when treating tokens but tags are predicted independently as an isolated output from each token.
- Need to develop a new model which can handle both token and tag dependencies and their interactions.

## Approaches

1. A transition matrix between two consecutive tokens formalized as a CRF layer.
   - Works better than isolated tag criterion. 
   - However, the transition matrix does not catch the order of sequences because it only captures the neighboring tag dependencies; does not work properly for long range of tokens.

2. Multi-channel model with three variants.

   - The model is trained on both the word context representation and tag dependency features.

   - Tag LSTM: a key tool for long range tag dependencies and word-tag interactions. 

     > Shared tag LSTM: By integrating both tag dependencies and word-tag interactions.
     >
     > Isolated tag LSTM: By feature integration prediction and joint taggin decision.

## Details

 Given a sentence $$x = w_1, w_2, ..., w_N$$ the goal is to find a tag sequence $$y = t_1, t_2, ..., t_N$$. Since BiLSTM-CRF model have been successful in sequence tagging, it is used as a baseline.

   1. Layers: the model consists of three layers.

      - Embedding Layer: Word embedding layer. 

        ​	One-hot vector $$w_i$$-> Embedded vector representation $$e_{w_i}$$

      - Word LSTM Layer: Extracts word context bidirectionally. The word context representation $${h_i^{word}}$$  consists of both the left-to-right $$\overrightarrow{h_{w_i}}$$ and right-to-left $$\overleftarrow{h_{w_i}}$$ order context.
  $$
        \begin{align}
        {h_i^{word}} = [\overrightarrow{h_{w_i}}, \overleftarrow{h_{w_i}}]
        \end{align}
        $$
      
      - Inference Layer: Conditional Random Field(CRF) layer is used for inferring a tag $$t_i$$ for each word $$w_i$$ based on its context representation $$h_1^{word}, ..., h_N^{word}$$.

2. Multi-Channel Model

   - First, then what is single-channel model?

     : Also referred as a word LSTM. It works for making prediction on tagging, given word context features only.

   - Multi-channel model needs more information. It utilizes both word context features and tag dependency features. 

     > Using transition score matrix for longer range tagging task can take high computation cost. To solve this problem, tag LSTM is introduced for different ranges of tag dependencies.

   

   - For each word $$w_i$$, both the word context representation $$h_i^{word}$$ and the previous predicted tags. Then the tag probability is formulated as:

$$
p(y|x) = \prod_i^Np(t_i|x, t_{<i})
$$

2. 1. Model I: Shared Tag LSTM

      - Tag dependency and word context representation flow through the same single model

   2. Isolated Tag LSTM

      - Problem of Shared tag LSTM: word context representation and tag dependency might interfere with each other. As the word LSTM does its work first and then does the tag LSTM, tag dependencies might fall into a minor factor in tagging decision.

      - Isolated tag LSTM makes the learning processes for word context representation and tag dependency independent.

      - Here come two mechanisms for isolated tag LSTM:

        > 1. Feature Integrated Prediction
        >
        >    - For each word $$w_i$$, both tag embedding and word embedding are concatenated $$[e_t, e_{w_i}]$$ and taken as an input to make a tag dependency feature $$h_i^{iso}$$.
        >
        >    - The final output, which is called *feature integrated prediction(FIP)*, is then:
        >      $$
        >      h_i = W^{iso}h_i^{iso} + W^{word}h_i^{word}
        >      $$