Description: 

During lectures, conferences or any sort of meeting that has a lot of audience present, it becomes really difficult to pinpoint which of the candidates are un-attentive. Over the years, quite some research has been done  in the area of attention detection and identification of human faces with respect to different applications. In this paper we used multiple criterias for determining whether the person is attentive or not. This attentiveness can be determined by the eye movements, head movements etc. We recognize the face of each candidate using image processing and then determine his/her attentiveness based on his facial features.  

Methodology 

The system is divided into three modules: 

 

Face detection Module: In the first step, we captured video from the webcam which is then converted into frames. The next task is to detect the faces from these frames. For the face detection, we used Histogram of Oriented Gradients (HOG) and Support Vector Machines (SVM). Here the sliding window approach is used on the image, where we slide a window from left-to-right and top-to-bottom for object recognition. After scanning the image, we applied non-maximum suppression to remove redundant and overlapping bounding boxes. These will give (x, y) coordinates of faces. 

 

Facial Landmark Detection Module: After getting the (x, y)-coordinates of the faces in the image, we applied facial landmark detection to the face regions. Then the shape predictor, which is a pre-trained model of dlib is applied, to obtain the (x, y)-coordinates of the face regions in the face region of interest .By applying facial landmark detection, we got 68 (x, y)-coordinates that map to the specific facial features in the face which was then converted from the dlib object to a NumPy array.  

 
Attention Detection:

After detecting facial landmark and extracting the eye regions.
Now that we have the eye regions, we can calculate the eye aspect ratio to determine whether the eyes are closed or not. If the eye aspect ratio indicates that the person’s eyes have been closed for a sufficiently long amount of time, we’ll conclude that the person is un-attentive. 

In the eye aspect ratio calculation we use the SciPy package so that we can calculate the Euclidean distance between facial landmarks points. We also use the imutils package, to make working with OpenCV easier. The EAR or Eye Aspect Ratio function is used to calculate the ratio of distances between the vertical eye landmarks and the distances between the horizontal eye landmarks. The return value of the eye aspect ratio remains approximately constant when the eye is open. The value will then rapidly reduce towards zero during a blink. In situation of eyes being closed, the eye aspect ratio will again remain constant(approximately), but will be much smaller than the ratio when the eye is open. 

On the top-left  diagram we have an eye which  is fully open with the eye facial landmarks plotted. Then on the top-right diagram we have an eye that is closed. The bottom diagram shows a plot between the eye aspect ratio and time. Here in the diagram we can see, the value of eye aspect ratio is almost constant (showing that the eye is open), then it rapidly drops to zero, then again increases, suggesting that the person blinked. In our attention detector case, we’ll be observing the eye aspect ratio to see if the value decreases but does not increase again, thus suggesting that the person’s eyes are closed. If the eye aspect ratio drops down below that particular threshold, we’ll start incrementing the counter to count the number of frames the person has closed their eyes for. If the number of frames the person has closed their eyes in goes above this threshold, we infer that the person is not paying attentive. The eye aspect ratio formula, we have used is: 

 

where p1, …, p6 are 2D facial landmark locations. 

 

The numerator of the equation calculates the distance between the vertical eye landmark locations while the denominator calculates the distance between horizontal eye landmark locations. It is important to weight the denominator appropriately since there is only one set of horizontal points but two sets of vertical points. 

Thus we conclude that if the EAR is drops down below this threshold, the person is dizzy which means he is not attentive . The EAR may differ due to closed eyes indicating that the person is asleep or tilted head movements all leading to the non-attentiveness of the person. 

 

Deep Learning for Face Detection 

 

Face recognition is the issue of identifying and verifying people in a picture by their face. It is a task that is trivially performed by humans, even under varying light and when faces are changed by age or obstructed with accessories and facial hair. Moreover, face recognition continued to be a challenging computer vision problem for decades until recently. Now, deep learning methods are able to grasp huge datasets of faces and learn rich and compact representations of faces, allowing modern models to first perform as-well and later to outperform the face recognition capabilities of humans. The deep learning-based facial embeddings we use here are both (1) highly accurate and (2) capable of being executed in real-time. 

Conclusion & future scope:  

The model made by us suggests that it is very much possible to detect the attention of a person by analysing their blink patterns under the assumption that all individuals develop drowsiness in the same way. Our system has been proved effective in determining the attentiveness of a person irrespective of whether or not they wear spectacles. This model has a clear potential usage as a tool for automated analytics of the learning process, providing a mechanism for large-scale analytics on student learning using minimum yet capable hardware. Other aspects of attention detection like head movements, body postures can also be taken into account to create a space wherein worrying about the students’ attention would be one of the least headaches to the teacher. 
