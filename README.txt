Optical Character Recognition using Neural Networks
By: Anant Agarwal (aa2387), Deekshith Belchappada (db786)

The code is based on Python 2.7, uses Anaconda, and Caffe.

Setting up Anaconda package:
i) Download the anaconda package based on your Operating System from -  https://docs.continuum.io/anaconda/install 
ii) Make sure you are downloading the "Python 2.7 version"
iii) Follow the instructions on the page, it should just require a few clicks to get it done.

Setting up Caffe:
i) Caffe installation requires a lot of intricate changes in setting it up the right way, and in installing the right set of dependencies. Describing all of these details here will make this README file very complicated.
ii) We list the blogpost which describes all the intricacies in setting up caffe in detail and was used by us extensively to setup our version. We feel that repeating the same content here in this file will be wasteful.
iii) Blogpost:  http://installing-caffe-the-right-way.wikidot.com/start
iv) Caffe official installation instructions: http://caffe.berkeleyvision.org/installation.html

How to run the code:
i) Code is contained in 2 python notebooks: Segmentation.ipynb, OCR.ipynb
ii) Jupyter python notebooks are part of Anaconda, and can be triggered by the following command in shell/terminal:
	jupyter notebook
iii) Once you have the notebook server running, open these notebooks.
iv) Both the notebooks are decribed below.

Segmentation.ipynb:
i) This file contains all the code related to segmentaion, the file temp/1-this_is_a_test-1.png is provided as a sample image to run this code.
ii) It will extract characters from this sample image and keep them in a sorted order.
iii) You can change the input image file to any other file, and the output will be generated in temp/segmentation_pdfimage/
iv) The code is heavily commented and provides explanation of all the chunks.
v) To run the code: in the top menu, go to Cell -> Run Cells.

OCR.ipynb:
This file contains following functionalities:
i)Data Generation:
This code block cell generates data using popular fonts.
The code has been explained with the help of comments in the file.
Output folder generated as a result of this code - "data_gen_new" has been included as well.

ii)Generate Training and Testing files:
This code block cell generates training_index.txt and test_index.txt
These files are used by caffe model for training and testing purposes.
They essentially contain the image file address and the image class label. Sample files created as a result of this code are present in the data_gen_new folder, and are named training_index.txt and test_index.txt

iii)Loading Caffe model in Python:
You need to train the caffe model first, and then provide its location to the python code along with its configuration file.
The process of training the model is described later in this file.

iv) Demo, Testing, Classification code: (You need to load the model first for any of this to run)
a)Demo code: We take one image per class and try to classify it using the model trained, the input folder has been provided, and can be found at "temp/0-9A-Za-z". The code also calculates Mean Reciprocal Rank using top 3 guesses.
b)Code for Testing the model: This one loads your test file, and uses the model to classify and calculate accuracy. A sample test file has been provided and can be found at "data_gen_new/test_index.txt"
c) Classify segmented images: This is essentially same as above, just that we are passing in the images generated as a result of character segmentation on a image. You can generate the inputs for this code piece by running the segmentation code from segmentation.ipynb 

Training the caffe Model:
We have two models - lenet (with 62 classes), alpha (referred as 'LeNet Modified' in report)
Caffe requires following 3 files:
Model File: temp/lenet.prototxt, temp/alpha.prototxt
Solver File: temp/lenet_solver.prototxt, temp/alpha_solver.prototxt
Deploy File: temp/lenet_deploy.prototxt, temp/alpha_deploy.prototxt
Details for each of these are mention in the report.
For training the following needs to be done:
i) Fix the paths in Model File for training_index.txt, test_index.txt
ii) See that the data(training image files) are located on the locations mentioned in the training and testing files.
iii) In the solver file, make sure the path to model file on line 2 is correct.
iv) In terminal/shell give the following command with desired solver file:
	caffe train -solver <solver file>
v) The model will start training, and a version of model will be stored after every few iterations.


All the details above, along with the report(it has additional details about caffe) should be sufficient in getting the code up and running. However, if there are any troubles, please feel free to reach out to any of us. (aa2387@cornell.edu, db786@cornell.edu)

Thanks!