# ros_peoplemodel

![Screenshot Debug Output](https://raw.githubusercontent.com/elggem/ros_slopp/master/images/vis_debug.png)

This is a collection of perception scripts primarily aimed at use in a  social robotics context. It combines various Deep Learning classifiers to build a model of people and their attributes. Working so far are modules for:

  - Detection of [68 Face landmarks](http://dlib.net/face_landmark_detection.py.html) to be used by classifiers based on Dlib 68 Landmark
  - Face ID using the [128D vector embedding from Dlib](https://github.com/davisking/dlib/blob/master/examples/dnn_face_recognition_ex.cpp), in addition with some simple clustering logic
  - Emotion recognition using [iCog Emopy](https://github.com/mitiku1/Emopy)
  - Eyes closed detection based on [iCog EyeState Detection](https://github.com/mitiku1/EyeStateDetection)

![Diagram Architecture](https://raw.githubusercontent.com/elggem/ros_slopp/master/images/arch.png)

In addition this repository contains some config files and experimental scripts for use of this package on Hanson Robotics humanoid robots.

## Roadmap

  - Integration with a classifier for speaking detection
  - Eventual integration with directional microphone to map what is spoken to individual faces.
  - Integration with OpenPose and various classifiers for
    - Body pose estimation (sitting, standing, waving, etc.)
    - Hand pose estimation (open palm, fist, etc.)
  - Integration wih Masked RCNN architectures to detect various categories of objects in the hands of people.
  - Better packaging and setup.py

## Dependencies

Most of the modules used depend on GPU accelerated Dlib or Tensorflow. In order to use it please do the following:

1. Install compatible NVIDIA drivers, [CUDA](https://developer.nvidia.com/cuda-90-download-archive) and [cuDNN](https://developer.nvidia.com/cudnn).
2. Install [Dlib](http://dlib.net/compile.html) from source using graphics acceleration support (after compilation and all dependencies are installed, follow the instructions for Compiling Dlib's Python Interface)
3. Install tensorflow-gpu.
4. Install additional dependencies `numpy`, `scikit-images`, `opencv`.

## Usage

In `launch/` there are several scripts to test the architecture:

  - `webcam_single.launch`: Can be used to launch the /camera node that will publish camera image.
  - `perception.launch`: Launches the entire architecture as described above.
  - In addition `scripts/vis_debug.py` will show a window for debugging output of the raw visual perception scripts.
  - In addition `scripts/model_debug.py` will show a window for debugging the output of model_people node, which fuses the various visual classifiers into a model of perceived faces.
