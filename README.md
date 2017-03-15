# harmony-classifier
Deep Learning Audio-to-Harmony Classifier

Copyright 2017 Koyote Science LLC

See my personal website http://www.douglasjmason.com/wordpress/?page_id=419 for more information and a general-audience introduction. 

Adapted from https://humblesoftwaredev.wordpress.com/2016/05/02/an-audio-dataset-and-ipython-notebook-for-training-a-convolutional-neural-network-to-distinguish-the-sound-of-foosball-goals-from-other-noises-using-tensorflow/

Key changes from above work:
* moved from softmax one-hot classification to multi-label sigmoid classification 
* classifying on pitch classes (https://en.wikipedia.org/wiki/Pitch_class)
* refactored code and added diagnostic outputs for debugging the network
* 2-dimensional convolutional networks and max-pooling weren't necessary in the original work to train model, so they were removed
* replaced net with funnel-shaped fully-connected layers
* generate "chords" from random weights applied to single-note samples added together (see data generation below)
* using the full FFT as opposed to the dimensionality-reduced Mel Spectrogram -- this is necessary since the Mel spectrogram is lower resolution and captures timbre, not pitch content
* only uses one frame of the FFT as opposed to the full spectrogram, motivating changes to the net structure

Notes on data generation:
* samples are created from Ableton by running the Max patch "music_MNIST_melody.maxpat"
* to work that, open Ableton Live (or any software synth), set output to SoundFlower (2ch) and MIDI input to "from Max 1", turn on Audactiy, have it read in SoundFlower (2ch), and run the Max Patch.
* the current version only uses bank '0' and then relabels it.
* whichever track has recording enabled will produce the necessary notes. Save the Audacity to an aiff and save the "music_MNIST_metadata.txt" to an appropriate file

Notes on running:
* should run currently using a previously-trained model (models have a small footprint) by running all cells in Audio-to-Harmony Development.ipynb
* to create samples dataframe run Build Samples DataFrame.ipynb
* to create training data change the options at the top of Audio-to-Harmony Development.ipynb to True: load_training_data, append_training_data
* if you have a training dataset you can now train the model by setting train_model to True!
* please write to me if you have any comments or questions

Changes between master and real-time-demo:
* added many new sample banks
* added more data "jitter" such as detuning whole chords and individual notes within chords, more noise options
* encoded all choices into easy-to-read hyper parameters
* separated out the sample collection, data preparation, model running and evaluation sectdions since each part is expensive and don't need to be repeated
* added MIDI output of classification to see if it sounds right
* added real-time listening and classification (works on Mac OSX)

Future Work:
* improve upon data creation methods to improve performance in real-world
* improve upon data creation, model running, and model output infra so we can iterate through multiple hyper parameters and evaluate results without human intervention
