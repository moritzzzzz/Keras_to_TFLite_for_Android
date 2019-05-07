# Keras_to_TFLite_for_Android
How to convert a trained Keras neural network to TensorFlow Lite, that can be applied in an Android application

I will summarize this procedure here, as it was a bit time intensive for me to pull together its parts from across the internet.

## Starting point: Keras trained model .hdf5 file

The starting point of this conversion is a Keras for Tensorflow - trained neural network model file. A trained Keras model file usually is of format .hdf5 or .h5 in-short.

## Step 1: Convert model.hdf5 to protobuf Tensorflow format .pb

Use the attached tool keras_to_tensorflow.py:

--> 	*python keras_to_tensorflow.py -input_model model.h5 –output_model outputmodel_path.pb*

Now we have the Keras-trained model in a frozen Tensorflow format .pb.

## Step 2: Converting TF protobuf model.pb to TFLite model.tflite

I could not get it to run under Windows. Therefore run it on Linux.

**My setup:**

- Ubuntu 18.04
- python 3.6  
              --> *sudo apt-get install python3.6*
              --> *sudo apt-get install python3-pip python3-dev*
- Tensorflow 1.6 (this version includes toco)
              --> *pip3 install tensorflow==1.60*
 
 ### Conversion using Toco
 
 For this we assume that the input to our model was a 299x299 pixel RGB image. (Dimensions 299x299x3)
 
 Below command should be one not-interrupted command!
 
 */home/moritz/.local/bin/toco --input_file=Desktop/model.pb* 
 *--output_file=Desktop/model.tflite* 
 *--input_format=TENSORFLOW_GRAPHDEF* 
 *--output_format=TFLITE --input_shape=1,299,299,3*                    
 *--input_array=input_1 --output_array=output_node*                    
 *--inference_type=FLOAT*

Note how the input_shape has to be defined according to the expected input of your model, as well as the name of the input layer. (*input_1* in my case)
Also the name of the output layer has to be defined correctly. (*output_node* in my case)

**Finding the output_array name**
This can pose a difficulty, as when using standard layers in Keras, their names are not obvious. Therefore i have added a line in the code of *keras_to_tensorflow.py* that will print out the name of the output layer:


