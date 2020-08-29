Keras implementation of DilatedNet for semantic segmentation
============================================================

The code has been tested on Tensorflow 1.3, Keras 1.2, and Python 3.6.

Install dependencies and run:

```
pip install -r requirements.txt
# For GPU support
pip install tensorflow-gpu==1.3.0

python predict.py --weights_path conversion/converted/dilation8_pascal_voc.npy
```

The output image will be under `images/cat_seg.png`.


Converting the original Caffe model
-----------------------------------

Follow the instructions in the `conversion` folder to convert the weights to the TensorFlow
format that can be used by Keras.


Training
--------

Download the *Augmented Pascal VOC* dataset
(http://home.bharathh.info/pubs/codes/SBD/download.html):

This will create a `benchmark_RELEASE` directory in the root of the repo.
Use the `convert_masks.py` script to convert the provided masks in *.mat* format to RGB pngs:

    python convert_masks.py \
        --in-dir benchmark_RELEASE/dataset/cls \
        --out-dir benchmark_RELEASE/dataset/pngs

Start training:

    python train.py --batch-size 2

Model checkpoints are saved under `trained/`, and can be used with the `predict.py` script for testing.

This will create a model that will be saved in the desired file structure.

Prediction using the trained model
----------------------------------

The trained model is being placed in the file structure named as "model.h5"

Using this model, run the below command by placing the image in the "images" folder.

python predict.py --weights_path model.h5 --input_path ./images/"your filename with extention"

After running this code, the segmentation image will be generated.

Creating the portrait Mode:
----------------------------

Once the segmented image is created, use the segmented image and original image using which the portrait mode can be obtained

Use the Blur.ipynb file in the file structure available.