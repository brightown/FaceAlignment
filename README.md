###Face Alignment
This program is a C++ reimplementation of algorithms in paper "Face Alignment by Explicit Regression"
by Cao et al. This program can be used to train models for detecting facial keypoints, and it is 
extremely fast both in training and testing. 

Please go to folder `FaceAlignment` to see the source files.

###Usage
To compile the program(OpenCV required):
```
// Go to folder FaceAlignment
cmake .
make TrainDemo.out
make TestDemo.out
```
To train a new model:
``` C++
ShapeRegressor regressor;
regressor.Train(images,ground_truth_shapes,bounding_box,first_level_num,second_level_num,
                    candidate_pixel_num,fern_pixel_num,initial_number);
regressor.Save("./data/model.txt");
```
To predict a new input:
``` C++
ShapeRegressor regressor;
regressor.load("./data/model_cofw_2.txt");
regressor.Predict(test_images[index],bounding_box[index],initial_number);
```
For details, please see `TrainDemo.cpp` and `TestDemo.cpp`.

###Dataset
A public dataset is provided [here](https://drive.google.com/file/d/0B0tUTCaZBkccUU5hVkNJTFB0VDQ/edit?usp=sharing). The dataset contains 1345 training images, 507 testing images, and each image has 29 landmarks. You can change the path
in `TrainDemo.cpp` and `TestDemo.cpp` to train new models.

###Model
I have prepared a model trained by me on COFW dataset, and you can access it [here](https://drive.google.com/file/d/0B0tUTCaZBkccOGZTcjJNcDMwa28/edit?usp=sharing).

###FAQ
1. How to get the bounding box of an input face image?

You can get the bounding box with a face detector, which has been implemented in OpenCV. However, do remember that, if you use the model provided by me, you must provide a bounding box of similar measure with the training data. Otherwise, the result will be poor. If the bounding box of training data is very small, but you provide a very big bounding box for testing data, it is certain that you will get a poor result. Here the same measure doesn't mean that they have to be the same size, but they have to be taken using the same standard, for example, the ratio between bounding box width and the two-eye distance should be the same. 

###Contact
If you have any question about the code, I prefer that you create an **issue** on GitHub rather than send me emails directly, so that others can also refer to it when they have problems. I will respond to it as soon as possible.

###Sample Results
![Sample Results](https://dl.dropboxusercontent.com/u/47747425/Photo/point1.png)


###Reference papers:
[Face Alignment by Explicit Shape Regression](http://research.microsoft.com/pubs/192097/cvpr12_facealignment.pdf)




