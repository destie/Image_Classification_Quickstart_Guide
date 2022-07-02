# Image_Classification_Quickstart_Guide
Quick walkthrough of how to set up a classification model in tensorflow for my students in the Loew lab (And elsewhere - should you find this helpful!). 

The following guide is intended for students in the Loew lab (And others who find this useful) to be able to quickly put together a model. This hopefully provides a useful framework and explanation for why things are the way they are in this model. 


**Creating_Training_and_Testing_Datasets**
This creates a training and testing set from one directory

**Model_Compilation_and_Training**
This builds your directory

**Validation**
This takes your model file and validates it on a new holdout/ validation set (or single image)

Remember before you start using this code, to first assess the data. What is your outcome variable? What does your data look like? Is there a corresponding CSV with metadata? A good first step with images is just to straight up look at the images and see what's in there and if you need to do any pre-processing. 

For example you can do the following:
#Sample Code to display the image using CV2, this code loads the package, loads in the file, then displays the image
import cv2
image = cv2.imread(yourdirectoryhere)
plt.imshow(image)

#Sample Code to display DICOM this code loads the package, loads the file, converts it appropriately, then displays the file
import pydicom as dicom
import PIL as Image
ds = dicom.dcmread(yourdirectoryhere)
                shape = ds.pixel_array
img = Image.fromarray(image_2d_scaled)

Next you need to prepare your data - usually this is done using a training and testing split of your directory. This is done because you want to see how the model will perform on new data. So you take some percentage (say 80%) of your old data to "train the model," and use the remaining 20% to see how it performs. The create training and testing file above helps you do this using tensorflow. 

Next you pick your model (in the above example we pick a ResNet) and set up the layers so that it will "learn" your data and try to make inferences from it. In the above file (Model Compilation and Training) we use a "Transfer learning" process where we remove the last layer of an already trained network and update it with new data to train our ResNet. 

Finally you validate the model. This can be done in a variety of ways. If you have a separate holdout dataset you can simply run your model and evaluate it on the new data. You can also use what's called "Cross-validation" where you run multiple 80/20 testing splits on the data to see how the model performs when trained and tested on different segments of the data. This is all described in the file above! To display the final results of the model we can use what's called an "ROC" curve, AUC, and loss metrics in addition to simply looking at accuracy. 

Finally remmeber to iteratively update the model depending on the performance. For example one can add more layers or Epochs to increase the training time and hopeful theoretical performance! 

And that's it - happy modeling! Please do feel free to get in touch with any questions. 
