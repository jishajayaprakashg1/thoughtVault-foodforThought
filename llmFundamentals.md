## LLM Fundamentals
Large Language Model: It is a trained neural network whose learned parameters enable it to predict and generate sequences of tokens.

## PRETRAINING

### Step1: Download and preprocess the internet
_Example of Fineweb by huggingface:  It is the data used to teach an AI model._
- 1. _Collect raw web data_ : huge list of html pages, repositories etc.
- 2. _Filter URLs and extract text_ : remove urls that are duplicate, blocked/blacklisted, malicious sites
Extract the main readable content from raw HTML. Discard navigation menus, subscription etc.
- 3. _Language filtering_ : FineWeb uses FastText language identification.
Documents with an English-language score below 0.65 are removed from the original English dataset.
- 4. _Quality filtering_ : Remove low-quality pages, repeated lines, list-like content, and badly formatted text.
- 5. _Deduplication_ : Reduce repeated content without having to compare every document directly with every other document.
- 6. _ PII anonymization_ : to prevent exposure of some personal identifiers.
Email addresses and public IP addresses are anonymized. The pipeline also records metadata such as language, language confidence, and token count.
- 7. _Publish and train_ : The processed documents are stored in a dataset that researchers can download and use to pretrain language models.
 
### Step2: Tokenisation : convert the text into (sequence of symbold) tokens
bites converted to bytes then run byte pair encoding algorithm ( merge most common token pair to mint new token)
For example the text is converted into 100277 tokens finally. this is called the vocabulary

### Step3: Neural Network Training : 
The sequence of tokens generated in the Step 2 is divide into window of tokens
- this input sequence of tokens (anywhere between 0 to a max size say 8000 tokens) is fed into neural network an is called context, there is 100277 probabilities of next token
- each nearest token is assigned a weight, the highest weighted token is the next predicated token
Example:
91 860 245 6781
It is  a    rainy
 --> neural network (100277 probabilities) --> probability of 234 ("Day") : 5%,  probability of 234 ("season") : 2%

_Neural Network Internals_: 
input sequence of tokens is combined with the weights to form mathematical expressions which will do the next prediction.
In this process the parameters (weights) are adjusted and optimized to make the prediction consistent and correct over time.

### Step4: Inference : generate data, one token at a time
_What happens during inference?_
- Input: The model receives text, images, or other data.
- Forward pass: The input passes through the neural network.
- Probability calculation: The model calculates scores for possible outputs and, for language models, can convert them into probabilities.
- Prediction: The model selects or samples an output.
- Iteration: For text generation, the new token is added to the context, and the process repeats.





