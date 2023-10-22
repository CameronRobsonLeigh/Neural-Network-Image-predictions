# Neural-Network-Image-predictions

1. Read dataset and create data loaders: 5%
Here we pull through the fashion mnist dataset that consists of 70,000 greyscale 28x28
images belonging to 10 different items of clothing.
Also, here I create transforms which I use to normalize our pixels and convert to tensors. I
was using other transforms such as image rotation that basically create artificial versions of
each image so we more knowledge on the image for training. However this was decreasing
my accuracy further down the line so I ended up removing them. However, the
normalization worked well for me as avoids high and low minima:
Next, we create our training and test variables that have our datasets including the
transformations (60,000 for training and 10,000 for testing), we then place these variables
inside our data loaders with a batch size of 256.
2. Create the model: 40% (Stem: 10%, Backbone: 30%)
So, the stem takes in an image of size 28x28 pixels that we divide into non-overlapping
patches.
We then iterate through our training and testing data loaders and run our patch function for
each image, which we then append our patches and the batch size into a new list. The shape
of our data loaders is [256, 1, 28, 28]. The new shape of our new tensors is [256, 49, 16].
Our next step is to define our backbone which is where our input, multi layered perceptron
and outputs are created. We take in 49 inputs (28x28), I defined 2 multi-layered
perceptron’s and of course 10 outputs which represents the 10 images.
The optimal for my accuracy was this setup, I tried making the network more complex by
adding 10 linear layers however it was decreasing my accuracy slightly.
3. Loss and Optimization function (5%)
For me the optimal loss was the cross entropy loss, this essentially is used when adjusting
model weights during training to minimize the loss.
For the optimization function I used Adam with a learning rate of 0.1 and no weight decay as
this was optimal. The weight decay significantly decreased my model performance and the
learning rate 0.1 seemed to work just right.
4. Training Script and Reporting (30%)
The training script I used is the train_ch3, which takes as parameters our net (our model), our
training iteration which is our patched-up data in it’s correct format (256, 49, 16), test iteration
which is the same but for our 10,000 samples instead of 60,000 samples, our loss function which we
defined earlier (cross entropy loss), our number of epochs (40) and our optimizer (Adam)
For our model, I went with using one block with 6 linear layers, making sure that the backbone
requirements were met:
In the model we use relu as our non-linear optimization function, sigmoid did not perform as well for
me. Non-linear activation functions are known to be the most used activation functions. It makes it
easy for networks to adapt with a variety of data and in general improve performance.
In our model we take the last layer when everything has processed through the network to calculate
the mean feature. Which we then implement our classifier with this mean tensor that will use both
the optimizer and loss to finalize our softmax regression.
In regards to our loss function, I used CrossEntropyLoss function without any parameters as when
adjusting I was getting negative results in relation to my models performance. The default
parameters is what seemed to work best for me.
I went ahead and used 40 number of epochs, around that number gave me the best results. When
going high (100+) for some reason my accuracy decreased, I believe this is because if we allow the
model more windows to train and cipher through the data, there is more chance outliers will be
picked up which will lead to a decrease in performance. 40 epochs means that we cipher through
60000 images 40 times.
The optimizer function that I used is Adam as stated previously, Adam is a method for stochastic
optimization. For me and through references Adam appears to converge faster. Although it is
thought that SGD performs better through its ability to generalise better, for me Adam did perform
better.
When running train_ch3 we also run a variety of other functions making use of the my_utils.py file.
Below is a screenshot of my performance curves:
5. Final model accuracy
My final accuracy was 0.8617788461538461
