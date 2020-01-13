# Scale AI Engima_machine coding assignment
Learning the Enigma with LSTM
## Problem Statement ##

Implement a deep sequence model that can decrypt messages from an enigma machine. The messages can be up to 42 characters in length. Do not use an unnecessarily large network, anything more than 60K parameter is overkill.
You are expected to achieve a score of 0.9, feel free to predict longer sequences as a stretch goal.

## Contents of the repo ##

1. Readme file
2. Helper Functions provided [cipher_take_home_py]()
3. Jupyter Notebook - Overall | [Google Collab Notebook](https://colab.research.google.com/drive/1uYrSfZqJTLRHxzXmY-3TBrpzX2ww3_GY) | [main_file.ipynb]()
4. Jupyter Notebook - Only testing by load saved model | [Google Collab Notebook](https://colab.research.google.com/drive/10wDGdFqsf93PONiIFHibaZUFzbxIQfHh) | [test_file.ipynb]()


## How to run the files and get the results ##

1. Overall File
    * Run the Python notebook on Google Collab. Particular instructions are mentioned in notebook
         - Mount the Google Drive. Update the root address. This will be root directory.
         - Computational Graph, Summary and models would be saved here for Tensorboard Visualization
2. Test File
    * Run the Python notebook on Google Collab. Particular instructions are mentioned in notebook

## Model Building and Coding ##
### Data Engineering ###

- The decryption of the first letter remains same for a particular varibale.
- Therefore, there is no need to learn the key for the message becuase the Enigma machine is already set to a particular configuration
- The data generated does not need any data cleaning and pre-preocessing since it is perfect simulated data

### Model ###

1. We will try to model this problem character by character prediction
2. Since the decryption of a particular character depends on the previous character and its decryption. 
3. Such a situation is ideally modeled using sequence to sequence neural networks
4. These networks range from deep RNN, GRU, LSTM to deep attention based Encoder-Decoder models
5. Attention-based networks have been proved to a lot better than other encoder-decoder networks
6. These networks are capable of capturing complex sequential patterns where the next symbol is partially determined by events that happened many time steps in the past.

#### Network Architecture ####
1. The following are the criteria used to pick the best network: 
    - Engima decryption is highly dependent if you can learn the key formating in the machine. 
    - These keys are distributed in advance, which gives the initial configuration of the machine to decrypt the message
    - Key list here is pre-defined in the `config` function
2. But with a constraint on ***Number of parameters<60K (Capacity of the network)***, 
    - Stacked LSTM is a good choice 
    - First, considering the learned key format in latent variables would be used throughout the decryption of the string
    - Second, LSTM handles vanishing gradient problem much better than similar networks RNN and GRU units
    
## Model visualization in Tensorboard ## 
- Download the log files form the [link](https://drive.google.com/open?id=1-2Up3k7sqm__4FxeTZhuhRjrMLIyNn8p) and run it on local Tensorboard
- Log files and visualization are also uploaded to Git Repo ##
