# Keras_to_TFLite_for_Android
How to convert a trained Keras neural network to TensorFlow Lite, that can be applied in an Android application

I will summarize this procedure here, as it was a bit time intensive for me to pull together its parts from across the internet.

## Starting point: Keras trained model .hdf5 file

The starting point of this conversion is a Keras for Tensorflow - trained neural network model file. A trained Keras model file usually is of format .hdf5 or .h5 in-short.

### Step 1: Convert model.hdf5 to protobuf Tensorflow format .pb

Use the attached tool keras_to_tensorflow.py:

--> 	*python keras_to_tensorflow.py -input_model model.h5 –output_model outputmodel_path.pb*
