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

 Given a sentence $x = $ $w$~1~,  $w$~2~, $...$, $w$*~N~*, the goal is to find a tag sequence $y = $ $t$~1~, $t$~2~, $...$, $t$*~N~*. Since BiLSTM-CRF model have been successful in sequence tagging, it is used as a baseline.

   1. Layers: the model consists of three layers.

      - Embedding Layer: Word embedding layer. 

        ​	One-hot vector -> embedded vector representation

      - Word LSTM Layer

      - Inference Layer







