A repository containing my implementation of Machine Learning Security experiments.

## Code Description

### Membership_Inference Directory
This directory contains my implementation of the techniques described in the 2017 S&P paper "Membership Inference Attacks Against Machine Learning Models" by Shokri et al.

**Shokri's Membership Inference Method in Detail**: 

Membership inference attacks aim to determine whether a specific data sample was used to train a target machine learning model. This is a significant privacy concern, especially for models trained on sensitive data like medical records or financial information.

The key components of my implementation following Shokri's approach include:

1. **Shadow Model Training**: I created multiple shadow models that mimic the behavior of the target model. These shadow models are trained on datasets sampled from the same distribution as the target model's potential training data. For each shadow model, I maintain records of which data points were used in training ("members") and which weren't ("non-members").

2. **Attack Model Training**: Using the shadow models' outputs, I trained specialized attack models that learn the difference between confidence vectors produced for member vs. non-member data points. These attack models essentially learn to recognize the "fingerprint" of data that was used during training.

3. **Data Synthesis**: When direct sampling from the target distribution isn't possible, I implemented the paper's data synthesis algorithm to generate appropriate training data for shadow models.

4. **Model Evaluation**: I evaluated the attack success rate on the CIFAR-10 dataset, measuring how effectively the attack models can distinguish between member and non-member data points.

The implementation consists of several key components:

The implementation consists of several key components:

- **data_synthesis.py**: Implementation of Algorithm 1 from the paper, which generates synthetic data when direct sampling from the target distribution isn't possible.

- **shadow_models.py**: Contains the shadow model implementation that mimics the target model's behavior. These shadow models generate the training data needed for the attack models.

- **attack_models.py**: Implements the actual membership inference attack models. These classifiers are trained to distinguish between member and non-member samples based on confidence vector patterns.

- **Experiment_CIFAR10.py**: A complete experiment implementation using the CIFAR-10 dataset, demonstrating the effectiveness of the attack in a practical setting.

- **nn_model.py**: Neural network architecture implementations using PyTorch.

- **utils.py**: Utility functions for data preprocessing, evaluation metrics, and other helper functions.

The results from my implementation show that membership inference attacks can indeed pose a significant privacy risk to machine learning models, particularly those that are overfitted or trained on small datasets.