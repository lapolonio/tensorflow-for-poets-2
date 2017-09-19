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
```

