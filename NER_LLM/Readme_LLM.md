# Named Entity Recognition with Large Language Models

In this repo folder, you will find the code used to evaluate the following generative instruct LLMs in the GPT4All suite:

1. mistral-7b-instruct-v0.1
2. nous-hermes-llama2-13b (uncensored)
3. Meta-Llama-3-8B-Instruct

These models were evaluated to extract fauna 🐱 and flora 🍀 entities from a test corpus of travel literature (18th - 20th century).
For more information on the data, refer to the main page of this GitHub. 

We experimented with different prompts which become incrementally more complex. As shown in the image below, we start out with a base prompt, then add a persona, annotation guide, context (metadata), and lastly: a couple of few-shot examples to steer the model in the right direction.

![llm_prompts](https://github.com/GhentCDH/CLSinfra/blob/main/NER_LLM/prompts.png)

All of these models were evaluated for each language in the corpus (English, Dutch, French and German).
We used Nervaluate for the evaluation process.
The code for the evaluation process can be found in the notebook **Evaluate_LLM_output.ipynb**. 
The code for the prompting process can be found in the notebook **PROMPT_V.ipynb**.

If you want to recreate our experiments, or are interested in the results we got:
* ![This is a link to our Drive Folder with the evaluation sets (dev) we used, and the outputs for each language, prompt and model: **Results_LLM**](https://drive.google.com/drive/folders/1JxqSYDTTHoeOGEXJnJQ4SH4adFzOhmPc?usp=sharing)
* ![This is a link to the presentations and posters made based on the results of our experiments: **Data_LLM.zip**.](https://drive.google.com/drive/folders/1JxqSYDTTHoeOGEXJnJQ4SH4adFzOhmPc?usp=sharing)


![bla](https://drive.google.com/drive/folders/1JxqSYDTTHoeOGEXJnJQ4SH4adFzOhmPc?usp=sharing)



