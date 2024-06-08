# Garbage Classification

## Project Goal and Motivation

The project was to develop a machine learning model to classify waste images into two categories. organic and recyclable. For this the Waste Classification Dataset from mendeley was used.

Efficient waste classification is critical for waste management systems. Helping to reduce waste and promote recycling is key to improve sustainability. Improving efficiency and accuracy for waste sorting will improve sustainability (reducing improper disposal, reducing pollution, more recycling, etc.). For example, the project could contribute to a more efficient recycling process and help achieving sustanability goals.

## Data

The data source was the Waste Classification Dataset on mendeley data. https://data.mendeley.com/datasets/n3gtgm9jxj/2

The dataset has a collection of 24705 images of household waste. The images are categorised into two classes: organic (13880 images) and recyclable (10825 images).

The dataset was downloaded and preprocessed to ensure there are no corrupt images and split the dataset into training and validation sets with the ratio 80-20.

To enhance the model's generalization capabilities, data augmentation techniques were used. Layers like random flipping, rotation, zoom, contrast , brightness adjustments were applied on the training images.

## Modeling

I chose ResNet50 as my pretrained convolutional neural network model for this project.

**Following an overview of the architecture**

- Base Model: ResNet50
- Global Average Pooling: To Reduce the spatial dimensions of the feature map.
- Dense Layer: With relu activation (ReLU activation function is used to introduce nonlinearity in a neural network, helping mitigate the vanishing gradient problem during machine learning model training and enabling neural networks to learn more complex relationships in data)
- Dropout Layer: randomly sets input units to 0. Helps to prevent overfitting.
- Ouput Layer: a sigmoid function to output the classification (two classes in our dataset so binary classification)

**Training**

The model was trained for 20 epochs with early stopping to prevent overfitting and model checkpoint callbacks to save the best model.
After the first training fine tuning was performed. In the earlier model, layers from the ResNet50 model were frozen/deactivated. For the fine tuning I activated 20 layers and trained for additional 10 epochs. The learning rate is now lower for the fine tuning.

**Configuration**

Optimizer: Adam
Loss Function: Binary Crossentropy
Metrics: Accuracy, Loss (for training and validation data)

## Interpretation and validation

**Performance**

The model's performance was evaluated using accuracy and loss metrics on both the training and validation sets. The following results were observed:

- Training Accuracy: Improved steadily over epochs, reaching around 94.99%.
- Validation Accuracy: Reached approximately 93% after fine-tuning.

**Validation**

To perform some tests I validated the model with different sample images. Out of 50 images 6 were classified wrong.

To further evaluate the model I have build a classification report and confusion matrix.

- Precision: 0.94 for Organic, 0.92 for Recyclable
- Recall: 0.93 for Organic, 0.94 for Recyclable
- F1-Score: 0.95 for Organic, 0.93 for Recyclable
- Accuracy: 0.94

**Critical thinking**

- High Accuracy Interpretation: High accuracy in both training and validation sets suggests that the model has learned to generalize well from the training data to new, unseen data. This is the ideal scenario. However, it is important to ensure that the dataset is representative of the real-world scenario where the model will be deployed.
- Overfitting Check: the accuracy is extremely high (close to 100%) on the training set and slightly lower but still very high on the validation set, it could indicate some degree of overfitting. This could very possibly be the case when the model learns the training data too well, including the noise, which can sometimes lead to slightly lower performance on the validation set.

**Checking other projects and models with same dataset**
I have checked other projects which did use the same dataset. On kaggle there were some projects visible. The accuracy of them was in the range between 82% up to 94%. So similar results regarding model performance in terms of accuracy.

## My conclusion

I think I successfully developed a deep learning model for waste classification using ResNet50 as my basemodel. The model has high accuracy and robustness, making it usable for automated waste sorting system or in general waste management. It was a insightfull and interesting project and a great learning opportunity.
