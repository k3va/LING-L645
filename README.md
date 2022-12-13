# Nahuatl and Spanish Speaker Segmentation & Identification

There has been little research done to distinguish Nahuatl from Spanish and identify one from another using machine, primarily because of the intense overlap between the two languages and the prevalence of natively bilingual speakers of both languages. This project aims to use deep
learning methods on code-mixed Spanish
and Nahuatl speech for language identification. It also aims to analyze the
speech data to derive insights into spokenlanguage features of either language, with
the intent of establishing the identity of
Nahuatl, as a language distinct from Spanish.

1. Introduction

Language data is vital to building NLP solutions
for the world’s languages. For low-resource languages like Nahuatl, building and maintaining a
data corpus is a challenging task, owing to the
lack of proper quality and quantity of training
data. Moreover, the combined effect of over 500
years of language contact, and socio-linguistic and
political factors, resulted in Nahuatl being classified as an endangered language. This project
uses computational methods to uncover characteristic spoken-language features of Highland Puebla
Nahuatl while learning to identify the language itself, in speech. The goal is to build a language
classifier for Nahuatl and Spanish, incorporating
previous work in speech-language research, using
supervised learning on our dataset.


2. Dataset

The speech data from Radio Tsinaka, a bilingual radio station in Mexico. The language classifier was trained on annotated audio segments
from their broadcasts in both Spanish and Nahuatl. The data has been collected and annotated
with the joint effort of Robert Pugh, Dr. Francis Tyers, Jacob Schmitt and a local in Mexico. The audio segments have been extracted
from hour-long bilingual radio broadcasts, annotated with segment labels from one of the following: ‘esp’(=Spanish), ‘azz’ (= Highland Puebla
Nahuatl), ‘ambos’ (=Both Spanish and Nahuatl),
‘na’(=Neither Spanish nor Nahuatl). The data was
split in an 80:10:10 ratio for the training, validation, and test sets. to keep together data with
similar background noises, and hence, mitigate,
as much as possible, the challenge of learning
and predicting based on similar audio background
noises.


3. Methodology

For the implementation, Speech Brain was used. The current version takes the annotated data and converts it into the relevant yaml file for training the data on the pre-built model. It is further planned to analyze this bilingual model, so built to potentially create a mapping between either language or their respective
phonological features to conclude on distinctive
speech characteristics that separate Nahuatl from
Spanish. 


#About the Project

This folder provides a working, documented setup for speaker identification of Nahuatl and Spanish speakers. The model is based on SpeechBrain’s speakerID model, which was trained on a few hours of data. The data we use is annotated data collected with the joint efforts of Robert Pugh, Dr. Francis Tyers. OpenRIR has also been used for augmentation and noise reduction.

1. There are 5 files here:

* `azz_esp.ipynb`: the main code file, outlining the speaker identification process
* `train.py`: the training code file, outlines the entire training process.
* `train.yaml`: the hyperparameters file, sets all parameters of execution.
* `custom_model.py`: A file containing the definition of a PyTorch module.
* `my_tools.py`: Prepares the data manifests using the annotated data
* `sample_tsinaka.tar.gz`: Zip file for (sample) annotated data
* `Research.zip`: Zip file containing folder to upload to google drive

To run the code, we need to open the main code file `azz_esp_train.ipynb` in google colab and proceed accordingly. A few prerequisites for running:

* The data needs to be uploaded to the appropriate folders in GoogleDrive. The data has been mounted under Research/training/data/sample folder while the training files have been mounted under Research/training folder. If data is being uploaded dynamically, the sample files need to be uploaded under the appropriate folders and paths need to be changed accordingly. The easiest way to run the code would be to upload the Research zip folder into your GoogleDrive and then run the code
* The function prepare_mini_librispeech in the my_tools.py file automatically creates the respective train, valid and test json files for the annotated data, under the /training folder
* The main code will prepare the data manifest files for the data, combining it with the OpenRIRs library, and then train a model with dynamically augmented samples. The training and evaluation are performed using the following piece of code, already incorporated in the main code file:

