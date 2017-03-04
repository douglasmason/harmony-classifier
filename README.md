# harmony-classifier
Deep Learning Audio-to-Harmony Classifier

2017 Koyote Science LLC

Adapted from https://humblesoftwaredev.wordpress.com/2016/05/02/an-audio-dataset-and-ipython-notebook-for-training-a-convolutional-neural-network-to-distinguish-the-sound-of-foosball-goals-from-other-noises-using-tensorflow/

Key changes:
* moved from softmax one-hot classification to multi-label sigmoid classification 
* classifying on pitch classes (https://en.wikipedia.org/wiki/Pitch_class)
* generate "chords" from random weights applied to single-note samples added together
* using the full FFT as opposed to the dimensionality-reduced Mel Spectrogram
** this is necessary since the Mel spectrogram mainly captures timbre, not pitch content
