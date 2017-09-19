# Overview

## Setup environment

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
- In repo head directory execute:
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


# Resources

## TensorFlow for poets 2 Overview

This repo contains code for the
["TensorFlow for poets 2" codelab](https://codelabs.developers.google.com/codelabs/tensorflow-for-poets-2).

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

