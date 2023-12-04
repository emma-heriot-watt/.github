## Embodied MultiModal Agent (EMMA)

Hello, thanks for your interest in our work. We're the [EMMA team](https://sites.google.com/site/hwinteractionlab/home/amazon-simbot-challenge), the Heriot-Watt University team that was one of the [finalists](https://www.amazon.science/alexa-prize/simbot-challenge/one) in the [Amazon Simbot Challenge](https://www.amazon.science/alexa-prize/simbot-challenge), a university competition organised by Amazon to advance the state-of-the-art in Conversational Embodied AI. We created this Github organisation to organise all the code and artefacts that we are releasing to the public as part of our effort to create the first V+L model for Embodied AI tasks.

## News
* [4/12] :mega: We have released the [checkpoints](https://huggingface.co/emma-heriot-watt/models) on Huggin Face! :hugs:
* [1/12] :mega: We're going to be at [EMNLP 2023](https://2023.emnlp.org/) to present the paper [Multitask Multimodal Prompted Training for Interactive Embodied Task Completion](https://arxiv.org/abs/2311.04067). We'll release everything soon! Follow the organisation for updates as we release things!


### Org Structure

#### [Policy](https://github.com/emma-heriot-watt/policy)
Policy is the main repo that is used to pretrain and fine tune EMMA as well as to evaluate a checkpoint on all image-based tasks.

#### [Datasets](https://github.com/emma-heriot-watt/datasets)
Datasets is where we have implemented all the components required to create a db for pretraining, as well as all downstream tasks. These dbs are required by the policy along with the features for each task.

#### [Perception](https://github.com/emma-heriot-watt/perception)
Perception is responsible for extracting the features for images used by policy. The repo can be used as a standalone to extract features before running things on policy, or used as an api to perform offline evaluation.

#### [Experience-hub](https://github.com/emma-heriot-watt/experience-hub)
Experience-hub is the repo associated with setting up all the pipelines and controllers required for the offline inference. Experience hub communicates with perception to extract features only when necessary, and queries policy to perform actions on the environment.

#### [Offline-inference](https://github.com/emma-heriot-watt/offline-inference)
The offline inference contains the instrastructure to run the evaluation on the Alexa Arena and report metrics using Weights and Biases


### Download stuff
We provide pretrained / finetuned checkpoints, dataset features, and dbs required to reproduce our setup. All the material is available on Huggin Face! :hugs:

#### Checkpoints
The checkpoints can be accessed from this link: https://huggingface.co/emma-heriot-watt/emma_models

#### Dataset Features
The features for pretraining and downstream evaluation are availble here: https://huggingface.co/emma-heriot-watt/emma_features

#### Dataset Dbs
The features for pretraining and downstream evaluation are availble here: https://huggingface.co/emma-heriot-watt/emma_datasets


### Results

#### Dowstream Image-Based Tasks

| Model | COCO Captioning | VQAv2 | RefCOCOg | NLVR2  |
| :--- |       :---:     | :---: | :---:    | :---: |
| VL-T5 | 116.5 | 70.3 | 71.3 | **73.6**
| VL-BART | 116.6 | 71.3 | 22.4 | 70.3 
| UniTAB | 119.8 |  71.0 | **84.5** | —
| <span style="color:gray">OFA-base</span> | <span style="color:gray">138.2</span> | <span style="color:gray">78.1</span> | <span style="color:gray">82.3</span> | —
| **EMMA**  | **122.3** | **73.2** | 80.3 | 70.3


#### Dialog Guided Task Completion
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
