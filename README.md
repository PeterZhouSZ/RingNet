# RingNet

![alt text](https://ringnet.is.tue.mpg.de/uploads/ckeditor/pictures/63/ringnet_teaset.png)

This is an official repository of the paper Learning to Regress 3D Face Shape and Expression from an Image without 3D Supervision. The project was formerly referred by RingNet. The codebase consists of the inference code, i.e. give an face image using this code one can generate a 3D mesh of a complete head with the face region. For further details on the method please refer to the following publication,

```
Learning to Regress 3D Face Shape and Expression from an Image without 3D Supervision
Soubhik Sanyal, Timo Bolkart, Haiwen Feng, Michael J. Black
CVPR 2019
```

More details on our NoW benchmark dataset, 3D face reconstruction challenge can be found in our [project page](https://ringnet.is.tue.mpg.de). A pdf prepreint is also available in the [project page](https://ringnet.is.tue.mpg.de).


## Installation

The code uses Python 2.7 and it is tested on Tensorflow gpu version 1.12.0.

### Setup RingNet Virtual Environment

```
virtualenv --no-site-packages <your_home_dir>/.virtualenvs/RingNet
source <your_home_dir>/.virtualenvs/RingNet/bin/activate
```
### Clone the project and install requirements

```
git clone https://github.com/soubhiksanyal/RingNet.git
cd RingNet
pip install -r requirements.txt
pip install opendr==0.77
mkdir model
```
Install mesh processing libraries from [MPI-IS/mesh](https://github.com/MPI-IS/mesh).

## Download models

* Downlaod pretrained RingNet weights from the [project website](https://ringnet.is.tue.mpg.de), downloads page. Copy this inside the **model** folder
* Download Flame model from [here](http://flame.is.tue.mpg.de/). Copy it inside the **flame_model** folder. This step is optional and only required if you want to use the output Flame parameters to play with the 3D mesh,i.e., to neutralize the pose and
expression and only using the shape as a template for other methods like [VOCA (Voice Operated Character Animation)](https://github.com/TimoBolkart/voca).

## Demo

RingNet requires a loose crop of the face in the image. Run the following command from the terminal to check the predictions of RingNet
```
python -m demo --img_path *.jpg --out_folder ./RingNet_output
```
Provide the image path and it will output the predictions in **./RingNet_output/images/**.

If you want the output mesh then run the following command
```
python -m demo --img_path *.jpg --out_folder ./RingNet_output --save_obj_file=True
```
It will save a *.obj file of the predicted mesh in **./RingNet_output/mesh/**.

If you want the predicted flame and camera parameters then run the following command
```
python -m demo --img_path *.jpg --out_folder ./RingNet_output --save_obj_file=True --save_flame_parameters=True
```
It will save a *.npy file of the predicted flame and camera parameters and in **./RingNet_output/params/**.

If you want to play with the 3D mesh, i.e. neutralize pose and expression of the 3D mesh to use it as a template in [VOCA (Voice Operated Character Animation)](https://github.com/TimoBolkart/voca), run the following command
```
python -m demo --img_path *.jpg --out_folder ./RingNet_output --save_obj_file=True --save_flame_parameters=True --neutralize_expression=True
```

## License

Free for non-commercial and scientific research purposes. By using this code, you acknowledge that you have read the license terms (https://ringnet.is.tue.mpg.de/license), understand them, and agree to be bound by them. If you do not agree with these terms and conditions, you must not use the code. For commercial use please check the website (https://ringnet.is.tue.mpg.de/license).

## Referencing RingNet

Please cite the following paper if you use the code directly or indirectly in your research/projects.
```
@inproceedings{RingNet:CVPR:2019,
title = {Learning to Regress 3D Face Shape and Expression from an Image without 3D Supervision},
author = {Sanyal, Soubhik and Bolkart, Timo and Feng, Haiwen and Black, Michael},
booktitle = {Proceedings IEEE Conf. on Computer Vision and Pattern Recognition (CVPR)},
month = jun,
year = {2019},
month_numeric = {6}
}
```

## Acknowledgement

* We thank Raffi Enficiaud and Ahmed Osman for pushing the release of psbody.mesh.
* We thank Benjamin Pellkofer and Jonathan Williams for helping with our [RingNet project website](https://ringnet.is.tue.mpg.de).
