---
title: "Deep Dive into LLMs like ChatGPT"
summary: "A detailed walkthrough on how LLMs work under the hood, starting from the basics."
year: 2025
link: "https://www.youtube.com/watch?v=7xTGNNLPyMI&list=PLWrKtdds2HC8oPCNKYxo407EY8cASruhs"
subjects: ["ai", "llms"]
tags: ["llms", "chatgpt", "transformers", "embeddings", "interpretability"]
---

## Why I saved this

## Key points
- Pretraining data
    - Data sets on which LLMs are trained are essentially text that has been scraped from millions websites
  - The HTML is cleaned up to only retain the main content text
  - The data is deduplicated
  - Sensitive data is removed
  - Different datasets are used to train LLMs for different purposes
  - E.g. of a dataset: https://huggingface.co/datasets/HuggingFaceFW/fineweb
- Tokenisation
  -  The training data, which is a long text string, is provided as a one dimensional sequence of binary bits
  -  The length of the sequence is a precious resource when it comes to training these models. So we want to reduce it
     -  We can use 256 bytes to represent sequences of bits
     -  We attach other symbols to represent bytes that frequently occur together
     -  We go on increasing symbol size to decrease length of the sequence they represent
     -  These symbols are called tokens. GPT-4 has about 100,277 tokens
     -  Try out tokenization here: https://tiktokenizer.chatgptcn.com/
  - Neural Network Training
    - We take a sequence of tokens
    - We then try to predict the next token in the sequence
    - Each of the tokens in the token set is given a probability by the neural network
      - These probabilities are random at first
      - These probabilities are assigned by weights in the neural network's function called 'parameters', which usually run into the billions
    - We update the neural network by using the actual token that appears next in the training data set 
    - This is done repeatedly in parallel, and in large batches, until the probabilities in the neural network are set such that it becomes good at predicting the next character reliably
  - Neural Network Internals
    - E.g. here: https://bbycroft.net/llm
    - This is a representation of a transformer
    - Whatever is shown are neurons that fire 
  - Inference
    - Inference: process of generating new data from the model
    - It is the process of generating new token streams from the model
  - GPT-2: Training & Inference

Bookmark: https://youtu.be/7xTGNNLPyMI?si=nj5DYt8gRkNJi_de&t=2099


