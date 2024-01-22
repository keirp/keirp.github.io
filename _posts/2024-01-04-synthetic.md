---
layout: post
title: Synthetic Data
date: 2024-01-04 00:00:00 -0000
description: this is what included images could look like
categories: language-models
---

## LLM Pretraining

The modern LLM training pipeline was popularized by the InstructGPT paper and consists of the following stages:

1. **Pretraining:** Pretrain the model on a large corpus of trillions of tokens of text.
2. **Supervised Fine-tuning:** Fine-tune the model on a smaller amount of examples of the task of interest.
3. **RLHF:** Train your model with an RL algorithm to directly maximize your objective (here, human preference).

Step 2 and 3 are often referred to as "post-training" and there is occasionally a step 1.5 called mid-training where the model is further pre-trained on a medium amount of higher-quality data.

The vasy majority of compute is spent on pretraining. This is because supervised fine-tuning is very data-limited - getting humans to create high quality examples is often very expensive. The same is true for RLHF, where preference labels are also expensive. In this stage is is common to create a preference model to amortize the cost of human labels, however, it is easy to overoptimize the preference model which is often only accurate near the training distribution.

You may notice that we spend more compute on stages that are not actually optimizing our objective directly. However, pretraining is still doing something useful: it is buying us sample efficiency in the later stages. This has been measured empirically in a paper by OpenAI. However, a recent Anthropic paper gives more insight on what this really means. The paper was primarily studying the impact that different pretraining data has on downstream model behavior. The researchers found that as you increase the amount of compute spend on pretraining, models are able to utilize their datasets more efficiently for answering downstream questions. For instance, while a small model may primarily utilize data with similar surface-level phrases to predict the next word, a large model can refer to data that is relevant in a semantic sense, even using data written in different languages!

The ability of pretraining to learn relationships between data in an unsupervised manner through compression is worth spending compute on. As language models learn to model their pretraining data better, they learn a ladder of increasingly complicated relationships between data. The above figure illustrates a conjecture of what this ladder might look like: the model starts by learning simple relationships like synonyms, moves on to relationships between similar concepts in different languages, and eventually even learns to model latent attributes about the writer of the text such as mathematical competence. The learned relationships later on in the ladder are increasingly infeasible for humans to label manually. For instance, how would one go about labeling all the math answers on the internet as correct or incorrect? Yet, it seems that the largest models such as GPT-4 are able to do a reasonable job at learning representations for correctness. As we scale past GPT-4, what other relationships will the model be able to learn?

The result of the ever-increasing data efficiency of language models is that anecdotally, GPT-4 took far fewer human data to align than GPT-3.5 did. In order to get smaller LLMs to generalize the same way that a larger one does for free, it has to essentially be spelled-out in fine-tuning. Concretely, where a larger model instruction-tuned in English may exhibit significant transfer to other languages, small ones need examples in each language to get the same behavior.

The Achilles heel of the modern pretraining pipeline is that is is data hungry. If we don't keep feeding the LLM increasing amounts of data, we will start seeing deminishing returns. GPT-3 was trained on 300B tokens, Llama 2 was trained on 2T tokens, and GPT-4 was likely trained on around 10T tokens. It is likely that we don't have too much more than 100T tokens without significantly sacrificing data quality. In order to avoid hitting this wall, some have their hopes set on synthetic data. However, before we can discuss synthetic data, we need to understand where our current data comes from.

## Where Does the Data Come From?

While the sources of pretraining data are a heavily guarded secret at the major labs, there have been several open-source pretraining corpuses that are likely similar. In the popular RedPajama dataset, the data is sourced from CommonCrawl, C4, GitHub, Books, ArXiv, Wikipedia, and StackExchange.

It is interesting to note that while the data is mostly human-generated, there are almost always some processes in place to ensure that the data is high quality before being published.

- **GitHub:** Code on GitHub is typically written by humans. Code tends to have been at least tested before being committed, and the best code is often reviewed by other humans and even contains tests.
- **Books:** Books are written by humans in an iterative process. Typically this involves several iterations by the author themselves, and later by editors at the publishing company. It is also worth mentioning the market forces that incentivize authors to write high-quality books.
- **ArXiv:** ArXiv papers are written by humans and mostly correspond to papers that underwent at least some type of peer review. Papers usually summarize months or years of work, either entirely theoretical or with some real-world experimentation.
- **Wikipedia:** Wikipedia articles are written by humans and undergo rigorous reviews by other humans. The articles are also often edited by many people over time.
- **StackExchange:** StackExchange posts and answers are written by humans and answers that were useful to the community are upvoted. Often answers are checked by putting them into practice and seeing if they work, such as the the case of coding questions.

The pattern in all the above data sources is that while they are human-generated, there is always some sort of verification or grounding. They aren't just a copy of data that already existed, but the combination of several data sources, including human judgements, grounding in real events or in the output of running code, and market forces. Even if there is no explicit verification, the writing that eventually makes it online is not usually a first draft but the last step in a long chain of thought.

<!-- ## Stage 1 versus Stage 2 Data

It is interesting to define a distinction between two types of data: that which exists and that which can be derived from existing data. Let's call the former stage 1 and the latter stage 2. Stage 2 data includes our inferences after ingesting stage 1 data. For instance, if we read a book, we can summarize it, we can write a review, we can compare it to other books, and we can implement an algorithm from the book and see the results. In some sense, human progress can be viewed as a continuous processing of available data and adding it back into the pool of available data. In that sense, what counts as stage 1 and stage 2 data is constantly changing. To a language model, the above data sources are all existing data in stage 1, but they were certainly created by humans processing other data. -->

## The Constant Processing of Data

<!-- Stage 1 data includes everything in the above list of data used in pretraining. Stage 2 data is what is outputted by a language model trained on that data, since the model consistutes a form of processing. However, there can be more ways in which data can be processed. For instance, we can review a book we read, we can compare and contrast subjects from multiple documents, and we can implement an algorithm from a paper and write about the results. While LLM pretraining is an incredibly powerful form of processing, there are many known limitations such as imperfect factual recall, the reversal curse, and a lack of grounding in the real world.  -->
