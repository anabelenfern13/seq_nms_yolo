# Seq_nms_YOLO

#### Membres: Yunyun SUN, Yutong YAN, Sixiang XU, Heng ZHANG

---

## Introduction

![](img/index.jpg) 

This project combines **YOLOv2**([reference](https://arxiv.org/abs/1506.02640)) and **seq-nms**([reference](https://arxiv.org/abs/1602.08465)) to realise **real time video detection**.

## Steps

1. Open a terminal and download all the files from this repository `git  clone https://github.com/sarabarahona/seqnmsyolo.git`
1. Download `yolo.weights` and `tiny-yolo.weights` by running

   ```
   wget https://pjreddie.com/media/files/yolo.weights
   wget https://pjreddie.com/media/files/yolo2-tiny.weights
   ```
1. The Makefile has been set to not use neither CUDA and OpenCV (flags in lines 2 and 3 are 0). If you want to use them you can activate them setting the flags to 1.
   Besides, lines 49 and 51 needs to be change to concorde with the version of CUDA, in our case 10.1.
   ```
    COMMON+=  -DGPU  -I/usr/local/cuda-10.1/include/
    LDFLAGS+=  -L/usr/local/cuda-10.1/lib64  -lcuda  -lcudart  -lcublas  -lcurand   
   ```
1. Create a conda environment
   ```
   conda  create  -y  –name  YoloSeqNMS  python=3.7
   ```
1. For executing the Makefile, set the path of the main folder in the terminal and type `make`. 
1. The following libraries need to be installed for being able to import them to the codes. This can be done writing the below commands in the terminal.
   - Numpy: `pip install numpy`
   - OpenCv `conda install -c conda-forge opencv`
   - Matplotlib: `pip install matplotlib`
   - Spicy: `pip install spicy`
   - Tensorflow: `pip install tensorflow`
   - Tensorflow Object Detection API: `pip install tensorflow-object-detection-api`
   - Imageio: `pip install imageio`
1. In the terminal write the following commands to set correctly the paths
   ```
   export PATH=/usr/local/cuda-10.1/bin${PATH:+:${PATH}}
   export LDLIBRARYPATH=$LDLIBRARYPATH:/usr/local/cuda-10.1/lib64
   export LIBRARYPATH=$LIBRARYPATH:/usr/local/cuda-10.1/lib64   
   ```
1. Set the path of the terminal in the video folder and type `python video2img.py -i input.mp4`. `Input.mp4` is the name of the video you want to use, which must be placed        in the video folder. In the video folder we have placed some videos that we have used which correspond to the five first classes of the UCF101 dataset. With this line you      will obtain every frame of the input video. 
1. Obtain a list with every frame typing `python get\_pkllist.py`
1. Return to the main folder and write the command `python yolo\_seqnms.py`. This outputs every input frame with the objects detected in `video/output`.
1. In the terminal enter to the video folder again and run `python img2video.py -i output`. This step is optional and you only perform it if you want to reconstruct the            video from the output images

## Reference

This project copies lots of code from [darknet](https://github.com/pjreddie/darknet) , [Seq-NMS](https://github.com/lrghust/Seq-NMS) and  [models](https://github.com/tensorflow/models).

This project aims to explain clearly the steps to download a Github repository, in this case [seq_nms_yolo](https://github.com/melodiepupu/seq_nms_yolo.git) and execute it. Besides, a code version for not applying the Seq-NMS algorithm has been created (seq_without_nms.py)
