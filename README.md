# 5LayerCNN_birdclassification
5-Layered CNN project to identify birds - ACM Fall Onboarding Project, won best Model + Paper Award
# MLab Onboarding Project – Fall 2024

This repository contains my completed onboarding project for Stanford ACMLab (Fall 2024). The goal of this project was to demonstrate familiarity with data handling, model implementation, and experimental analysis (specifically for CNNs) using standard machine learning tools and practices.

## Project Summary

In this notebook, I:
- Loaded and explored a sample dataset
- Performed preprocessing and parameter hypertuning
- Implemented and trained a basic 5 layered CNN with dropout layers and pooling
- Evaluated model performance using metrics and visualizations

## Technologies Used

- **Python 3** 
- **Jupyter Notebook**
- **NumPy** 
- **Pandas** 
- **Matplotlib & Seaborn** 
- **PyTorch** 
- **Torchvision** 
- **PIL (Python Imaging Library)** 
- **h5py**
- **TQDM** 

Anagha Ramaswamy, Elana Chen, Luiza Ribeiro, Sabrina Yen-Ko
ACMLab Fall 2024 Onboarding Project
04 December 2024

MLab Bird Classification Written Report

Architecture. What model class did you choose, and why? Did you experiment with different architectures? How did they perform?
We settled on a 5-layer convolutional neural network (CNN) with Max Pooling after the second, third, fourth, and fifth layers. We found this architecture allowed us to capture the various differing features while still being able to train in a reasonable amount of time and avoid overfitting.
We experimented with different architectures, including the initial 3-layer CNN, a 10-layer CNN, and the ResNet50 architecture. The 3-layer CNN performed adequately with minimal training, but performance eventually plateaued at around 60% accuracy, Training for more epochs caused it to overfit rapidly. We were unable to adequately train the 10-layer CNN with the given GPU power. While it could have potentially resulted in more accurate predictions, we decided it was not feasible to train it in the amount of time we had. ResNet50 achieved a final validation accuracy of 66.56% after 50 epochs with a batch size of 32, but our 5-layer CNN outperformed it, achieving a validation accuracy of 82.96% at 150 epochs and a batch size of 64. 

2. Training. How did you train your model? What losses did you use and why? What hyperparameters did you tune and what results did you see? How can you explain your choice of hyperparameters?
We also evaluated model performance across varying hyperparameters. A fixed learning rate of 0.001 resulted in stable, efficient convergence across cases. The training loop included real-time monitoring of training loss to detect overfitting. Afterward, to visualize training dynamics, we plotted the loss values at each epoch. This plot allowed us to monitor how the loss changed over epochs, helping us identify signs of underfitting (both losses remaining high) and noticing when the loss plateaued.
Smaller batch sizes (e.g., 32) led to unstable training, particularly with more complex architectures. Increasing the batch size to 64 improved generalization while maintaining training efficiency. The 5-layer CNN with batch size 64 outperformed its counterpart with a batch size of 32, achieving higher validation accuracy (82.96% vs. 77.65%) and a lower final loss.
Training for 50 epochs often resulted in underfitting for more complex models. Extending training to 100–150 epochs consistently improved validation accuracy. However, overfitting was observed in some cases, such as with the 3-layer CNN, when trained for more than 10 epochs.
Data augmentation significantly improved validation accuracy across all models. The 5-layer CNN trained with augmentation showed a marked improvement, reaching 82.96% validation accuracy compared to its unaugmented counterpart.
Incorporating dropout into the 5-layer CNN improved generalization, achieving a validation accuracy of 79.26% and a final loss of 0.4125 after training for 150 epochs; however, this performance was not as high as the model without dropout layers, which reached an accuracy of 82.96%.



3. Results. Did you validate or test your model? Explain your choice of validation and test set. Report and describe strategies to reduce overfitting, if present. Did you conduct any error analysis? Can you hypothesize an explanation for the errors?
We validated our model using a randomized 80/20 train-test split. When choosing a validation and test set, we aimed to evaluate the data as well as have our model generalize to new data. The 80/20 split is a common and straightforward approach, using 80% of the data for training (to learn patterns, relationships, and features) and the remaining 20% for testing. This split ensures that the model has enough data to learn from while also using a sufficient test set to evaluate its performance on new examples. The randomness of the split helps limit biases in the data that could arise from a deterministic split and prevents overfitting. Other strategies used to reduce overfitting were implementing image augmentation and dropout layers. We used image augmentation techniques like rotation, flipping, and cropping that helped our validation accuracy and final loss results. However, including the dropout layer was ineffective, so we did not continue with that implementation. 
To conduct error analysis, we analyzed the predictions our model made as compared to true values. We looked at which labels were frequently misclassified by our model to detect if certain classes were more difficult to classify overall. The following graph shows the percentage of wrongly labeled examples for the validation dataset. We found that the Albatross (class 7) and Purple Finch (class 5) were most commonly misclassified, which may have been because they share common characteristics with other classes. 


