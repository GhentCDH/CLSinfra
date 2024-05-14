# NER and ABSA for literary-historical corpora 🎓

This repository hosts the work done in the framework of the [Computational Literary Studies Project (2020-2025)](https://clsinfra.io/). The CLS project is an infrastructure research projects which aims to create materials to support the digital humanities community by pointing them to the myriad of available tools and resources to collect, analyze and publish their literary-historical datasets. 

We at the [Ghent Center for Digital Humanities](https://www.ghentcdh.ugent.be/) were responsible for building Natural Language Processing pipelines for the DH community for **Named Entity Recognition**, **sentiment analysis** and **relation extraction** purposes in English, Dutch, French and German. 

We decided to tackle this task by focusing our efforts on the development of aspect-based sentiment analysis workflows in two steps:
1.	Named entity and/or aspect extraction*.
2.	Sentiment analysis on the aspect and sentence columns.

We theorize that **aspect-based sentiment analysis** as a technique may be more valuable to literary scholars and historians than sentiment analysis on the level of the document, paragraph or sentence. In theory, this technique could thus be used to answer fine-grained research questions on the representation and interpretation of entities in a corpus!

*_We define an aspect as a unit in the sentence which can be both a named entity (a proper name) and a noun._

❗🧠 These Notebooks are not meant to reinvent the wheel. We simply want to build an infrastructure for scholars looking to perform NER or sentiment analysis on their corpus, and we do this by making step-wise code examples which can be freely used and adapted for your own purposes! 

🚀 Below we list the resources and Jupyter Notebooks we created for 1) **annotation and data preparation**, 2) **aspect and/or entity extraction** and 3) **aspect-based sentiment analysis**.

## Annotation and data preparation
###	**annotation_guide_2024.pdf (example)**
This document shows you the annotation guidelines which were developed to label a corpus of travelogues in German, Dutch, French and English for aspect-based sentiment analysis. It also includes a small guide on the open-source annotation platform [INCEPTION](https://inception-project.github.io/), which we at GhentCDH used for our projects.
###	**Annotations for ABSA on travelogues (example)**
We include links to our Drive folder which hosts the annotations we made for **aspect-based sentiment analysis on our multilingual corpus of travelogues**. They can be freely reused and adapted, and are the use-case for the development of our workflows. For each notebook, we'll load a sample of our (annotated) data directly from our GitHub repository to showcase each workflow. 
###	**Bootstrapping_inception**
This notebook shows you how to bootstrap your corpus. It uses spaCy’s off-the-shelf NER tool, and shows you how to integrate the results in XMI XML. This is the input format of the annotation platform Inception, and allows you to post-correct entities instead of annotating your texts from scratch. This notebook can be adapted with other tools to bootstrap data for Inception.
###	**Annotations_to_IOB**
This language-agnostic notebook shows you how to transform your annotations to an IOB-format. It takes the sentence/chunk and the entity text column as an input, and adds a new column to your DataFrame with the IOB-annotations in a list. We do this to be able to apply span evaluation and calculate F1-scores.

![dataframe_to_bio](https://github.com/GhentCDH/CLSinfra/blob/main/Dataframe_to_bio.png)
 
You can evaluate your data with an evaluation package of your choice – but we used [Nervaluate](https://pypi.org/project/nervaluate/)!

## Labelling and evaluation (NER) 🔎🌎
Our notebooks cater to scholars who want to perform aspect/named entity recognition in three scenarios: 1) you have no gold standard data available, 2) you have limited gold standard data available (only for evaluation) and 3) you have enough gold standard data available for training and evaluation. 
All notebooks show you how to start from a plain text corpus, transform it into a Pandas DataFrame and output an entity/aspect column. Each notebook details the background knowledge you need to adapt the code, details the steps and talks about the limitations and advantages of each approach. Additionally, we point you to other interesting notable sources and packages to try!

