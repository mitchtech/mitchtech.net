+++
author = "michael"
categories = ["Tutorials","Ubuntu"]
comments = true
date = "2012-05-02 15:58:13+00:00"
layout = "post"
link = "http://mitchtech.net/opencv-python/"
slug = "opencv-python"
tags = ["C","Computer Vision","Device Driver","Face Detection","Linux","Motion Tracking","OpenCV","OpenNI","PrimeSense","Python","Ubuntu","Webcam"]
title = "OpenCV + Python"

+++

Here are some of the more interesting OpenCV demos using the Python wrapper.  The installation process on Ubuntu is covered in my previous post, [OpenCV + Ubuntu.](http://mitchtech.net/opencv-ubuntu/) The demo scripts are located in samples/python within the OpenCV release.

The cam shift sample below demonstrates the color/object detection capability of OpenCV. To set the object/color to track, click and drag a box on the video using the mouse.  The histogram window will display the target for OpenCV to locate and track within the field of view.  The more distinct the color from the background of the scene, the better it works.  The trailing 0 at the end means to use camera input device 0.

```
python ./camshift.py 0
```

{{< youtube AqXaGPEAkRA >}}

To run the face detection demo, you will need to use the -c command line option to specify the classifier to use. Different classifiers detect using different algorithms and so are better suited to certain detection condition, angles, etc. compared to others.  The classifier used in the demo works best with faces directly facing the camera, and doesn’t do as well with tilted, rotated, or otherwise not direct faces.  This is why some of the  titled faces in the Google image search part of the video fail to be recognized by OpenCV.

```
python ./facedetect.py -c /usr/local/share/OpenCV/haarcascades/haarcascade_frontalface_alt.xml 0
```

{{< youtube jCjUCeYWKBg >}}

If you don’t have a camera connected, and still want to verify that the Python wrapper is working correctly, you can run the previous examples  using an image or video file, otherwise try out the following examples (also in samples/python):

```
python ./minarea.py

python ./delaunay.py

python ./dmtx.py

python ./drawing.py
```

