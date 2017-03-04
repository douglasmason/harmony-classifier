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

Notes on data generation:
* samples are created from Ableton by running the Max patch "music_MNIST_melody.maxpat"
* to work that, open Ableton Live (or any software synth), set output to SoundFlower (2ch) and MIDI input to "from Max 1", turn on Audactiy, have it read in SoundFlower (2ch), and run the Max Patch.
* the current version only uses bank '0' and then relabels it.
* whichever track has recording enabled will produce the necessary notes. Save the Audacity to an aiff and save the "music_MNIST_metadata.txt" to an appropriate file

Future work:
* adding new sample banks
* encoding all choices into easy-to-read hyper parameters
* separating out the sample collection, data preparation, model running and evaluation sectdions since each part is expensive and don't need to be repeated
* creating a data creation, model running, and model output infra so we can iterate through multiple hyper parameters and evaluate results without human intervention