![overview_notebooks](https://github.com/GhentCDH/CLSinfra/blob/main/notebooks_overview.png)
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

# Travelogues example data 🧭🗺

This README details the **Metadata**, **Data**, **Annotations and annotation guide** used as an example use-case to run the notebooks! 

## Metadata 

The metadata for the entire corpus is split per collection, and can be downloaded via our [Drive folder](https://drive.google.com/drive/folders/17hqPMR-gi2fg1TbuBzBLrt-xcu-_1MO7?usp=sharing).

* **Biodiversity Heritage Library** | BHL_merged.csv
* **Travelogues Project** | TP_merged.csv
* **Italian Travelogues** | IT_merged.csv
* **Gutenberg Project** | GB_merged.csv
* **DBNL** | DBNL_merged.csv

Each .CSV-file contains the following columns:

* ID (new ID for processing the data)
* language (language the text is written in)
* title (title of the book)
* author (author of the book)
* date_published (year the book was published)
* Original_ID (original ID from the source. These are also the names of the text files in the gathered corpus.)
* no_of_character (number of characters)
* no_of_tokens (number of tokens as processed by SpaCy)
* OCR_quality (quality of the OCR according to the [Garbageness Score](https://ryanfb.xyz/etc/2015/03/16/automatic_evaluation_of_ocr_quality.html).


## Data (travelogues corpus)

Texts gathered are named according to the Original_ID column.

### **Biodiversity Heritage Library** 

The [BHL corpus](https://drive.google.com/drive/folders/1cig-uR5W7YILuDiVZLTOUnS1mkG-utQE?usp=drive_link) is published on our Drive due to its size. 
The dataset is split according to the key words used to scrape the texts (explor, journe, excurs, travel, expeditie, reis, trip). 
The texts contain a multitude of languages (Dutch, English, French, German, Portuguese, Latin, ...). 
The code used to scrape this data from the API is published in our **Notebooks** folder.

### **Gutenberg Project Travelogues**

The [Gutenberg corpus](https://drive.google.com/drive/folders/1HrFVVYageLbpl3tcDcajousWPVj-JnPx?usp=drive_link) is published on our Drive.
The texts are in both English and French.

### **DBNL dataset**

The [DBNL](https://drive.google.com/drive/folders/1-1uY54VHEr1XEGDglm-42K_NLeA3ip3j?usp=drive_link) is published on our Drive.
It contains all texts requested from the [DBNL website](https://www.dbnl.org/) that are related to travel. 
The texts are all in Dutch.

### **Italian Travels dataset**

The Italian Travels dataset can be gathered from the [project "Today we Have Passed with the Ancients...": Visions of Italy between XIX and XX century ](https://sites.google.com/view/travelwritingsonitaly/home?authuser=0).
Files are available in .TEI and .TXT.

### **German Travelogues Project dataset**

The German Travelogues Project dataset can be gathered from their [GitHub repository](https://github.com/travelogues/travelogues-corpus). More information on the corpus can be found on [their website](https://www.travelogues-project.info/).


## Annotations

We created an annotated dataset comprising texts in English, Dutch, German and French which were annotated for biodiversity-related aspects and their associated sentiment. 
The [annotated dataset](https://drive.google.com/file/d/1ebv8IeBg4fmuEcVnKrp3GqhCy2-wLp3F/view?usp=sharing) is published on our Drive.
The aspects annotated are further detailed in the **annotation_guide.PDF**. Sentiment-bearing words are annotated on a 1 (very negative) to 5 (very positive)-point scale. Sentiment was also annotated on the level of the sentence.
The .ZIP-file **_Annotations.zip_** contains the annotated files in UIMA CAS XMI (XML 1.1), and can easily be parsed using the [Inceptalytics API](https://github.com/catalpa-cl/inceptalytics).

The following aspects were considered: 

* PERSON
* LOCATION
* ORGANISATION
* FAUNA
* FLORA
* BIOME
* HUMAN_LANDFORM
* NATURAL_LANDFORM
* NATURAL_PHENOMENON
* WEATHER
* MYTH


## Other interesting sources to check! 🦾❗

Looking for other ways to apply NER and/or aspect recognition on your corpus? Make sure to check out these incredibly interesting sources for Digital Humanists to experiment with!
* [LitBank](https://github.com/dbamman/litbank)
* [Python Programming for DH (YouTube)](https://www.youtube.com/@python-programming)
* [Gollie](https://hitz-zentroa.github.io/GoLLIE/): open-source Large Language Model trained to follow annotation guidelines.


