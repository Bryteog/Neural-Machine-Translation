#### Overview

Made a Sequential language translation model to translate english sentences to other languages using Torch and TorchText. [data]().
Pre-trained tokens for various languages from the SpaCy library is used for tokenization, etc. The data is loaded using the Pandas library.


#### Model 

A custom `Dataset_Loader` class handles the data by retrieving the data in pairs. A function for the tokens of a specified language is obtained to build the vocabulary. Special tokens for unkown, start and end of sequences are also defined and added to the vocabulary. The vocabulary is created by mapping a unique token to a unique integer.

Further functions are created to:
- Execute transformation on text sequentially.
- Pad token IDs with start and end tokens and convert the sequence to Torch tensors.
- Tokenize input sentences pads to maximum length and return context (English) and target (Eg.Spanish) batches.

Masks are then generated for the context and target sentences to ensure tokens in the input do not attend to future tokens and the model focuses on relevant info only. All this is done so the model adheres to the sequential nature of the task.

A `PositionalEncoding` class ensures information about relative and absolute position of tokens in the sequence is provided, using sinusoidal functions. Tokens are then converted into vectors using embeddings.

The main model is a Sequence to Sequence Transformer. It uses an `Encoder` to process the input sequence (English sentences), the output serves as the input for the `Decocder` which generates the output sequence (Eg. Spanish translation).
The CrossEntropyLoss and Adam serves as the loss and optimizers respectively, a learning rate of 0.0001 is used.

The training and evaluation functions are then defined and the model is trained.
To perform inference, a function employing the greedy algorithm is used. This algorithm picks the word with the highest probability at each step to be the next word in the sequence.
The translation is then done by converting input sentence into corresponding token representation. The greedy function is used to generate the token format for the translated sentence, which is inturn converted into reabale format, stripped of all special tokens (start and end tokens).

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


- #### English - French model

After training for 20 epochs the training and validation losses are 1.773 and 1.724. (Longer training will definitely improve the model performance)

Some sample english phrases, their actual translation in french and the predicted translation.

Context: It's bright outside today !

Actual: Il est brillant a l'exterieur aujourd'hui !

Predicted:  C' est désormais aujourd'hui ! 

Context: Don't forget to dehydrate.
Actual: N'oubliez pas de deshydrater
Predicted:  N' oublie pas de oublier . 
 
Context: I'll see you again tomorrow.
Actual: Je te reverrai demain
Predicted:  Je te verrai demain . 
 
Context: What time is it?
Actual: Quelle heure est-il?
Predicted:  À quelle heure est -il ? 
 
Context: This translation model is not bad.
Actual: Ce modele de traduction n'est pas mauvais
Predicted:  Ce n' est pas mauvais .

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


- #### English - German model

After training for 30 epochs the training and validation losses are  and . 

Some sample english phrases, their actual translation in german and the predicted translation.
