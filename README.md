This project helps to find the moving objects from a environment

The code has been shared and the line by line explanation is as follows ;

#1   ->  import cv2                 -> This project is made on ComputerVision so cv2 is imported

#2   ->  import imutils             -> This imutils library is used to resize the image

#3   ->  cam = cv2.VideoCapture (0) -> This line helps to use the camera of the device 0 for default or inbuilt cam ; 1 for external cam

#4   ->  firstFrame=None            -> Initialize the firstFrame

#5   ->  area = 500                 -> Initialize area to 500

#6   ->  while True:                -> Infinite loop ; It will continue till the Normal screen and Moving Object detected gets detected

#7   ->  _,img = cam.read()         -> Used to read from camera ; _ is used to avoid True or False as we need only values ; frames from camera is read and stored in img

#8   ->  text = "Normal"            -> Initializing text to Normal ; If no moving object is detected then Normal text will be shown

#9   ->  img = imutils.resize(img, width=1000)           -> Using imutils library resize the video streaming window and setting width to 100

#10  ->  grayImg = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)  -> Using cv2 img is converted into gray scale image

#11  ->  gaussianImg = cv2.GaussianBlur(grayImg, (21, 21), 0) -> Using cv2 grayImg is converted into gaussianImg (smoothening the image)

#12  ->  if firstFrame is None:     -> Loop statement if firstFrame is None the loop will continue to next lines

#13 & #15  -> firstFrame = gaussianImg  
              continue              -> The gaussianImage is stored in firstFrame and if the GaussianImage is stored the loop continues

#16  ->  imgDiff = cv2.absdiff(firstFrame, gaussianImg)   -> The difference b/w firstFrame and gaussianImg is calculated so that in imgDiff the moving image can be calculated

#17  ->  threshImg = cv2.threshold(imgDiff, 25, 255, cv2.THRESH_BINARY)[1]  -> threshhold value given to imgDiff

#18  ->  threshImg = cv2.dilate(threshImg, None, iterations=2)  -> The leftover erotions in the thresImg will be removed

#19  ->  cnts = cv2.findContours(threshImg.copy(), cv2.RETR_EXTERNAL,  - >  contours are found and stored in cnts
            cv2.CHAIN_APPROX_SIMPLE)                                   - >  contours are image moving in the frame

#20  ->  cnts = imutils.grab_contours(cnts)  -> All the contours in the frame is grabbed and overwritted to cnts

#21,22,23  ->  for c in cnts:
            if cv2.contourArea(c) < area:   ---> if the ccontourArea is less than area=500 the 
                    continue                         will continue

#24,25,26  ->  (x, y, w, h) = cv2.boundingRect(c)
            cv2.rectangle(img, (x, y), (x + w, y + h), (0, 255, 0), 2)

            text = "Moving Object detected"

            explanation : the coordiates for bounding Rectangles are given so that in the c the rectangles will be drawn
            25 for  rectangle will be drawn around the src image from the starting point to endind and the color and thickness given as follows
            when this conditions runs the text will be shown as "Moving Object detected"

#27,28,29  -> print(text)

    cv2.putText(img, text, (10, 20),
            cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 0, 255), 2)

    cv2.imshow("cameraFeed",img)  

    explain : text is printed ; the text is putted in the img , font is defined , color and thickness defined 

#30,31  -> cv2.imshow("cameraFeed",img)
           key = cv2.waitKey(1) & 0xFF    -->  the camera window will be shown ; key will be initialized to the wait key defined below

#31,32,33,34 ->  if key == ord("q"):
                    break

                 cam.release()
                 cv2.destroyAllWindows()

                 explain : if key equal to order of q (if q is pressed) the camera window gets close command

                 the camera is released and then AllWindows will be destroyed
