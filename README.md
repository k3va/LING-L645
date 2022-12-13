# Nahuatl and Spanish Speaker Identification

This folder provides a working, documented setup for speaker identification of Nahuatl and Spanish speakers. The model is based on SpeechBrain’s speakerID model, which was trained on a few hours of data. The data we use is annotated data collected with the joint efforts of Robert Pugh, Dr. Francis Tyers and + OpenRIR (for noise reduction).

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


Citations

* @misc{speechbrain,
  title={{SpeechBrain}: A General-Purpose Speech Toolkit},
  author={Mirco Ravanelli and Titouan Parcollet and Peter Plantinga and Aku Rouhe and Samuele Cornell and Loren Lugosch and Cem Subakan and Nauman Dawalatabad and Abdelwahab Heba and Jianyuan Zhong and Ju-Chieh Chou and Sung-Lin Yeh and Szu-Wei Fu and Chien-Feng Liao and Elena Rastorgueva and François Grondin and William Aris and Hwidong Na and Yan Gao and Renato De Mori and Yoshua Bengio},
  year={2021},
  eprint={2106.04624},
  archivePrefix={arXiv},
  primaryClass={eess.AS},
  note={arXiv:2106.04624}
}
