# Music_Generation
Creating new Music using Recurrent Neural Network (RNN).
The code builds a Recurrent Neural Network (RNN) for music generation."character RNN" is used to predict the next character of sheet music in ABC notation to generate a brand new music file that has never been heard before!

Steps taken to build the model:

1-Data Collection: Collected the data of Irish music in “abc” format

2-Text Vectorization: Generated two lookup tables (a: maps char to numbers and b: numbers to char)

3-Preparing training data: Each input sequence that we feed into our RNN will contain seq_length characters from the text. We'll also need to define a target sequence for each input sequence, which will be used in training the RNN to predict the next character.

To do this, we'll break the text into chunks of seq_length+1. Suppose seq_length is 4 and our text is "Hello". Then, our input sequence is "Hell", and the target sequence "ello".

4-Defining RNN model: The model is based on the LSTM architecture, where we use a state vector to maintain information about the temporal relationships between consecutive characters. The final output of the LSTM is then fed into a fully connected Dense layer where we'll output a softmax over each character in the vocabulary, and then sample from this distribution to predict the next character.

5-Training the model: At this point, we can think of our next character prediction problem as a standard classification problem. We have the previous state of the RNN as well as the input at a given time step and want to predict the class of the next character, that is, actually predict the next character.

6-Generating new music: 

   a-Initialize a "seed" start string and the RNN state, and set the number of characters we want to generate.
  
   b-Use the start string and the RNN state to obtain the probability distribution of the next predicted character.
  
   c-Sample from multinomial distribution to calculate the index of the predicted character. This predicted character is then used as the next input to the model.
  
   d-At each time step, the updated RNN state returned is fed back into the model, so that it now has more context. After predicting the next character, the updated RNN states are again fed back into the model, which is how it learns sequence dependencies in the data, as it gets more information from the previous predictions.

