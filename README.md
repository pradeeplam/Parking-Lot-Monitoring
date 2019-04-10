# Parking-Lot-Monitoring
Using Yolo to monitor a parking lot and keep track of when cars arrive and depart

Requires yolo-coco diretory in order to work. Please download and place in local directory.
Folder contains coco.names, yolov3.cfg, and yolov3.weights.

Analysis of Solution:

My intent was to provide a light-weight and reasonably accurate solution to the problem at hand. 
And, basic testing shows that my solution works well in general cases. 

An example of a potential fail case would be a partial/full occlusion of the camera. In the case of full
occulsion, the program will detect that the car has left and then detect a "new" car after the occlusion clears.

Drastic changes in lighting/noise may also provide issue. In terms of color detection, cars which 
are white, under certain lighting, will be considered blue using current method. In addition, if the 
lighting change is so intense as to blur the boundaries of the car, there may be resultant artifacts 
when comparing vehicles between frames which could result in misclassification. An attempt was made to 
limit the latter scenario, by updating the stored image every couple of minutes. 

A more agile solution would require more complex models for all 3 components of the program.

One possible idea is replacing Yolo3 with UNets. UNets are state of the art of image segmentation. 
A well trained UNet for vehicle segmentation will only capture the vehicle (Versus a bounding box around the vehicle).

This means, less noise when comparing vehicles and running color detection.

Currently, color detection uses a rule-based method. Even with perfect data, may be prone to misdetect at times. 
For example, a blue car with a bright red light be misdetected as red. With traing data, we could train several 
svms with color-histograms. A one-verus-k approach could then be used to identify most likely color.

For vehicle comparison, we could seek to retireve and compare the intermediate convolutional results from yolo. 
The same vehicle should be considered a vehicle for generally the same reasons. Having initially attempted and 
failed to use ORB for feature matching, I wrote it off as an image quality problem, but it's possible that I
hadn't optimized parameters correctly. If so, using ORB would be the simpler approach.

This was done as a coding assignment for the Computer Vision Enginnering position at Verkada.
