# Correcting Image Orientation (Project)
</br>
The following are the main python files in this project:</br>

1. create_dataset.py </br>
This file uses the raw input dataset of 10,000 images and performs random rotations on them to obtain 4 categories of images with angles 0, 90, 180 and 270. </br>
To run:
   </t>   `python create_dataset.py --dataset indoor_cvpr/images --output indoor_cvpr/rotated_images ` </br>

2. extract_features.py </br>
This file works on the data obtained from above and performs **feature extraction** using the VGG16 network. The images are passed through the model and the output extracted features are stored in the .hdf5 file. </br>
To run: </br>
</t> ` python extract_features.py --dataset indoor_cvpr/rotated_images --output indoor_cvpr/hdf5/orientation_features.hdf5 ` </br>

3. train_model.py </br>
This model works on the extracted features obtained in the .hdf5 file, and runs a Logistic Regression model on them to classify. </br>
To run: </br>
</t> `python train_model.py --db indoor_cvpr/hdf5/orientation_features.hdf5 --model models/orientation.cpickle` </br>

4. orient_images.py </br>
Performs image orientation on 10 random images and the correct oriented images is output to the screen. </br>
To run: </br>
</t> `python orient_images.py --db indoor_cvpr/hdf5/orientation_features.hdf5 --dataset indoor_cvpr/rotated_images --model models/orientation.cpickle`

</br> </br>
This model obtained 93% accuracy. It’s worth mentioning here that we would not be able to obtain such a high prediction accuracy if VGG16 was truly rotation invariant. Instead, the (collective) filters inside VGG16 are able to recognize objects in various rotations – the individual filters themselves are not rotation invariant. If these filters truly were rotation invariant, then it would be impossible for us to determine image orientation due the fact that the extracted features would be near identical regardless of image orientation.



