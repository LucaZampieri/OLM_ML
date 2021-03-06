*** README for the 2nd Machine Learning Project, Road Segmentation --- Team: "..no party!!"

Licence GPL3.0

********************************
To obtain the best submission:
- Install tensorflow 1.3.0
- Install panda, scikit-learn, opencv2, Pillow (PIL) and numpy
- Run the following commands:
      cd unet_cnn/
      python3 run.py
********************************

The .zip folder is organized according to the following structure:
- "Image_processing_KNN/": folder to run a prediction model based on KNN feature extraction with “Image processing”;
- "unet_cnn/": folder to run prediction model based on CNN (convolutional neural network). Code used for the final submission.


noparty.zip
  |— unet_cnn/
  |   |—- data_processing.ipynb
  |   |—- layers.py
  |   |—- extract_data.py
  |   |—- image_util.py
  |   |—- mask_to_submission.py
  |   |—- padding.py
  |   |—- postprocessing.py
  |   |—- run.py          --> FILE TO RUN TO HAVE THE UNET SUBMISSION
  |   |—- unet.py
  |   |—- util.py
  |   |—- output/
  |   |—- prediction/
  |   |—- unet_trained/
  |   |—- test_set_images/
  |   |—- training/
  |— Image_processing_KNN/
  |   |—- GMM+KNN.ipynb   --> FILE TO RUN TO HAVE THE GMM+kNN SUBMISSION
  |   |—- KNN.ipnyb       --> FILE TO RUN TO HAVE THE KNN SUBMISSION
  |   |—- Image_processing_pre_proc.ipynb
  |   |—- feature_extraction.py
  |   |-- feature_increase.py
  |   |—- fill_the_gaps.py
  |   |—- GMM_functions.py
  |   |—- helper_functions.py
  |   |—- mask_to_submission.py
  |   |—- image_predicted/
  |   |—- test_set_images/
  |   |—- training/

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

INSIDE "unet_cnn/" :    subfolders: "output", "prediction", "unet_trained", "test_set_images", "training";

To obtain the submissions corresponding to the two methods used, run the IPython notebook KNN.ipynb and GNN+KNN.ipynb

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

EXTERNAL LIBRARIES USED TO INSTALL BEFORE RUNNING:
Tensorflow, panda, scikit-learn, opencv2, Pillow (PIL), numpy

SUBFOLDERS:
-  “test_set_images”: it contains the RGB images for test data set
-  “training”: it contains the RGB images for training set as well as the groundtruth images
-  "output": it contains the prediction images and the submission file
-  "unet_trained": it contains the models used by tensorflow, i.e. the values of the different parameters of the neural network

FILES:

1) data_processing.ipynb: IPython notebook explaining some preprocessing steps
(not necessary to get the submission, present just to have further explanation on our work)

2) layers.py: used to build the neural network features, variables and layers,
and to compute the different evaluation metrics (cross entropy, F score)

3) extract_data.py: used to extract the images (original training set, grountruth
images of the training set, and testing set)

4) image_util.py: used to handle the data and add it in memory dynamically to save some RAM

5) mask_to_submission.py: functions used to make the submission to Kaggle.

6) padding.py: functions used to extend an image with mirror boundary conditions.

7) postprocessing.py: functions used to postprocess the predicted labels for each image.

8) run.py: MAIN FILE run.py where the implementation and run of the U-net is done.
- Setting of the different parameters: here, the user can set any parameter he wants to change the unet/training set/testing set
- Creation of the U-net
- Training of the U-net
- Computing the predictions on the training set
- Testing: computing the predictions on the testing set

9) unet.py: contains all necessary functions to build and train a neural network
following the U-net architecture.

10) util.py: contains all helper functions to perform the road segmentation
algorithm with a U-net.

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

INSIDE “Image_processing_KNN/” :    subfolders: “image_predicted”, “test_set_images”, ”training”;

To obtain the submissions corresponding to the two methods used, run the IPython notebook KNN.ipynb and GNN+KNN.ipynb

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

EXTERNAL LIBRARIES USED TO INSTALL BEFORE RUNNING:
Panda, scikit-learn, opencv2, numpy

SUBFOLDERS:
- “image_predicted”: it contains the predicted groundtruth for test;
-  “test_set_images”: it contains the RGB images for test data set
-  “training” : it contains the RGB images for training set as well as the groundtruth images

FILES:

