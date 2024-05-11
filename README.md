# NER and ABSA for literary-historical corpora 🎓

This repository hosts the work done in the framework of the [Computational Literary Studies Project (2020-2025)](https://clsinfra.io/). The CLS project is an infrastructure research projects which aims to create materials to support the digital humanities community by pointing them to the myriad of available tools and resources to collect, analyze and publish their literary-historical datasets. 

We at the [Ghent Center for Digital Humanities](https://www.ghentcdh.ugent.be/) were responsible for building Natural Language Processing pipelines for the DH community for **Named Entity Recognition**, **sentiment analysis** and **relation extraction** purposes in English, Dutch, French and German. 

We decided to tackle this task by focusing our efforts on the development of aspect-based sentiment analysis workflows in two steps:
1.	Named entity and/or aspect extraction*.
2.	Sentiment analysis on the aspect and sentence columns.

We theorize that **aspect-based sentiment analysis** as a technique may be more valuable to literary scholars and historians than sentiment analysis on the level of the document, paragraph or sentence. In theory, this technique could thus be used to answer fine-grained research questions on the representation and interpretation of entities in a corpus!

*_We define an aspect as a unit in the sentence which can be both a named entity (a proper name) and a noun._

❗🧠 These Notebooks are not meant to reinvent the wheel. We simply want to build an infrastructure for scholars looking to perform NER or sentiment analysis on their corpus, and we do this by making step-wise code examples which can be freely used and adapted for your own purposes! 

Below we list the notebooks we created for 1) **annotation and data preparation**, 2) **aspect and/or entity extraction** and 3) **aspect-based sentiment analysis**.

## Annotation and data preparation
*	**Annotation guidelines on travelogues (example)**
This document shows you the annotation guidelines which were developed to label a corpus of travelogues in German, Dutch, French and English for aspect-based sentiment analysis. 
*	**Annotations for ABSA on travelogues (example)**
This folder includes the annotations made for aspect-based sentiment analysis on our multilingual corpus of travelogues. They can be freely reused and adapted.
*	**Bootstrapping_inception**
This notebook shows you how to bootstrap your corpus. It uses spaCy’s off-the-shelf NER tool, and shows you how to integrate the results in XMI XML. This is the input format of the annotation platform Inception, and allows you to post-correct entities instead of annotating your texts from scratch. This notebook can be adapted with other tools to bootstrap data for Inception.
*	**Annotations_to_IOB**
This language-agnostic notebook shows you how to transform your annotations to an IOB-format. It takes the sentence/chunk and the entity text column as an input, and adds a new column to your DataFrame with the IOB-annotations in a list. We do this to be able to apply span evaluation and calculate F1-scores. 

 
You can evaluate your data with an evaluation package of your choice – but we used [Nervaluate](https://pypi.org/project/nervaluate/)!

## Labelling and evaluation (NER) 🔎🌎
Our notebooks cater to scholars who want to perform aspect/named entity recognition in three scenarios: 1) you have no gold standard data available, 2) you have limited gold standard data available (only for evaluation) and 3) you have enough gold standard data available for training and evaluation. 
All notebooks show you how to start from a plain text corpus, transform it into a Pandas DataFrame and output an entity/aspect column. Each notebook details the background knowledge you need to adapt the code, details the steps and talks about the limitations and advantages of each approach. Additionally, we point you to other interesting notable sources and packages to try!
###	**Aspect_spacy**
Using our labeled travelogues data as a showcase, we show you the following functionalities of the [spaCy package](https://spacy.io/usage/training#config):
1.	Generate off-the-shelf entities for your corpus using spaCy’s models (EN, FR, NL, GER).
2.	Generate off-the shelf entities for your corpus and enrich with rules [(EntityRuler)](https://spacy.io/api/entityruler).
3.	Generate zero-shot entities for your corpus with spaCy’s [GliNER](https://github.com/urchade/GLiNER).
4.	Train and save a model on top of spaCy’s off-the-shelf models.

###	**Aspect_flair**
Using our labeled travelogues as a showcase, we show you the following functionalities of the [Flair package](https://flairnlp.github.io/):
1.	Generate off-the-shelf entities for your corpus using [Flair’s off-the-shelf models (EN, FR, NL, GER)](https://flairnlp.github.io/docs/category/tutorial-1-basic-tagging).
2.	Evaluate the results of your tagger on a small test set.
3.	Generate zero-shot entities for your corpus using Flair’s [TARSTAGGER](https://github.com/flairNLP/flair/blob/master/resources/docs/TUTORIAL_10_TRAINING_ZERO_SHOT_MODEL.md).
4.	Generate few-shot entities for your corpus by fine-tuning Flair’s TARSTAGGER.
5.	Create your own SequenceTagger on top of TARSTAGGER. 

###	**Aspect_mixtral**
This notebook shows you how to use the [LangChain](https://www.langchain.com/) framework in combination with Mistral’s Large Language Model [Mixtral-8x7b](https://huggingface.co/mistralai/Mixtral-8x7B-Instruct-v0.1) to perform aspect/named entity recognition in English, French, German and Dutch:
1.	Perform zero-shot aspect/named entity recognition, validate and parse the output as JSON.
2.	Perform few-shot aspect/named entity recognition, validate and parse the output as JSON.

## Training and evaluation (ABSA) 😀😥
###	**ABSA_HF**
These notebooks show you an approach to train an ABSA-system for your corpus in English, French, Dutch and English. A machine learning-based pipeline is developed in two steps: 
1)	The aspect extraction task is tackled by training a Flair-based sequence tagger using Huggingface models, and evaluating them on your gold-standard data using 5-fold cross-validation. 
2)	For the sentiment analysis task, our notebook shows you how to fine-tune HuggingFace’s embeddings on your gold standard aspects. These embeddings subsequently serve as input for diverse machine learning classification architectures, including SVM, AdaBoost, Random Forest, and MLP classifiers.

### **Rule-based ABSA** 
This notebook shows you an example of a rule-based ABSA-pipeline built for English in several steps: 
1)	Aspect extraction based on spaCy’s noun extraction module (aspects here are defined as nouns).
2)	Opinion word identification using spaCy’s POS-tagger to extract adjectives, adverbs and auxiliary constructions.
3)	Sentiment analysis based on the extracted opinion words using the SenticNet package. In the case of negated sentiment words, NLTK’s synset module was used to fetch the word’s antonym and generate a score.



