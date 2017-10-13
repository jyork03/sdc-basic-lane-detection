# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[final2]: ./test_images_output/final_2.jpg "Lanes Detected"

![alt text][final2]

## Overview

**Below describes details of a program that finds lane lines on the road**

## Running the Code

First clone the project down.

Running it with Docker:
```bash
docker pull udacity/carnd-term1-starter-kit
cd project/directory
docker run -it --rm -v `pwd`:/src -p 8888:8888 udacity/carnd-term1-starter-kit
```

If you don't use docker, you'll need to install the dependencies yourself.

The dependencies include:
* python==3.5.2
* numpy
* matplotlib
* jupyter
* opencv3
* moviepy
* ffmpeg


## Contents

The project is written in a Jupyter Notebook, and the file is `P1.ipynb`.  The premodified images and videos are
located in `./test_images` and `./test_videos` respectively.  The modified images and videos are located in 
`./test_images_output` and `./test_videos_output`.

If you wish to read a description of how the algorithm works, as well as shortcoming and ideas for improvement,
please read writeup.md.