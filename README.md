# Transfer Learning in Computer Vision 101

This is the entry point for our Intro to Transfer Learning workshop. The whole goal during this workshop is to go through the 
first steps for image classification with Deep Learning and implement the 
building blocks from scratch. 

If you want to do some reading beforehand, you'll find the following useful:

* [About Tensorflow](https://www.tensorflow.org/)
* [Different subsets of Tensorflow](https://www.tensorflow.org/guide/).
* Notions on image classification and re-training of classifiers in [the original version of this workshop](https://www.tensorflow.org/hub/tutorials/image_retraining#training_on_flowers).

## How do I get set up? ###

1. Make sure you have wget and python3-venv installed: `sudo apt-get install wget python3-venv`.
2. Make sure you create a new virtual environment (instructions below).
3. Install the dependencies with the `requirements.txt` in this repo. This includes the latest Tensorflow.
 **We will be using features released on the latest version (1.12).**
4. There are two sides for this workshop:
    1. Using the current code as-is and understanding its effects (which will serve as an intro).
    2. Getting our hands dirty, re-implementing the code. We will start from branch `ẁorkshop_init`.
  
Python 3.5+ should work. Instructions to create a Python3 based environment are given below.

(If, instead of this, you are used to and prefer using docker, go right ahead! 
[Please choose one based on v1.12 from here.](https://hub.docker.com/r/tensorflow/tensorflow/)))


### TL;DR: Quick start with a virtual environment ###

Assuming you want to store your virtual environment under this same repo (FYI, other people prefer to do so under `$HOME/.venvs`):
```sh
~/TransferLearning$ sudo apt-get python3.6-venv 
~/TransferLearning$ python3.6 -m venv venv-tf
~/TransferLearning$ source venv-tf/bin/activate
~/TransferLearning$ pip install -r requirements.txt
```

#### GPU users

**Only** if you already have a GPU and **working CUDA** installation, do this in addition to the commands above:

```sh
~/TransferLearning$ pip install tensorflow-gpu
``` 

(i.e. same as above **and** install tensorflow-gpu on top.)
### Pre-trained model & new dataset ###
**Linux users**: run this from the repo root folder:
```sh
~/TransferLearning$ bash sh/downloads.sh
```

This script will:
1. download a [pretrained model](https://github.com/JonathanCMitchell/mobilenet_v2_keras/releases/download/v1.1/mobilenet_v2_weights_tf_dim_ordering_tf_kernels_1.0_128_no_top.h5)
and save it in the correct location.
2. download a flower dataset, already [split](https://www.dropbox.com/s/n257xs7qvnlfik8/split_flowers.tgz?dl=0) into training, validation and testing sets, and extract it to the correct location.


#### Resulting files ####
Whichever method you chose, your folder structure should be:

```
~/TransferLearning$ tree tf_files/
tf_files/
├── split_flowers
|   ├── train
|   │   ├── daisy
|   │   │    ├── image12345.jpg
|   │   │    └── ...
|   │   ├── dandelion
|   │   ├── roses
|   │   ├── sunflowers
|   │   └── tulips
|   ├── val   
|   │   ├── daisy
|   │   │    ├── image456779.jpg
|   │   │    └── ...
|   │   ├── dandelion
|   │   ├── roses
|   │   ├── sunflowers
|   │   └── tulips
|   └── test
|       ├── daisy
|       │    ├── image234673.jpg
|       │    └── ...
|       ├── dandelion
|       ├── roses
|       ├── sunflowers
|       └── tulips
...
```


## Finding your way ###
`sh` is your entry point; there's a bash script to showcase the usage of the retraining code.

`scripts` contains the retraining code; notice there have been major 
modifications in the API (Tensorflow has changed _a lot_, thankfully)  
since the original tutorial was released, so only the interface should feel 
familiar.

`tf_files` contains data, models and tensorboard logs (training_summaries).


### Warning
Notice after you have played with the current state of the code, we will be re-implementing data loading, model loading 
and training.


## Tensorboard ####
Notice tf_files/training_summaries contains the following structure:

```
experiment_label
└── training_timestamp1
    └── events_file
```
    
This way you will be able to compare the loss function and other metrics from different trainings in the same Tensoboard
plot. If you don't fully follow this currently, don't worry, it will be explained during the Workshop.

![tensorboard](doc/tensorboard_multiple.png)

Once you've already launched a training, go to a second terminal and
start your Tensorboard with:

```sh
~/TransferLearning$ tensorboard --logdir=tf_files/training_summaries &
```

Go with your browser to http://localhost:6006 and enjoy!


## Plan for the workshop

**[Check the wiki!](https://github.com/ividal/TransferLearning/wiki)**

Recap:

We'll be switching back and forth between the command line (to launch trainings) to
Tensorboard (to see what's going on).

We will be re-implementing different modules to load images, load pre-trained models and train.

The ranch `workshop` contains incremental commits, showing building blocks one by one.

## License ###
Modifications are under the same Apache license as the original Tensorflow code.
