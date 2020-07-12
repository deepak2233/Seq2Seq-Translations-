# Seq2Seq-Translation-
Seq2Seq Machine Translation of Languages is done by using Pytorch
<p align="center">
  <img width="300" height="210" src="https://cdn.analyticsvidhya.com/wp-content/uploads/2018/02/pytorch-logo-flat-300x210.png">
</p>

each word in a language is represented as a one-hot vector, or giant vector of zeros except for a single one (at the index of the word). 

### The Seq2Seq Model
A Recurrent Neural Network, or RNN, is a network that operates on a sequence and uses its own output as input for subsequent steps.

A Sequence to Sequence network, or seq2seq network, or Encoder Decoder network, is a model consisting of two RNNs called the encoder and decoder. The encoder reads an input sequence and outputs a single vector, and the decoder reads that vector to produce an output sequence.
Unlike sequence prediction with a single RNN, where every input corresponds to an output, the seq2seq model frees us from sequence length and order, which makes it ideal for translation between two languages.
With a seq2seq model the encoder creates a single vector which, in the ideal case, encodes the “meaning” of the input sequence into a single vector — a single point in some N dimensional space of sentences.

### The Encoder
The encoder of a seq2seq network is a RNN that outputs some value for every word from the input sentence. For every input word the encoder outputs a vector and a hidden state, and uses the hidden state for the next input word.
<p align="center">
  <img width="214" height="207" src="https://pytorch.org/tutorials/_images/encoder-network.png">
</p>
 
 ### The Decoder
 The decoder is another RNN that takes the encoder output vector(s) and outputs a sequence of words to create the translation.
 In the simplest seq2seq decoder we use only last output of the encoder. This last output is sometimes called the context vector as it encodes context from the entire sequence. This context vector is used as the initial hidden state of the decoder.

At every step of decoding, the decoder is given an input token and hidden state. The initial input token is the start-of-string <SOS> token, and the first hidden state is the context vector (the encoder’s last hidden state).
  <p align="center">
  <img width="214" height="291" src="https://pytorch.org/tutorials/_images/decoder-network.png">
</p>
  
 ##### The Attention Decoder
 If only the context vector is passed betweeen the encoder and decoder, that single vector carries the burden of encoding the entire sentence.

Attention allows the decoder network to “focus” on a different part of the encoder’s outputs for every step of the decoder’s own outputs. First we calculate a set of attention weights. These will be multiplied by the encoder output vectors to create a weighted combination. The result (called attn_applied in the code) should contain information about that specific part of the input sequence, and thus help the decoder choose the right output words.
<p align="center">
  <img width="332" height="316" src="https://i.imgur.com/1152PYf.png">
</p>

Calculating the attention weights is done with another feed-forward layer attn, using the decoder’s input and hidden state as inputs. Because there are sentences of all sizes in the training data, to actually create and train this layer we have to choose a maximum sentence length (input length, for encoder outputs) that it can apply to. Sentences of the maximum length will use all the attention weights, while shorter sentences will only use the first few.
<p align="center">
  <img width="395" height="629" src="https://pytorch.org/tutorials/_images/attention-decoder-network.png">
  
  
  
you can use https://pytorch.org/tutorials/intermediate/seq2seq_translation_tutorial.html to learn more about Seq2Seq Translation
</p>
