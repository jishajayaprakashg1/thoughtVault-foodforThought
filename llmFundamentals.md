## LLM Fundamentals
Large Language Model: AI model trained on huge datasets work son neural networks

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

### Step3: Nueral Network Training : 
