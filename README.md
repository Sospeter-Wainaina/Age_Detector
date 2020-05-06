# Age_Detector
So what really is age_detection
automatically discerning the age of a person solely from a photo of their face.

Typically, you’ll see age detection implemented as a two-stage process:

Stage #1: Detect faces in the input image/video stream
Stage #2: Extract the face Region of Interest (ROI), and apply the age detector algorithm to predict the age of the person
For Stage #1, any face detector capable of producing bounding boxes for faces in an image can be used, including but not limited to Haar cascades, HOG + Linear SVM, Single Shot Detectors (SSDs), etc.

Exactly which face detector you use depends on your project:

Haar cascades will be very fast and capable of running in real-time on embedded devices — the problem is that they are less accurate and highly prone to false-positive detections
HOG + Linear SVM models are more accurate than Haar cascades but are slower. They also aren’t as tolerant with occlusion (i.e., not all of the face visible) or viewpoint changes (i.e., different views of the face)
Deep learning-based face detectors are the most robust and will give you the best accuracy, but require even more computational resources than both Haar cascades and HOG + Linear SVMs
When choosing a face detector for your application, take the time to consider your project requirements — is speed or accuracy more important for your use case? I also recommend running a few experiments with each of the face detectors so you can let the empirical results guide your decisions.

Once your face detector has produced the bounding box coordinates of the face in the image/video stream, you can move on to Stage #2 — identifying the age of the person.

Given the bounding box (x, y)-coordinates of the face, you first extract the face ROI, ignoring the rest of the image/frame. Doing so allows the age detector to focus solely on the person’s face and not any other irrelevant “noise” in the image.

The face ROI is then passed through the model, yielding the actual age prediction.

There are a number of age detector algorithms, but the most popular ones are deep learning-based age detectors — we’ll be using such a deep learning-based age detector in this tutorial.


 Deep learning age detection is an active area of research. Here, we use the model implemented and trained by Levi and Hassner in their 2015 paper (image source, Figure 2).
The deep learning age detector model we are using here today was implemented and trained by Levi and Hassner in their 2015 publication, Age and Gender Classification Using Convolutional Neural Networks.

In the paper, the authors propose a simplistic AlexNet-like architecture that learns a total of eight age brackets:

0-2
4-6
8-12
15-20
25-32
38-43
48-53
60-100
You’ll note that these age brackets are noncontiguous — this done on purpose, as the Adience dataset, used to train the model, defines the age ranges as such (we’ll learn why this is done in the next section).

We’ll be using a pre-trained age detector model.
you can add as many images as you would like and feel free to contribute
