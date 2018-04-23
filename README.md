## iGAN: Interactive Image Generation via Generative Adversarial Networks
[[Project]](http://www.eecs.berkeley.edu/~junyanz/projects/gvm/) [[Youtube]](https://youtu.be/9c4z6YsBGQ0)   [[Paper]](https://arxiv.org/pdf/1609.03552v2.pdf)  
Forked project from a research prototype developed by UC Berkeley and Adobe CTL.  

## Getting started
* Install the python libraries. (See `Requirements`).
* Download the code from GitHub:
```bash
git clone https://github.com/ChatSam/GAN3D_src
cd GAN3D_src
```
* Download the model. (See `Model Zoo` for details):
``` bash
bash ./models/scripts/download_dcgan_model.sh shoes_64
```

* Run the python script:
``` bash
THEANO_FLAGS='device=gpu0, floatX=float32, nvcc.fastmath=True' python iGAN_main.py --model_name shoes_64
```

## Requirements
The code is written in Python2 and requires the following 3rd party libraries:
* numpy
* [OpenCV](http://opencv.org/)
```bash
sudo apt-get install python-opencv
```
* [Theano](https://github.com/Theano/Theano)
```bash
sudo pip install --upgrade --no-deps git+git://github.com/Theano/Theano.git
```
* [PyQt4](https://wiki.python.org/moin/PyQt4): more details on Qt installation can be found [here](http://www.saltycrane.com/blog/2008/01/how-to-install-pyqt4-on-ubuntu-linux/)
```bash
sudo apt-get install python-qt4
```
* [Qdarkstyle](https://github.com/ColinDuquesnoy/QDarkStyleSheet)
```bash
sudo pip install qdarkstyle
```
* [dominate](https://github.com/Knio/dominate)
```bash
sudo pip install dominate
```
* GPU + CUDA + cuDNN:
The code is tested on GTX Titan X + CUDA 7.5 + cuDNN 5.  Here are the tutorials on how to install [CUDA](http://www.r-tutor.com/gpu-computing/cuda-installation/cuda7.5-ubuntu) and [cuDNN](http://askubuntu.com/questions/767269/how-can-i-install-cudnn-on-ubuntu-16-04). A decent GPU is required to run the system at real-time. [**Warning**] If you run the program on a gpu server, you need to use a remote desktop software (e.g. VNC), which may introduce display artifacts and latency problem.

## Python3
For `Python3` users, you need to replace `pip` with `pip3`:
* PyQt4 with Python3:
``` bash
sudo apt-get install python3-pyqt4
```
* OpenCV3 with Python3: see the installation [instruction](http://www.pyimagesearch.com/2015/07/20/install-opencv-3-0-and-python-3-4-on-ubuntu/).


## Interface:
See [[Youtube]](https://youtu.be/9c4z6YsBGQ0?t=2m18s) at 2:18s for the interactive image generation demos.  

<img src='pics/ui_intro.jpg' width=800>  

#### Layout
* Drawing Pad: This is the main window of our interface. A user can apply different edits via our brush tools and the system will display the generated image. Check/Uncheck `Edits` button to display/hide user edits.  
* Candidate Results: a display showing thumbnails of all the candidate results (e.g. different modes) that fits the user edits. A user can click a mode (highlighted by a green rectangle), and the drawing pad will show this result.
* Brush Tools:  `Coloring Brush` for changing the color of a specific region; `Sketching brush` for outlining the shape. `Warping brush` for modifying the shape more explicitly.
* Slider Bar: drag the slider bar to explore the interpolation sequence between the initial result (i.e. random generated image) and the current result (e.g. image that satisfies the user edits).
* Control Panel: `Play`: play the interpolation sequence; `Fix`: use the current result as additional constraints for further editing  `Restart`: restart the system; `Save`: save the result to a webpage. `Edits`: Check the box if you would like to show the edits on top of the generated image.


#### User interaction
* `Coloring Brush`:  right click to select a color; hold left click to paint; scroll the mouse wheel to adjust the width of the brush.
* `Sketching Brush`: hold left click to sketch the shape.
* `Warping Brush`: We recommend you first use coloring and sketching before the warping brush. Right click to select a square region; hold left click to drag the region; scroll the mouse wheel to adjust the size of the square region.
* Shortcuts: P for `Play`, F for `Fix`, R for `Restart`; S for `Save`; E for `Edits`; Q for quitting the program.
* Tooltips: when you move the cursor over a button , the system will display the tooltip of the button.



## Command line arguments:
Type `python iGAN_main.py --help` for a complete list of the arguments. Here we discuss some important arguments:
* `--model_name`: the name of the model (e.g. outdoor_64, shoes_64, etc.)
* `--model_type`: currently only supports dcgan_theano.
* `--model_file`: the file that stores the generative model; If not specified, `model_file='./models/%s.%s' % (model_name, model_type)`
* `--top_k`: the number of the candidate results being displayed
* `--average`: show average image in the main window. Inspired by [AverageExplorer](https://people.eecs.berkeley.edu/~junyanz/projects/averageExplorer/), average image is a weighted average of multiple generated results, with the weights reflecting user-indicated importance. You can switch between average mode and normal mode by press `A`.
* `--shadow`: We build a sketching assistance system for guiding the freeform drawing of objects inspired by [ShadowDraw](http://vision.cs.utexas.edu/projects/shadowdraw/shadowdraw.html)
To use the interface, download the model `hed_shoes_64` and run the following script
```bash
THEANO_FLAGS='device=gpu0, floatX=float32, nvcc.fastmath=True' python iGAN_main.py --model_name hed_shoes_64 --shadow --average
```

## Dataset and Training
See more details [here](./train_dcgan/README.md)
