## LLM Fundamentals
Large Language Model: It is a trained neural network whose learned parameters enable it to predict and generate sequences of tokens.

## Stage1:  PRE-TRAINING --> output is BASE MODEL (internet document simulator)

### Step1: Download and preprocess the internet
_Example of Fineweb by huggingface:  It is the data used to teach an AI model._
- 1. _Collect raw web data_ : huge list of html pages, repositories etc.
- 2. _Filter URLs and extract text_ : remove urls that are duplicate, blocked/blacklisted, malicious sites
Extract the main readable content from raw HTML. Discard navigation menus, subscription etc.
- 3. _Language filtering_ : FineWeb uses FastText language identification.
Documents with an English-language score below 0.65 are removed from the original English dataset.
- 4. _Quality filtering_ : Remove low-quality pages, repeated lines, list-like content, and badly formatted text.
- 5. _Deduplication_ : Reduce repeated content without having to compare every document directly with every other document.
- 6. _PII anonymization_ : (Personally Identifiable Information) to prevent exposure of some personal identifiers.
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

```
Imagine an AI model as a student.
Tokens are the words the student reads in a question and writes in an answer.
Parameters are the knowledge and learned patterns the student uses to formulate the answer.
```

### Step4: Inference : generate data, one token at a time
_What happens during inference?_
- Input: The model receives text, images, or other data.
- Forward pass: The input passes through the neural network.
- Probability calculation: The model calculates scores for possible outputs and, for language models, can convert them into probabilities.
- Prediction: The model selects or samples an output.
- Iteration: For text generation, the new token is added to the context, and the process repeats.

### Compute Engine
- GPU (Graphics Processing Unit) : is a specialized electronic circuit designed to rapidly  perform parallel mathematical calculations
for rendering images, video and running heavy workloads like AI and ML
- GPU is the perfect fit for training models
- Rent a computer on the cloud ( services are provided by platforms like Lambda)
- Multiple GPUs are stacked into single node, multiple nodes are stacked in Data center

```
A base model is an AI model that has been trained on a large amount of data to learn patterns in language,
code, or other information, but has not yet been specifically fine-tuned to follow instructions or behave
like a conversational assistant.

In simple terms, a base model is the starting point from which specialized AI models can be created.
```
_The output of the pre-training is a BASE model_

## Stage2: POST-TRAINING --> output is AI Assistant with which human can have conversation --> SFT model : an assistant trained by Supervised finetuning
For this the base model has to be trained on data sets of conversations
```
Human: what is 2+3
Assistant: 5
Human: what if it is * instead of +
Assistant: 6
```

- This conversation is converted into tokens
- It was a tedious process of training, where human linguists were asked to come up with different questions (prompts) and then answer them.

- Vague recollection : knowledge in parameters it was trained on
- Working memory : knowledge in the tokens of the context window
- knowledge of self : it can tell who it is based on the data fed about that
- Models can hallucinate : who is abcd? Model can give a wrong answer confidently: How to mitigate
  + Mitigation1: feed new training example: In which reply is I don't know!
  + Mitigation2: allow the model to search the internet
- Models need token to think
- Models cannot count 
- Models are not good with spelling : they see tokens not characters
- Fix by saying use code in the prompt

Here the output is a SFT model and assistant trained by Supervised finetuning

## Stage3:  POST-TRAINING REINFORCEMENT Learning --> output is a RL model
```
analogy: consider a text book, it gives the background information (pretraining),
then an example problem with a solution (finetuning) and finally a practise problem with answer but no solution (reinforcement learning)
```
Example:
```
So now we have a quetsion and it's answer, we need to come up with solution to derive at that answer.
Say we got 15 solutions, only 4 were right. Take the top solution that is right and short.
Train the model on it.
Repeat
```

To summarise an SFT model will mimick an expert's answer but a RL model will think and come up woth different solutions and present the
shortest and right solution.

## Stage4: REINFORCEMENT Learning from Human Feedback --> output is a RLHF model
- Human must give orders / score for the output.
- Train another model call it reward model which will act as a human scorer for the solutions generated during thinking process by LLM.
- Reward model will give a score between 0 and 1 --> 0 being the worst score.
- Reward model is trained such that it's scores must become consistent with the  Human ordering at the end

## SUMMARY
```
User enters a query in chatGPT.
This query is chopped into tokens (can be viewed in toktokenizer)  as it goes through the conversational Protocol/format .
Hence, a one-dimensional sequence of tokens is generated and it continues to generate tokens in response.

How was it able to do it?
Knowledge acquisition through internet,
finetuned
Open AI has hired Data labellers, often called AI trainers or data annotators
there will be thousands of prompts each of which has to be answered by the human data labeller,
who follows the labelling instructions at open AI.

Hence, the response of the prompt is actually a neural network simulation of the data labeller's response.
```
























