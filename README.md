# manini

[![License BSD-3](https://img.shields.io/pypi/l/manini.svg?color=green)](https://github.com/hereariim/manini/raw/main/LICENSE)
[![PyPI](https://img.shields.io/pypi/v/manini.svg?color=green)](https://pypi.org/project/manini)
[![Python Version](https://img.shields.io/pypi/pyversions/manini.svg?color=green)](https://python.org)
[![tests](https://github.com/hereariim/manini/workflows/tests/badge.svg)](https://github.com/hereariim/manini/actions)
[![codecov](https://codecov.io/gh/hereariim/manini/branch/main/graph/badge.svg)](https://codecov.io/gh/hereariim/manini)
[![napari hub](https://img.shields.io/endpoint?url=https://api.napari-hub.org/shields/manini)](https://napari-hub.org/plugins/manini)

Manini is thought as a tool to boost the collaborative contribution of end-users to the assessment of deep learning model during their testing phase.
It is a user-Friendly plugin that enables to manually correct the result of an inference of deep learning model by an end-user. The plugin covers the following informational tasks: segmentation, classification and object detection.

----------------------------------

This plugin was written by Herearii Metuarea, student intern at LARIS (French laboratory located in Angers, France) in Imhorphen, french scientific team lead by David Rousseau (Full professor). This plugin was designed in the context of the european project INVITE and PHENET.

![Screenshot from 2023-11-13 00-12-18](https://github.com/hereariim/manini/assets/93375163/dbee7211-2982-4a0b-bf58-91bc788ec22e)

The Manini plugin for napari a tool to perform image inference from a pre-trained model (tensorflow .h5) and then annotate the resulting images with the tools provided by napari. Its development is ongoing.

![Screencast from 24-01-2023 14 00 51](https://user-images.githubusercontent.com/93375163/214298805-8405a923-5952-458c-8542-7c78887479ab.gif)

----------------------------------

This [napari] plugin was generated with [Cookiecutter] using [@napari]'s [cookiecutter-napari-plugin] template.

<!--
Don't miss the full getting started guide to set up your new package:
https://github.com/napari/cookiecutter-napari-plugin#getting-started

and review the napari docs for plugin developers:
https://napari.org/stable/plugins/index.html!

-->

## Installation

You can install `manini` via [pip]:

    pip install manini

To install latest development version :

    pip install git+https://github.com/hereariim/manini.git


## Description

This plugin is a tool to perform 2D image inference. The inference is open to the model for image segmentation (binary or multiclass), image classification and object detection.
This tool is compatible with tensorflow h5 models. In this format, the h5 file must contain all the elements of the model (architecture, weights, etc).

### Image segmentation

This tool allows image inference from a segmentation model.

#### Input

The user must deposit two items (+1 optional item).

- A compressed file (.zip) containing the images in RGB

```
.
└── input.zip
    ├── im_1.JPG
    ├── im_2.JPG 
    ├── im_3.JPG
    ...
    └── im_n.JPG
```

- A tensorflow h5 file (.h5) which is the segmentation model
- A text file (.txt) containing the names of the classes (optional)

The Ok button is used to validate the imported elements. The Run button is used to launch the segmentation.

#### Processing

Once the image inference is complete, the plugin returns a drop-down menu showing a list of RGB images contained in the compressed file. When the user clicks on an image displayed in this list, one items appear in the napari window:

- A menu that presents a list of the classes given as input

![cpe](https://user-images.githubusercontent.com/93375163/214246685-e86a9f62-bb27-44b5-92eb-86ef5aa2c663.png)

A widget also appears to the right of the window. This is a list of the classes in the model with their associated colours. In this tool, the number of classes is limited to 255.

The user can make annotations on the layer label. For example, the user can correct mispredicted pixels by annotating them with a brush or an eraser.

#### Output

The Save button allows you to obtain a compressed image file. This file contains folders containing the RGB images and their greyscale mask.

### Image classification

This tool performs image inference from an image classification model.

#### Input

This tool offers three mandatory inputs:

- A compressed file (.zip) containing the RGB images

```
.
└── input.zip
    ├── im_1.JPG
    ├── im_2.JPG 
    ├── im_3.JPG
    ...
    └── im_n.JPG
```

- A tensorflow h5 (.h5) file which is the image classification model
- A text file (.txt) containing the class names

The Ok button is used to validate the imported elements. The Run button is used to launch the classification.

#### Processing

Once the image inference is complete, the plugin returns one elements :

- an table containing the predicted class for each image.

![cpe2](https://user-images.githubusercontent.com/93375163/214252875-c8e59773-4c3d-4582-b8db-67c59ab01975.png)

The user can change the predicted class by selecting a class displayed in the associated drop-down menu for an image.

#### Output

The Save button allows you to obtain a csv file. This file is the table on which the user had made his modifications.

### Detection

This tool performs image inference from an yolo object detection model.

#### Input

The user must deposit two items (+1 optional item).

- A compressed file (.zip) containing the images in RGB

```
.
└── input.zip
    ├── im_1.JPG
    ├── im_2.JPG 
    ├── im_3.JPG
    ...
    └── im_n.JPG
```

- A tensorflow h5 file (.h5) which is the detection model
- A text file (.txt) containing the names of the classes (optional)

The Ok button is used to validate the imported elements. The Run button is used to launch the segmentation.

#### Processing

When the prediction of bounding box coordinates is complete for each image, the plugin returns one elements:

- A menu that presents a list of the classes given as input

![Screenshot from 2023-01-24 10-33-07](https://user-images.githubusercontent.com/93375163/214257222-945ed096-49dd-4b91-aa2a-df4c43a30372.png)

The window displays the bounding boxes and the RGB image. The bounding box coordinates are taken from the json file which is an output file of the darknet detector test command. The user can update these coordinates by deleting or adding one or more bounding boxes. From the list of classes, the user can quickly add a bounding box to the image.

#### Output

The Save button allows you to obtain a json file. This file contains for each image, the bounding box coordinates and the class for each detected object.

## License

Distributed under the terms of the [BSD-3] license,
"manini" is free and open source software

## Issues

If you encounter any problems, please [file an issue] along with a detailed description.

[napari]: https://github.com/napari/napari
[Cookiecutter]: https://github.com/audreyr/cookiecutter
[@napari]: https://github.com/napari
[MIT]: http://opensource.org/licenses/MIT
[BSD-3]: http://opensource.org/licenses/BSD-3-Clause
[GNU GPL v3.0]: http://www.gnu.org/licenses/gpl-3.0.txt
[GNU LGPL v3.0]: http://www.gnu.org/licenses/lgpl-3.0.txt
[Apache Software License 2.0]: http://www.apache.org/licenses/LICENSE-2.0
[Mozilla Public License 2.0]: https://www.mozilla.org/media/MPL/2.0/index.txt
[cookiecutter-napari-plugin]: https://github.com/napari/cookiecutter-napari-plugin

[file an issue]: https://github.com/hereariim/manini/issues

[napari]: https://github.com/napari/napari
[tox]: https://tox.readthedocs.io/en/latest/
[pip]: https://pypi.org/project/pip/
[PyPI]: https://pypi.org/