1) KNN.ipnyb: contains the code to run the KNN. The structure of the code is the following:
		   - Load the data of the training and testing set
		   - Extract the labels for the training set with the groundtruths
                   - Extract the features for training and testing set
                   - Run the cross validation on KNN to determine the degree of the polynomial matrix and the best number of neighbors to consider;
		   - With the optimal parameters, fit the model on the training set;
		   - Make the prediction
		   - Save the label of each patch [1,0] as black and white picture and save this predicted images in “image_predicted”;
                   - Post Processing: fill_the_gaps; the images are saved in the main folder;
                   - Create the submission on this image;
                   IMPORTANT !!! : for the submission be aware that no file .png is present inside the folder except the ones
										     generated by the code



2) GMM+KNN.ipynb: contains the code to run KNN with GMM. The structure of the code is the following:
	           - Load the data of the training and testing set
                   - Extract the features for training and testing set
		   - Extract the labels for the training set with the groundtruths
                   - Run the cross validation to determine the degree of the polynomial matrix, the best number of neighbors to consider and the best number of clusters in which the image has to be segmented;
	           - With the optimal number of clusters, enhance the training set with GMM functions ( see GMM_function.py )
		   - With the optimal parameters fit the model on the training set;
		   - Make the prediction;
		   - Save the label of each patch [1,0] as black and white images (images saved in image_predicted/);
                   - Post Processing: fill_the_gaps; the images are saved in the main folder;
                   - Create the submission on this image;
                   IMPORTANT !!! : for the submission be aware that no file .png is present inside the folder except the ones
										      generated by the code


3) Image_processing_pre_proc.ipynb: it contains the pre-processing functions (image processing based) used for features extraction.
   Used to find informative features that can be used in our fit model (creation of the features training set).


4) feature_extraction.py: Creation of the training set in reference to the considerations made in “Image_processing_pre_proc.ipynb”.
        - create_train_table (n_rows,n_features):        Create a new table for train
				- add_feature(train_tx,new_column_feature):      Add a new column to the train matrix
				- extract_features(img) :                        Extract 6-dimensional features consisting of average RGB color as well as variance
				- extract_mean_RGB(img):                         Extract mean RGB of the patch
				- extract_variance_RGB(img):                     Extract variance RGB of the patch
  			- get_spectrum(img_patches):                     Calculate the fft of the image
				- get_spectrum_grey(img_patches):                Calculate the fft of the grey scal patch
				- extract_mean_spectrum_grey(spectrum):          Extract the mean of the spectrum  (grey scale patch)
				- extract_variance_spectrum_grey(spectrum):       Extract the variance of the spectrum (grey scale patch)
				- extract_mean_spectrum(spectrum):                Extract the mean of the spectrum  (RGB patch)
				- extract_variance_spectrum(spectrum):            Extract the variance of the spectrum  (RGB patch)
				- extract_new_features(img_patches,n_features,…):     Extract features for a given set of patches according to the input parameters
				- extract_img_features(filename,n_features..) :       Extract features for a given image


5) feature_increase.py: Functions to increase the training model once the features have been fixed;
			   -  add_ones(tx):                                        Add column of ones to the dataset tx
			   -  build_poly(x, degree):                               Returns the polynomial basis functions for input data x, for j=2 up to j=degree.


6) GMM_functions.py: Functions used for GMM (unsupervised method) to enhance our dataset:
			   - label_to_img_GMM(imgwidth, imgheight, w, h, labels):    From a vector of labels (label in this case means the class of a specific cluster) this function returns a segmented image where each patch is colored according to the class;
			   - build_new_X(Z_GMM,X,n_components):                      Adding the features obtained with GMM to X train matrix.
										    METHOD for features extraction:
				 - Given in input the X matrix and Z_GMM, a vector containing the label of the clusters (Z_GMM and X have the same length)
 											do the following :
					  - being S the set of ALL the patches which belong to the same label k , calculate the mean R,G,B and the variance R,G,B
										       for S and add these values as feature of the patches of S.
				    - do the same of the same for “mean grey” and “variance grey”
					  - for the mean_grey add also the difference between “mean grey” of the set S and the mean grey of the single patch;


7) helper_functions.py: it contains the functions useful for elaborate the images and visualize the results in the notebook
			-load_image(infilename)
			-img_float_to_uint8(img)
			-concatenate_images(img, gt_img)
			-img_crop(im, w, h)
			-RGB_to_grey(image): 					    Transform the RGB image into grey scale
			-value_to_class(v)
			-label_to_img(imgwidth, imgheight, w, h, labels)
			-make_img_overlay(img, predicted_img)
			-binary_to_uint8(img)


8) mask_to_submission.py : 							functions to create the submission given the images

9) fill_the_gaps.py : post processing function , it corrects the image filling the holes if present
