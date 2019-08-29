# neurodivergent keras with nltk

the official keras docker image...but with [nltk](https://www.nltk.org/ 'https://www.nltk.org/') for natural language processing with deep learning.

to use: 

1) [install docker](https://docs.docker.com/install/ 'https://docs.docker.com/install/')
2) for gpu support, [install nvidia for docker](https://github.com/NVIDIA/nvidia-docker/blob/master/README.md 'https://github.com/NVIDIA/nvidia-docker/blob/master/README.md')
3) check out the repo (or download [Dockerfile](https://github.com/neurodivergent-ai/keras/blob/master/docker/Dockerfile 'https://github.com/neurodivergent-ai/keras/blob/master/docker/Dockerfile'), [theanorc](https://github.com/neurodivergent-ai/keras/blob/master/docker/theanorc 'https://github.com/neurodivergent-ai/keras/blob/master/docker/theanorc'), and [Makefile](https://github.com/neurodivergent-ai/keras/blob/master/docker/Makefile 'https://github.com/neurodivergent-ai/keras/blob/master/docker/Makefile'))
4) run `make` from the same directory

#### examples:

* open a simple, non-gpu [jupyter notebook](http://jupyter.org/index.html 'http://jupyter.org/index.html'):

`make notebook`

* open a jupyter notebook with [cuda](https://developer.nvidia.com/about-cuda 'https://developer.nvidia.com/about-cuda') gpu support:

`make notebook GPU=0`

* open a gpu-supported jupyter notebook with read/write access to your local machine:

`make notebook GPU=0 DATA=~/`

all [indigenous.engineering](https://github.com/indigenousengineering 'https://github.com/indigenousengineering') notebooks use docker with nvidia gpu support & [tensorflow backend](https://keras.io/backend/ 'https://keras.io/backend/').

### for more information, see the original keras documentation below:

# Using Keras via Docker

This directory contains `Dockerfile` to make it easy to get up and running with
Keras via [Docker](http://www.docker.com/).

## Installing Docker

General installation instructions are
[on the Docker site](https://docs.docker.com/installation/), but we give some
quick links here:

* [OSX](https://docs.docker.com/installation/mac/): [docker toolbox](https://www.docker.com/toolbox)
* [ubuntu](https://docs.docker.com/installation/ubuntulinux/)

## Running the container

We are using `Makefile` to simplify docker commands within make commands.

Build the container and start a Jupyter Notebook

    $ make notebook

Build the container and start an iPython shell

    $ make ipython

Build the container and start a bash

    $ make bash

For GPU support install NVIDIA drivers (ideally latest) and
[nvidia-docker](https://github.com/NVIDIA/nvidia-docker). Run using

    $ make notebook GPU=0 # or [ipython, bash]

Switch between Theano and TensorFlow

    $ make notebook BACKEND=theano
    $ make notebook BACKEND=tensorflow

Mount a volume for external data sets

    $ make DATA=~/mydata

Prints all make tasks

    $ make help

You can change Theano parameters by editing `/docker/theanorc`.


Note: If you would have a problem running nvidia-docker you may try the old way
we have used. But it is not recommended. If you find a bug in the nvidia-docker report
it there please and try using the nvidia-docker as described above.

    $ export CUDA_SO=$(\ls /usr/lib/x86_64-linux-gnu/libcuda.* | xargs -I{} echo '-v {}:{}')
    $ export DEVICES=$(\ls /dev/nvidia* | xargs -I{} echo '--device {}:{}')
    $ docker run -it -p 8888:8888 $CUDA_SO $DEVICES gcr.io/tensorflow/tensorflow:latest-gpu
