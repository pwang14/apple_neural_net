#Apple-recognition neural network

This neural network recognizes if an input image contains an apple or not. 

The code for this neural network comes from https://github.com/mnielsen/neural-networks-and-deep-learning. I have added to and modified code at certain points, though.
It accompanies Michael Nielson's online book 'Neural Networks and Deep Learning', in which the fundamental ideas behind neural networks are introduced and explained.

The neural network consists of 9408 input neurons (representing a 56 x 56 px input image, where each pixel contains three RGB values), two hidden layers with 500 and 25 neurons respectively, and 1 output neuron representing the probability with which the network thinks the input image contains and apple. 

The network is quite standard; it trains through gradient descent (used backpropogation to calculate the gradient vector of the cost function).
However, many techniques were also used to accelerate the learning rate of the network and improve the initialization of its weights and biases.

* I set a centered, circular boundary with a diameter = 6/8 * side length of the input image. For each pixel outside this boundary, I initialized every weight attached to that pixel to be 0.
  This technique relies on the fact that if an input image does contain an apple, that apple will most likely be centered. As such the background pixels surrounding the apple should have no effect on the output of the network.

The remaining techniques are outlined in the 3rd chapter of Nielson's book (titled, 'Improving the way the neural networks learn').
* Using a cross-entropy cost function allows the final hidden layer of the neural network to learn faster when compared to using a quadratic cost function.
* Modified guassian distribution for the initialization of the weights decreases the number of saturated neurons, allowing for faster learning
* Network has capability for L2 regularization

I created the files data_collect.py and display.py to collect the images in the apple_data folder, resize them, store their RGB and luminance values in arrays, and feed the data to the neural network.

The neural network trained on a dataset of 1775 pictures. The training data was collected by myself. I took 936 pictures of apples, and 839 picutres of non-apples.
I first trained the network for 50 epochs, with a learning rate of 0.5. When it reached an above 95% accuracy with the training data, it stored its own weights and biases in parameters.json.
After that, I loaded the network from parameters.json before training it more. I decreased the learning rate to 0.1. Right now, it is at a 97% accuracy with the training data.

If you want to see the network at work on images in the test_data folder, just run display.py.
Before running the program you must first unzip parameters.json and put it in the neuralnet folder.

I collected a small sample of new test images, and ran them through the network. It had an 100% accuracy.