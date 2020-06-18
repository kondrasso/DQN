[![Google Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kondrasso/DQN/blob/master/DQN_QUEUE.ipynb)

# Queue managind via DQN agent

Application of DQN algorithm in RL model to queue management. Data used in this project comes from [COVID-2019 dataset](https://www.kaggle.com/iamhungundji/covid19-symptoms-checker)  

## Premise

RL models provide a great insight to optimization. We can try to determine "optimal" strategy, by which means agent can maximize or minimize given function.
By constructing an enviroment (state-space) and determining possible actions (action-space) we can create sophisticated constraints to a given task, that can serve a great representation of a field's real-world specifics.
Thus we can find a balance between abstract and real, which gives us opportunity to create ready-to-use agents to solve optimization problems.

## Features

Fully working cutsom queue model fully compatible with OpenAI Gym API, and contains all necessary steps to run it out-of-the-box in Google colab. 

## Queue model

Queue consists of patients, which are represented by ![img](https://latex.codecogs.com/gif.latex?16%5Ctimes%201) vectors, where:  

![img](https://latex.codecogs.com/gif.latex?x_1) - time that patient spent wainting in a queue, discrete; ![img](https://latex.codecogs.com/gif.latex?0%20%5Cleq%20x_1%20%3C%20inf)   

![img](https://latex.codecogs.com/gif.latex?x_2) - severity of the given patient which a pre-dertimned and implicitly dependent of time ![img](https://latex.codecogs.com/gif.latex?x_2%20%3D%20c%20&plus;%20f%28x_1%29)   

![img](https://latex.codecogs.com/gif.latex?x_3%2C...%2Cx_%7B16%7D) - various features from dataset, binary.

Thus, in each given time state-space (queue) is

![img](https://latex.codecogs.com/gif.latex?Q%20%3D%20%5Cbegin%7Bbmatrix%7D%20x_%7B11%7D%20%26%20x_%7B21%7D%20%26%20%5Cdots%20%5C%5C%20%5Cvdots%20%26%20%5Cddots%20%26%20%5C%5C%20x_%7B1n%7D%20%26%20%26%20x_%7Bnn%7D%20%5Cend%7Bbmatrix%7D)

## Actions

Action space is discrete and described like 

![img](https://latex.codecogs.com/gif.latex?AS%20%3D%20%5Cleft%20%5C%7B%20a_1%2Ca_2%2Ca_3%2Ca_4%20%5Cright%20%5C%7D)

where:  
![img](https://latex.codecogs.com/gif.latex?a_1) - remove last patient, ![img](https://latex.codecogs.com/gif.latex?x_%7Bn%7D) in our case  
![img](https://latex.codecogs.com/gif.latex?a_2) - remove patient with lognest time, thus ![img](https://latex.codecogs.com/gif.latex?%5Cmax_%7Bn%7D%20%28x_1_1%2C%20...%2C%20x_n_1%29)  
![img](https://latex.codecogs.com/gif.latex?a_3)  - remove patient with maximal severity, thus ![img](https://latex.codecogs.com/gif.latex?%5Cmax_%7Bn%7D%28x_1_2%2C%20...%2C%20x_n_2%29)  
![img](https://latex.codecogs.com/gif.latex?a_4)  - remove patient with maximal linear combination of weights and binary features, thus ![img](https://latex.codecogs.com/gif.latex?%5Cmax_%7Bn%7D%28S_1%2C...%2CS_N%29)  
where:

![img](https://latex.codecogs.com/gif.latex?S%20%3D%20%5Csum_%7Bj%3D3%7D%5E%7B16%7D%20x_i_j%20w_j)

and w - vector of feature weights

## Goal

Our goal is to find a strategy (sequence of actions in each game) that can minimize 

![img](https://latex.codecogs.com/gif.latex?%5Csum_%7Bi%3D1%7D%5E%7Bn%7D%5Csum_%7Bj%3D1%7D%5E%7B16%7D%20x_i_j%20w_j)

## Results 

Results looks promising, but to conclude we need much more computational power and time due to enormous number of all possible state-spaces and quite unbalanced dataset. 

## Acknowledgements

Thanks for the idea of DQN managed queues to [Yasar Sinan Nasir and Dongning Guo, Multi-Agent Deep Reinforcement Learning for Dynamic Power Allocation in Wireless Networks \\ 2018, arXiv:1808.00490](https://arxiv.org/abs/1808.00490)
