# Scale AI Engima_machine coding assignment
Learning the Enigma with LSTM
## Problem Statement ##

Implement a deep sequence model that can decrypt messages from an enigma machine. The messages can be up to 42 characters in length. Do not use an unnecessarily large network, anything more than 60K parameter is overkill.
You are expected to achieve a score of 0.9, feel free to predict longer sequences as a stretch goal.

## Contents of the repo ##

1. Readme file
2. Helper Functions provided [cipher_take_home.py](https://github.com/hkhoont/scale_ai_engima_machine/blob/master/cipher_take_home.py)
3. Jupyter Notebook - Overall | [Google Collab Notebook](https://colab.research.google.com/drive/1uYrSfZqJTLRHxzXmY-3TBrpzX2ww3_GY) | [main_file.ipynb](https://github.com/hkhoont/scale_ai_engima_machine/blob/master/main_file.ipynb)
4. Jupyter Notebook - Only testing by load saved model | [Google Collab Notebook](https://colab.research.google.com/drive/10wDGdFqsf93PONiIFHibaZUFzbxIQfHh) | [test_file.ipynb](https://github.com/hkhoont/scale_ai_engima_machine/blob/master/test_file.ipynb)
5. Tensorboard Log files
6. Tensorboard Image files
7. Saved model

## How to run the files and get the results ##

1. Overall File
    * Run the Python notebook on Google Collab. Particular instructions are mentioned in the notebook
         - Mount Google Drive. Update the root address. This will be the root directory.
         - Computational Graph, Summary, and models would be saved here for Tensorboard Visualization
2. Test File
    * Run the Python notebook on Google Collab. Particular instructions are mentioned in the notebook
    
## Requirements ##
-  `py-enigma`
-  `faker`
-  `PyTorch`
-  `hyperopt`

## Model Building and Coding ##
### Data Engineering ###

- The decryption of the first letter remains the same for a particular variable.
- Therefore, there is no need to learn the key for the message because the Enigma machine is already set to a particular configuration
- The data generated does not need any data cleaning and pre-processing since it is perfect simulated data

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
- Download the log files form the [link](https://drive.google.com/open?id=17WO-mzmo754fUaYQYuDFkP-EZv_W0kKj) and run it on local Tensorboard
- Log files and visualization are also uploaded to Git Repo
## Epoch,Batch,Iteration ##
- Since we are working on simulated data. For each batch, we can generate new simulated data.
- This has allowed us to just iterate over a batch of data
- #Epoch=1 because epoch is the number of times model is trained over the data

## Hyperparameter tuning
- Popularly there are 3 techniques to optimize hyperparameters of the model
- **Grid Search**
    - High computation is required, especially when the grid becomes higher-dimensional. 
    - It does not consider any improvements over any parameters to anchor the tuning. 
    - Brute force method
- **Random Search**
    - Many times random search gives better result
    - However, this is too random for the conclusion and hope for the best parameters
    - It becomes difficult when the number of hyperparameters increases
- **Bayesian Optimization**
    - Bayesian Optimization based on Gaussian process
    - [Tutorial on Bayesian Optimization](https://arxiv.org/pdf/1012.2599.pdf)
- I used a bit of all three techniques, concepts based on learning theory and previous experiences of training deep learning models to hyperparameter tuning
