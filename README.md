# Brown Tail Moth Investigation - DavisAI

## A fully functional implementation of the Pix2Pix GAN used to conduct image-to-image translation between the RGB and NIR color-spaces

## Table of Contents
- [Project Goals](#project-goals)
- [Results](#results)
- [Getting Started](#getting-started)
- [Contents](#contents)
	- [Coordinate_Mapping](#coordinate_mapping)
	- [Data](#data)
		- [SEN12MS](#sen12ms)
		- [Drone_Images](#drone_images)
  - [Pix2Pix](#pix2pix)
    - [GAN Creation Files](#GAN_creation_files)
    - [Image Storage Folders](#Image_Storage_Folders)
    - [GAN Model Storage Files](#GAN_Model_Storage_Files)
	- [combine_images.py](#combine_images)
- [License](#license)

## Project Goal <a name="project-goals"></a>
The goal of this project was to develop a computer vision pipeline to detect Brown Tail Moth infestations using drone footage by performing image processing, data analysis, training an AI model, and mapping the detected infestations. To do so, we attempt to conduct RGB to NIR image-to-image translation using a Pix2Pix GAN model with the goal of making BTM overwintering pods more visible to a object detection AI model.

## Results <a name="results"></a>
- Insert image of results (before and after) once Pix2Pix is uploaded

The above figures show the generator does not do a very good job at simulating the NIR channel using the drone captured images. Possible reasons that the model does not perform well are 1) the data it was trained is too dissimilar from the data it is being used for and 2) the model produces images in the RGB colorspace instead of in grayscale

## Getting Started <a name="getting-started"></a>
1. Download the Pix2Pix folder
2. Rename one of 3 'dataset_xyz.py' files to 'dataset.py' depending on what dataset you want to work with
   - ex. if using SEN12MS dataset, rename 'dataset_SEN12MS.py' --> 'dataset.py'
4. Rename one of 3 dataset_xyz folders to 'dataset' depending on what dataset you want to work with
   - ex. if using SEN12MS dataset, rename 'dataset_SEN12MS' --> 'dataset'
6. Change the names of the files that the generator and discriminator models get saved to
   - i.e. in 'config.py' change 'CHECKPOINT_DISC = ' and 'CHECKPOINT_GEN = ' to names of your choice
8. Run 'pix2pix.ipynb' and wait!

## Contents <a name="contents"></a>

### Coordinate_Mapping <a name="coordinate_mapping"></a>
- insert image of coordinate mapping once it is uploaded
Contains the python scripts in order to extract the metadata (latitude, longitude,  etc.) from the images in a Mac folder, and maps that coordinates of the manually captured data vs. the coordinates of the drone captured. As we can see, there is a surprising lack of overlap between the two datasets making them difficult to use in conjunction with one another.

### Data <a name="data"></a>
Contains the datasets used to train (SEN12MS) and test (Drone_Images) the GAN

#### SEN12MS <a name="sen12ms"></a>
A folder that contains the RGB-NIR paired images in two versions: 1) the raw, separated images, and 2) the combined images where the 2 separate images are combined side-by-side into a single image. The SEN12MS dataset is an open source dataset of over 180,000 RGB-NIR paired images.
#### Drone_Images <a name="drone_images"></a>
A folder that contains over 5000 aerial drone images of trees that either both infested with BTMs or healthy.


## Pix2Pix <a name="pix2pix"></a>
This is the only folder needed in order to run train/validate/test the GAN. In this folder we have...

<ins>**GAN Creation Files**</ins> <a name="GAN_creation_files"></a>

*Must change one of 3 'dataset_xyz.py' files to 'dataset.py' depending on what dataset you want to work with (if using SEN12MS dataset, rename 'dataset_SEN12MS.py' --> 'dataset.py')*
- config.py
- dataset_anime.py
- dataset_maps.py
- dataset_SEN12MS.py
- discriminator_model.py
- generator_model.py
- train.py
- utils.py

<ins>**Image Storage Folders**</ins> <a name="Image_Storage_Folders"></a>

*Must change one of 3 dataset_xyz folders to 'dataset' depending on what dataset you want to work with (if using SEN12MS dataset, rename 'dataset_SEN12MS' --> 'dataset')*

- data_anime
- data_maps
- data_SEN12MS
- evaluation
- results
- saved_images
- test_drone_images

<ins>**GAN Model Storage Files**</ins> <a name="GAN_Model_Storage_Files"></a>

*Change the output file name in 'config.py'; output files will build on top of previous training if name is not changed*
- disc_SEN12MS_april30.pth.tar
- disc.pth.tar
- gen_SEN12MS_april30.pth.tar
- gen.pth.tar

## combine_images.py <a name="combine_images"></a>
A helper method that combines two images, one from training set folder and one from a validation set folder, into one image by placing them side by side. The purpose of this is to put images into the correct format for the Pix2Pix GAN. The images in the train and validation folders must have the same order for them to combined together.

## License <a name="license"></a>
