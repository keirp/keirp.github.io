---
layout: post
title: Chain of Thought
date: 2024-01-04 00:00:00 -0000
description: this is what included images could look like
categories: language-models
---

## LLM Pretraining

Imagine we want to predict whether a model will be able to complete a particular task. Given that language models seem to have emergent capabilities that are inherently hard to predict, this seems like a tall task. However, I will argue that this type of emergent capabilities is due to a phenomenon I will call emergent generalization.

To understand the capabilities of the model, we need to know two things: the data it was trained on and the amount of compute spent during training. The former determines the knowledge it has access to, and the latter determines the degree to which it can generalize.

<!-- This is instructive for understanding how to create better models. For instance, if you do not have a lot of compute, you need to carefully enumerate all the ways in which you want your model to be able to use its knowledge, for instance by translating examples into different languages or by changing the numbers or order of words in math problems. On the other hand, if you have a lot of compute, you can focus on including as diverse a set of data as possible and let the model figure out how to use it. -->

<!-- If you want to understand the capability level of a pretrained language model, you need to know two things: the data it was trained on and the amount of compute spent during training. The former determines the knowledge it has access to, and the latter determines the degree to which it can generalize. This is instructive for understanding how to create better models. For instance, if you do not have a lot of compute, you need to carefully enumerate all the ways in which you want your model to be able to use its knowledge, for instance by translating examples into different languages or by changing the numbers or order of words in math problems. On the other hand, if you have a lot of compute, you can focus on including as diverse a set of data as possible and let the model figure out how to use it. -->

<!-- Language models are pretrained to predict the next token on massive datasets. By throwing a lot of compute at improving its performance, the LLM learns increasingly general representations that allow it to relate any next-token prediciton problem to something that it has seen before. It is interesting to view the capabilities of LLMs through the lens of retrieval. First, note that the weights of the LLM are strictly a product of the data it was pretrained on. When you query the LLM, the only thing it can do is use the data it was trained on in some way to answer the question. As we scale our models up, they become more competent at using seemingly unrelated data to answer these questions. For instance, in a paper by Anthropic, they show that as you scale up, data from other languages becomes more influential in the model's predictions, even for English-only queries. If you want to reason about the capabilities of a model, then you should reason about the data it was trained on (the knowledge it has access to) and the amount of compute spent during training (which determines the degree to which it can generalize). -->
