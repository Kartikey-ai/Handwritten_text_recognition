# Handwritten_text_recognition

Objective was to predict the handwritten text in the images provided by the dataset. 
Various deep learning and machine learning algorithm and new researches are done in this field.

What I have used in this implementation is CNN + Bi LSTM + CTC.
Convolution neural network was used to extract a feature map from the images. Then this feature map 
was fed into LSTM and then using CTC function actual text was predicted.  

![Alt text](predicted_images/handwrittentext1.jpg?raw=true "Optional Title")

## CTC 
Imagine a dataset of text images and specifying each time-step of the image’s corresponding character. There are a couple of issues with this approach:

Annotating a dataset at the character level is a tedious task
What if the character takes up more than one time-step? It will result in duplication of the characters. 
Leading to problems like <good> becomes <ggoood> or <hey> becomes <hheyy>.
  
Here, CTC helps us:

CTC only requires the text that occurs in the image. We can ignore both the width and position of the characters in an image.
There is no need for post-processing the output of the CTC operation! Using decoding techniques, we can directly get the result of the network.

## Working of CTC
  
CTC merges all the repeating characters into a single character. For instance, the word is <hey> where ‘h’ takes two time-steps, ‘e’ takes one time-step and ‘y’ takes two time-step each. Then the output from the network using CTC will be ‘hheyy’, which as per our encoding scheme, gets collapsed to ‘hey’.

What about the words where there are repeating characters Like <good> For those cases, CTC introduces a pseudo-character denoted as “-“ . While encoding the text, if a character repeats, then a blank is placed between the characters in the output text. Let’s consider the word ‘good’, possible encodings for it will be, ‘gg-oo-oo-d’, ‘ggg-o-o-ddd’, wrong encoding will be ‘gg-oo-d’, as it’ll result in ‘god’ when decoded. The CRNN is trained to output the encoded text.  
