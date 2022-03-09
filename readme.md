# Audio Similarity Search

This notebook seeks to leverage appropriate machine learning techniques to enable similarity search with audio files. The end goal is an effective audio similarity search algorithm that can return similar audio to a user selected file. After reviewing the research, the following approach is attempted:

## Data Sourcing:
* ~760 audio files (98MB on disk) were sourced from a collection of musical instrument samples collected over time, either from commercial libraries or Freesound.
* The audio-data folder should be placed in the root directory alongside this .ipynb Jupyter notebook file, and can be downloaded here: https://drive.google.com/file/d/1RnQkkrvUNa-eWl3yDFaYKnV1lJU8fSjv/view?usp=sharing
* This is a somewhat restricted use case, however enough to demonstrate the success/failure of the approach with respect to audio-based similarity search.
* Audio has been standardized to 22,050Hz sample rate, 16-bit depth, .wav files in order to save disk space, however the ingestion process is capable of handling many audio file types and any sample rate and bit-depth, and itself loads audio at a fixed sample rate.
## Data Ingestion:
* Locating and loading Audio files: Up to the first 2 seconds of each audio file is loaded
* This is a simplifying step that would be trivial to change or add sophisitcation around which 2 section of audio should be loaded (eg; the middle 2 seconds, etc.)
* Mel Spectrogram image generation for each loaded audio file via librosa, with algorithm hop-size set to spread the spectrogram for the given audio length across the entire image size.
* Image Normalization (value normalization)
## Approach:
* Images are fed into a novel Convolutional Autoencoder model in order to train an Encoder to encode the mel spectrogram features into compressed yet meaningful feature vectors.
* The trained Encoder from the Convolutional Autoencoder can then be employed to enable audio to be searched, wherein the encoded embeddings (feature vectors) are used directly in a simple Cosine Similarity search.
* It may be possible to achieve even better image reconstruction with transfer learning, wherein something like a pre-trained network (eg; VGG-19) could be leveraged and fine-tuned for this purpose.
More sophisticated search algorithms, possibly coupled with further dimensionality reduction, may lead to further useful results.