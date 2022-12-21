# tiger-call-classification

This repository is for a Deep Learning solution for Tiger Call classification.

Our dataset was a weakly annotated set of audio clips from a tiger enclosure. Each audio clip is from half hour to an hour long and spans recordings from multiple days.

Even though the dataset was weakly annotated, we took a supervised approach towards identifying tiger calls. To do this, we split longer audio clips in 3 second snippets, denoised them and converted each of them into audio spectrograms. We performed a study of these spectrograms to identify characteristic features of tiger calls and other unique sounds. 

This image is an example of what a tiger call looks like as an audio spectrogram.

![SMM01167_20220929_165802_420_reduced](https://user-images.githubusercontent.com/115058347/208987986-5b8643f6-baee-407f-a65c-ff85502eb3b9.png)

Using this understanding of the audio clips and the weak annotation, we were able to build a dataset of tiger calls. This dataset was divided into two directories, one contained 3 second audio clips of tiger calls and the other had 3 second audio clips corresponding to silence. We used the tiger calls as positive samples labelled as class '1' and silence was labelled as class '0'.

We had 128 samples of each class, which was split into batches of 16 to be fed into a model that we designed and compiled using TensorFlow. Each clips was converted to an audio spectrogram and used as input to the model.

Since, the no. of features in each image was pretty small, we decided to go with a simple convolutional neural network model. Our model uses 2 convolutions layers, a flatten layer, two dense layers and the final dense layers outputs a class prediction. The model summary is as below - 

![Screenshot 2022-12-12 174616](https://user-images.githubusercontent.com/115058347/208989640-e0f35504-45ab-4da6-b9bd-c312d934a1b0.png)

Once the model was trained, we decided to test its performance on longer clips. To do this we split the test clips into 3 second long windows, converted each window to a spectrogram and used this as inout to the trained model.

The model output was an array of class predictions. We converted this array to a csv file where we had columns with the time steps and the corresponding model predictions. We also used this array to create a call density csv file, where we grouped consecutive positive and negative predictions and output the sum of all positive instances.

These outputs will help individuals identify where these tiger calls were identified and make it easier for them to annotate files going forward.
