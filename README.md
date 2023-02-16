This project is classification project using leaf images. The idea is to be able to identify diseased vs healthy leaves. There are 11 different plants and the entire dataet is divded into 22 categories.

The dataset is from Kaggle: This is a collection of about 4503 images of which contains 2278 images of healthy leaves and 2225 images of the diseased leaves. Twelve plants named as Mango, Arjun, Alstonia Scholaris, Guava, Bael, Jamun, Jatropha, Pongamia Pinnata, Basil, Pomegranate, Lemon, and Chinar have been selected. Images are split between training, test, validating and prediction datasets for model training and testing purposes.

**Why leaves matter:**

Food Security:

The United Nations declared 2020 the International Year of Plant Health. It is estimated that food production will need to increase by 60% by 2050 to feed the estimated 10 billion people expected on Earth.

According to the university of Hawaii Manoa leaf disease can lead to 90% loss in yields for mangoes. Research conducted by the University of Florida found that 90% of yields were lost due to leaf disease in pomegranates. 

Economics:

The Food and Agriculture Organization of the United Nations (FAO) estimates that plant diseases cost the global economy around US$220 billion per year, with 20–40% of crop production lost.

**Data**

The data is split in train, validation and tests sets. All models used the validation set to calculated thier initial accuracy before being evaluated on the test set. Here is a look at some of the images in the train set:

![Leaves](https://user-images.githubusercontent.com/115169255/219439381-782abf30-e933-4a1f-a1f4-322a10c271f6.png)

**CNN**

I used CNN models, which are excellent for processing data with grid patterns such as images. A CNN model consists of convolution, pooling and fully connected layers. The first two layers are responsible for feature extraction and the connected layers are responsible for the final output such as classification. 

Convolution is a mathematical operation that does an element wise product on the input(Tensor) with an array of numbers(kernel). The resulting tensor is sent to a activation function, which decides whether the output should be set to 0 or not. The tensor is then collected by the pooling layers which decides how much and what information to keep. For example, Max pooling will only keep the highest value in a grid of convolutions. This reduces the dimentionality and decreases the amount of learnable parameters. Lastly, the calculations are passed to the connected(dense) layers where the features are "flattened" into a one dimentianal array and classificaion probabilities are calculated. 

Our goal in training a model is to reduce the loss between the ground truth of the data and what the model is predicting. To this end CNN models use backpropagation, a process where weights are updated using gradient descent to minimize loss(error).

**Models**

I created a 2d CNN model, with a 3x3 kernel, 2x2 stride and relu activation. This base model has three layers of convolutions and poolings before flattening and fed to the dense layer. The softmax funtion then takes all this information and calulates probabilities. I deciced to train models for fifty epochs; an epoch when the data is processed fully forwards and backwards in the model. As expected, the model was not accurate and was overfitting the data. 

![BaseAccuracy](https://user-images.githubusercontent.com/115169255/219435623-e53a471e-a37f-4524-aca4-2538cc552f23.png)

**Overfitting**

There are a few techniques that help overfitting. I used least absolute shrinkage and selection operator(Lasso) and Ridge regression to penalize the loss function. Also, I added a dropout which nullifies some of the contributions from the layers. This did reduce the overfitting but as accurate as I was hoping for.

![L1ModelAccuracy](https://user-images.githubusercontent.com/115169255/219440404-f9c5a057-fb18-42f8-b637-9aa77fc616e8.png)


**Data Augmentation**

When creating CNN models with the minimal amount of data, it is wise to use data augmentation. Essentially the images are flipped and rotated so the model has more data to train with. This helps the model learn the outlines of the images and helps with classification. The result was a model with good accuracy and was less prone to overfitting. The final accuray on the model on the test set was 75%.

![L1Model2Accuracy](https://user-images.githubusercontent.com/115169255/219446397-6c48c1a5-9049-47b2-8069-879322251dbb.png)

Here is the artitecture of my final model:

![L1Model2](https://user-images.githubusercontent.com/115169255/219447549-63904b21-136f-46a9-bda6-9e4b5546f059.png)


