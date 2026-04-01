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
  - Reliable sources of information like Wikipedia are weighted higher. They are fed to the training multiple times to reinforce the model's memory. 
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
 - Loss: measure of how well your model is at token prediction. Training aims to bring this loss value lower. 
 - Base model: Only handle prediction of the next token. No capability of Q&A. 
 - A base model is comprised of
   - The mathematical functions that are responsible for inference (usually a short python code)
   - The parameters that are fed into this function (usually upwards of a billion)
- Llama 3.1 base model inference
	 - Hyperbolic: A nice sandbox to try out token generation from base models
	 - The pre-training stage is around 3 months
- Post training data (conversations)
	 - The base model is then fed a new training data set that is comprised of conversations that are typically between a human and an LLM
 	 - The post-training stage usually only lasts a couple of hours
	 - There are protocols used to convert conversations into tokens. Analogous to TCP/IP 
   	 - Each LLM has a different protocol
	 - This protocol has specific tokens for start and end of conversations
	 -  Initially, a highly manual process was used to generate the conversations that were fed to LLMs for training them
   		-  Today, a lot of this is automated with existing LLMs
   	 -  Experts in the field are hired to do the labelling and construction of datasets
   	 -  A good mental model to use when talking with an LLM -> A simulation of a conversation with a human labeller
  -  This process employs Reinforcement Learning with Human Feedback (RLHF)
- Hallucinations
	- When you ask a model about a person that doesn't exist, it will generate a response in the confident tone and the style of answers to questions about real people present in the training set, in a manner that is statistically consistent
	- To avoid hallucinations, they
  	- Take a sample from the training data
  	- Generate a factual question from it
  	- Sample responses from the model
  	- Score the correctness of the response by using the original context and the model as the judge
  	- Score the informativeness of the response by using the original context and the model as the judge
    	- Informativeness is a measure of how cogently and confidently the model is able to answer the question
  	- For responses that are informative and incorrect, they
    	- Either generate a refusal to answer th question
    	- Or add a web search tool to look up the question on the web  
 - The context window is analogous to working memory. The training data is analogous to long term memory. 
- Knowledge of self
  - For questions like "Who are you?", "What is your name?" etc. the model is provided with a set of hard-coded responses. It is then fine-tuned to give these responses when it is asked these sort of questions. 
- Thinking and reasoning
  - When training a model to reason, it is better to train it with dataset that breaks the reasoning down in small steps that go from left to right, as the answer is generated. This is because each token that is generated only has a finite amount of computation power, and it is better to spread this out across many tokens rather than cram them into a few tokens
    - E.g. Consider this - Human: "Emily buys 3 apples and 2 oranges. Each orange costs $2. The total cost of all the fruit is $13. What is the cost of apples?"
    - To answer this question, it is better to use this answer - Assistant: "The total cost of the oranges is $4. 13 - 4 = 9, the cost of the 3 apples is $9. 9/3 = 3, so each apple costs $3. The answer is $3. 
    - An answer like this is counterproductive - Assistant: "The answer is $3. This is because 2 oranges at $2 are $4 total. So the 3 apples cost $9, and therefore each apple is 9/3 = $3". This is because the model is forced to cram the entire computation of this answer into its 4th token, where it produces the final answer
  - For math problems, it is better to ask the model to "use code" to answer the question
- Jagged intelligence
  - Models are still not good at certain simple tasks that take little intelligence
- Supervised finetuning to reinforcement learning
   

