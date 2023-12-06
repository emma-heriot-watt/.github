# Embodied MultiModal Agent (EMMA)

Hello, thanks for your interest in our work. We're the [EMMA team](https://sites.google.com/site/hwinteractionlab/home/amazon-simbot-challenge), the Heriot-Watt University team that was one of the [finalists](https://www.amazon.science/alexa-prize/simbot-challenge/one) in the [Amazon Simbot Challenge](https://www.amazon.science/alexa-prize/simbot-challenge), a university competition organised by Amazon to advance the state-of-the-art in Conversational Embodied AI. We created this Github organisation to organise all the code and artefacts that we are releasing to the public as part of our effort to create the first V+L model for Embodied AI tasks.

## News

* [4/12] :mega: We have released the [checkpoints](https://huggingface.co/emma-heriot-watt/models) on Hugging Face! :hugs:
* [1/12] :mega: We're going to be at [EMNLP 2023](https://2023.emnlp.org/) to present the paper [Multitask Multimodal Prompted Training for Interactive Embodied Task Completion](https://arxiv.org/abs/2311.04067). We'll release everything soon! Follow the organisation for updates as we release things!

## Organisation Structure

### How do all the repositories connect together?

There are multiple repos which can make it confusing up front, so here’s how all the pieces connect on a high-level. 

- [Datasets](https://github.com/emma-heriot-watt/datasets) efficiently merges all annotations from all the datasets without duplicating images. 
- [Perception](https://github.com/emma-heriot-watt/perception) extracts visual features from every single image. 
- [Policy](https://github.com/emma-heriot-watt/policy) takes each instance and the visual features, creates the pretraining and fine-tuning datasets, and trains the EMMA models. It also evaluates checkpoints on the image-based tasks.
- [Experience Hub](https://github.com/emma-heriot-watt/experience-hub) brings all the models together for inference; taking a request and an observation and predicting the next action for the environment.
- [Arena Evaluation](https://github.com/emma-heriot-watt/offline-inference) sends observations and instructions from the Alexa Arena to the experience Hub, and returns the predicted actions for execution in the environment. 


#### Some more details on how it all works. 

We have multiple image-based datasets where every example from the raw data can be turned into a single example consisting of an image and its annotations in its metadata. As we mix every dataset together for training, all the data must be in a single structure for easy training. Additionally, as each dataset contributes different tasks, many have introduced new tasks and annotations on the same images as other datasets. For example, while COCO provides image captions, VisualGenome provides scene graphs and also possible region descriptions. 

The purpose of datasets is to convert every dataset from its raw form (as it was released) into a single structure, to merge multiple datasets together and remove duplicates, to store all this information in a lightweight format that allows quick querying, and to do it as fast as possible. We easily merge all annotations from multiple datasets without duplicating images, validate the fields using Pydantic, we store these in an incredibly simple SQLite table called a “DatasetDb” or “Db”. Importantly, datasets only handles the metadata for a given image. So, everything except for the actual image, but it keeps a reference to the original image. 

The other part of providing input to the model involves extracting visual features for every single image. As mentioned in the paper, we use a feature extractor that is trained separately. To train the model efficiently, we want to extract the visual features for every single image up front. We use Perception to extract all visual features using VinVL for every single image for every single dataset. 

Policy holds the main model of EMMA. Using the Dataset Dbs and the extracted features, we train the models to perform the various tasks. Policy also contains the evaluation for each of the image-based tasks. 

The Experience Hub contains all logic for integrating the models together for inference: taking in a request from a user, processing the observation with Perception, predicting the next action with Policy, and returning the action to the environment.

The Arena Evaluation is how we send requests and observations from the Alexa Arena to the Experience Hub, and return actions to perform in the environment back to the Alexa Arena. 






## Download stuff
We provide pretrained/finetuned checkpoints, dataset features, and dbs required to reproduce our setup. All the material is available on Hugging Face! :hugs:

### Checkpoints
The checkpoints can be accessed from this link: https://huggingface.co/emma-heriot-watt/emma_models

### Dataset Features
The features for pretraining and downstream evaluation are availble here: https://huggingface.co/emma-heriot-watt/emma_features

### Dataset Dbs
The features for pretraining and downstream evaluation are availble here: https://huggingface.co/emma-heriot-watt/emma_datasets


## Results

### Dowstream Image-Based Tasks

| Model | COCO Captioning | VQAv2 | RefCOCOg | NLVR2  |
| :--- |       :---:     | :---: | :---:    | :---: |
| VL-T5 | 116.5 | 70.3 | 71.3 | **73.6**
| VL-BART | 116.6 | 71.3 | 22.4 | 70.3 
| UniTAB | 119.8 |  71.0 | **84.5** | —
| <span style="color:gray">OFA-base</span> | <span style="color:gray">138.2</span> | <span style="color:gray">78.1</span> | <span style="color:gray">82.3</span> | —
| **EMMA**  | **122.3** | **73.2** | 80.3 | 70.3


### Dialog Guided Task Completion
| Model | MSR (&#8593;) | NRA (&#8595;) | QA | 
| :--- |       :---:     | :---: | :---:
| [**LeaderBoard**](https://eval.ai/web/challenges/challenge-page/1903/leaderboard/4491) | | | |
| GauchoAI | 36.47 | — | — |
| SEAGULL | 30.98 | — | — | 
| Kingfisher | 22.37 | — | — |
| [**Baseline**](https://eval.ai/web/challenges/challenge-page/1903/leaderboard/4491) | | | |
| NS | 19.32 | 11.73 | :x:
| NS | 22.80 | 12.73 | :white_check_mark:
| VL | 18.19 | 11.82 | :x:
| VL | 34.20 | 18.82 | :white_check_mark:
| **EMMA:** | | | |
| EMMA-modular | 33.76 | 18.91 | :x:
| EMMA-modular | 33.95 | 19.05 | CR
| EMMA-modular | 35.16 | 18.92 | :white_check_mark:
| EMMA-unified | 33.26 | 18.79 | :x:
| EMMA-unified | 33.59 | 18.89 | CR
| EMMA-unified | **36.81** | **18.69** | :white_check_mark:
