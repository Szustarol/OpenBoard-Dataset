# OpenBoard-Dataset
OpenBoard Dataset is a dataset of chess diagram photos with labels for the board area and each figure.
The dataset is separated into two parts, as usually is the task of detecting chess positions from photos.
I also provide saved Tensorflow models trained with this dataset, along with software that can run them in [the OpenBoard repository](https://github.com/Szustarol).

### The raw version of the dataset (the `source_diagrams` directory)
The dataset was gathered manually, by taking photos of chess positions as seen on an LCD display, from twitch streams, lichess.org and chess.com websites, with various board visual settings.
To improve labeling speed, each photo is labeled the following way:
1. A polygon surrounding the board area is created. In theory the polygon can consist of any number of vertices, however in this case I have provided, that every polygon is a quadrilateral. 
2. Each figure present on the board is assigned a keypoint, that is a point that lies inside the square on which the figure is located. 

All of the data has been labeled in label studio, but to give it a more readable format, I have converted it to a more accessible `labels.json`, which contain all the information required to do classification.
Except for the figure keypoints, each photo for which it applies, contains keypoints for the A0 square, and the H8 square, so board orientation can be detected.

The `source_diagrams` directory also contains a `rotation_data.csv` file with metadata concerning image rotation.

### The segmentation dataset (the `segmentation_data` directory)
For segmentation training, I have extracted polygons from the JSON file and made the segmentation sub-dataset readily available, so no JSON parsing is required. Please keep in mind that the images have NOT been unrotated.

### The classification dataset (the `classification_data` directory)
For classification, the classification data is also provided, with each square extracted from the corresponding image, aligned and resized to am 64x64 RGB image. Please bear in mind, that classes are imbalanced, as empty tiles correspond to most of the samples. Each image's label is given by it's name, which is of the following format: `<image_id>_class_<class index>.png`. This directory also contains a `class_map.json` file, which maps the class name to class id (eg. `"White pawn", "2"`).


## Pretrained models and model training examples
As mentioned, I provide all the source code required to train segmentation and classification models, along with perspective correction and extracting squares from images in [the OpenBoard repository](https://github.com/Szustarol).
