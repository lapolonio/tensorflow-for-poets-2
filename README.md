# Overview

## Setup environment
```
Boat urls from http://image-net.org/api/text/imagenet.synset.geturls?wnid=n02858304
```


```
mkdir cloud
mkdir boat
mkdir tf_files/ibm_task
mkdir tf_files/ibm_task/cloud
mkdir tf_files/ibm_task/boat
mkdir tf_files/test_ibm_task
mkdir tf_files/test_ibm_task/cloud
mkdir tf_files/test_ibm_task/boat

virtualenv IBM_env
source IBM_env/bin/activate
pip install -r requirements.txt
python -m ipykernel install --user --name=IBM_env
jupyter notebook
```

## How to use

- Open `Data Retreival.ipynb` and execute all cells to retrieve all relevant source flickr images, 
create thumbnail images and put in relevant location
- In repo head directory to train model execute:
```
IMAGE_SIZE=224
ARCHITECTURE="mobilenet_1.0_${IMAGE_SIZE}"

python -m scripts.retrain \
  --bottleneck_dir=tf_files/bottlenecks \
  --how_many_training_steps=4000 \
  --model_dir=tf_files/models/"${ARCHITECTURE}" \
  --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=tf_files/ibm_task
```
- After model is finished training. Open `Model Performance Analysis.ipynb` for model performance
- Open `attributions.ipynb` to visualize gradient activations to gain insight into model internals


## Design Considerations

Google has made available, through Tensorflow, production level deep learning models for the public to use. One model
called MobileNet, optimized for speed and size while maximizing accuracy, was trained on ImageNet data and is 
available to customization. Incorporating an existing model into another model is called Transfer Learning.

The parameters I specified were input image size, 224px and model fraction, 1.0 to maximize the possible accuracy of
the predictions. I used 80/20 split on the retrieved images for each category. I assumed that the images were randomly
ordered, representative of each category distributions and spilt the retrieved image file lists. 80% of the images were used
for training and evaluating the performance of the model. The other 20% was used to measure the out of sample performance. 

# Resources

## TensorFlow for poets 2 Overview

This repo contains code for the
["TensorFlow for poets 2" codelab](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/index.html?index=..%2F..%2Findex#0).

This repo contains a simplified and trimmed down version of tensorflow's
[android image classification example](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/android)
in the `android/` directory.

The `scripts` directory contains helpers for the codelab.

## CNN Atribution
[Attributing a deep network’s prediction to its input features](http://www.unofficialgoogledatascience.com/2017/03/attributing-deep-networks-prediction-to.html)

[Attribution code](https://github.com/ankurtaly/Integrated-Gradients/blob/master/attributions.ipynb)


## Helpful commands
```
pip freeze > requirements.txt

tensorboard --logdir tf_files/training_summaries &
```

