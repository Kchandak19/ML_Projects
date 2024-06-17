Description: 

During lectures, conferences or any sort of meeting that has a lot of audience present, it becomes really difficult to pinpoint which of the candidates are un-attentive. Over the years, quite some research has been done  in the area of attention detection and identification of human faces with respect to different applications. In this paper we used multiple criterias for determining whether the person is attentive or not. This attentiveness can be determined by the eye movements, head movements etc. We recognize the face of each candidate using image processing and then determine his/her attentiveness based on his facial features.  

Methodology 

The system is divided into three modules: 

 

Face detection Module: In the first step, we captured video from the webcam which is then converted into frames. The next task is to detect the faces from these frames. For the face detection, we used Histogram of Oriented Gradients (HOG) and Support Vector Machines (SVM). Here the sliding window approach is used on the image, where we slide a window from left-to-right and top-to-bottom for object recognition. After scanning the image, we applied non-maximum suppression to remove redundant and overlapping bounding boxes. These will give (x, y) coordinates of faces. 

 

Facial Landmark Detection Module: After getting the (x, y)-coordinates of the faces in the image, we applied facial landmark detection to the face regions. Then the shape predictor, which is a pre-trained model of dlib is applied, to obtain the (x, y)-coordinates of the face regions in the face region of interest .By applying facial landmark detection, we got 68 (x, y)-coordinates that map to the specific facial features in the face which was then converted from the dlib object to a NumPy array.  

 

Attentiveness detection Module: The last part of the project was to detect whether a person is attentive or not. To determine if the eyes are closed or not we computed the eye aspect ratio (EAR). If the eye aspect ratio< 0.3 for an adequately long amount of time, we concluded that the person is inattentive. 