```
!python train.py train.yaml
```
Note: Any parameters required to be altered need to be passed into the above command, so it can be overridden by the yaml file created.
* Using GoogleDrive may sometimes lead to errors in accessing the audio files, in which case, just re-run the above piece of code.


2. Training

The training output generates the following under /training:

* results: nested directory containing the generated log.txt and the label_encoder file, alongwith the copy of the hyperparams.yaml and train.py files.
* RIRS_NOISES: nested directory containing audio files from the Room Impulse Response and Noise Database, required for data augmentation and noise suppression.
* train.json, valid.json and test.json files: The corresponding files used for training and evaluation.

The current version is buggy with an assertion error that is being worked on at the moment.

3. Further Development

Using Inference for predictions on new data using the SpeechBrain EncoderClassifier class.


# Citations

@misc{speechbrain,
  title={{SpeechBrain}: A General-Purpose Speech Toolkit},
  author={Mirco Ravanelli and Titouan Parcollet and Peter Plantinga and Aku Rouhe and Samuele Cornell and Loren Lugosch and Cem Subakan and Nauman Dawalatabad and Abdelwahab Heba and Jianyuan Zhong and Ju-Chieh Chou and Sung-Lin Yeh and Szu-Wei Fu and Chien-Feng Liao and Elena Rastorgueva and François Grondin and William Aris and Hwidong Na and Yan Gao and Renato De Mori and Yoshua Bengio},
  year={2021},
  eprint={2106.04624},
  archivePrefix={arXiv},
  primaryClass={eess.AS},
  note={arXiv:2106.04624}
}

# References

1. Fortification of Neural Morphological
Segmentation Models for Polysynthetic
Minimal-Resource Languages: Katharina
Kann, Manuel Mager, Ivan Meza-Ruiz,
Hinrich Schutze: 1804.06024.pdf (arxiv.org)
2. Multilingual and code-switching ASR challenges for low-resource Indian languages:
Anuj Diwan, Rakesh Vaideeswaran, Sanket Shah, Ankita Singh, Srinivasa Raghavan, Shreya Khare, Vinit Unni, Saurabh
Vyas, Akash Rajpuria, Chiranjeevi Yarra,
Ashish Mittal, Prasanta Kumar Ghosh,
Preethi Jyothi, Kalika Bali, Vivek Seshadri,
Sunayana Sitaram, Samarth Bharadwaj, Jai
Nanavati, Raoul Nanavati, Karthik Sankaranarayanan: 2104.00235v1.pdf (arxiv.org)
(“ISCA Archive”)
3. Meta-Transfer Learning for Code-Switched
Speech Recognition Genta Indra Winata,
Samuel Cahyawijaya, Zhaojiang Lin,
Zihan Liu, Peng Xu, Pascale Fung:
2004.14228v1.pdf (arxiv.org)
4. Large vocabulary speech recognition for languages of Africa: multilingual modeling and
self-supervised learning, Sandy Ritchie, YouChi Cheng, Mingqing Chen, Rajiv Mathews, Daan van Esch, Bo Li, Khe Chai Si:
2208.03067.pdf (arxiv.org) (“Large vocabulary speech recognition for languages of
Africa ...”)
5. Rethinking Data Augmentation for LowResource Neural Machine Translation: A
Multi-Task Learning Approach, V ??ctor
M. S ?anchez-Cartagena, Miquel Espl`aGomis Juan Antonio P ?erez-Ortiz, Felipe
S ?anchezMart ??nez: Rethinking Data Augmentation for Low-Resource Neural Machine
Translation: A Multi-Task Learning Approach (aclanthology.org) (“Rethinking Data
Augmentation for Low-Resource Neural
Machine ...”)
6. Speech Brain, Dr. Mirco Ravanelli and
Dr. Titouan Parcollet, multiple contributors:
SpeechBrain: A PyTorch Speech Toolkit
7. Annotated bilingual data, Robert Pugh:
Lguyogiro (Robert Pugh) (github.com)
8. Room Impulse Response and Noise Database: http://www.openslr.org/28
