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
The checkpoints can be accessed from this link: https://huggingface.co/gpantaz/emma_models

#### Dataset Features
The features for pretraining and downstream evaluation are availble here: https://huggingface.co/gpantaz/emma_features

#### Dataset Dbs
The features for pretraining and downstream evaluation are availble here: https://huggingface.co/gpantaz/emma_datasets


### Results

#### Dowstream Image-Based Tasks

| Model | COCO Captioning | VQAv2 | RefCOCOg | NLVR2  |
| :---: |       :---:     | :---: | :---:    | :---: |
| EMMA  | B|


#### Dialog Guided Task Completion