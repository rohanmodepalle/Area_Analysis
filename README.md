# Area Analysis for large areas
Area analysis for large areas using live video stream/IP camera in OpenCV.

- The major goal is to leverage the project as a ready-to-scale business model.
- Use case: real-time analysis of different sections of a large area like supermarkets.
- Improving performance by automating features and optimising the real-time stream.
- Also serves as a very useful tool for shopowners to analyse the products in the store by checking how the demand is distributed.

--- 

## Table of Contents
* [Introduction](#introduction)
* [Running Inference](#running-inference)
* [Features](#features)
* [References](#references)
* [Limitations](#limitations)

## Introduction
**SSD detector:**
- We're employing a MobileNet architecture with an SSD (Single Shot Detector). In most cases, only one shot is required to detect everything is present in an image. That is, one for generating region suggestions and another for determining what each proposal's purpose is.
- SSD is quite fast when compared to other 2 shot detectors like R-CNN.
- MobileNet is a DNN designed to run on low-resource devices, as the name suggests. Mobile phones, IP cameras, scanners, and other similar devices are examples.
- As a result, a MobileNet seasoned SSD should ideally result in a faster, more efficient object detection.
---
**Centroid tracker:**
- The Centroid Tracker is one of the most trustworthy trackers available.
- The centroid tracker, to put it simply, calculates the centroid of the bounding boxes.
- The bounding boxes, in other words, are the (x, y) coordinates of the objects in a picture.
- The tracker computes the centroid (centre) of the box once our SSD obtains the co-ordinates. To put it another way, the object's core.
- Then, for tracking purposes over the sequence of frames, each detected object is given a unique ID.

## Running Inference
- Install all the required Python dependencies:
```
pip install -r requirements.txt
```
- To run inference on video files or IP cameras:
```
# Enter the video file path or IP camera url in the url list of 'mylib/config.py' (eg., url = 'rtsp://username:password@IP_address:port/stream','videos/example_01.mp4')

url = ''
```
> Set url = 0 for webcam.

## Features

***1. Scheduler:***
- Automatic scheduler to start the software. Configure to run at every second, minute, day, or Monday to Friday.
- This is extremely useful in a business scenario, for instance, you can run it only at your desired time (9-5?).
- Variables and memory would be reset == less load on your machine.
- Set Scheduler = True in mylib/config.py file to use this feature.

```
##Runs at every day (9:00 am). You can change it.
schedule.every().day.at("9:00").do(run)
```

***2. Simple analysis chart:***
- Graphs all the data after every run.
- Useful for analysing different areas of the store in the same graph.
- Total number of people in that area and the average time the people spend there can be clearly seen.
- Once all the video streams end, we can see the graph.

***3. Threshold Time:***
- Threshold time is the time in seconds that the person has to be in the frame to be counted.
- This is useful in a business scenario, for instance, you can set it to be 5 seconds.
- Set Threshold Time = 5 in mylib/config.py file to use this feature.
- This is because it is not correct to count people who are crossing people from one side to another as people who spend time in that area.

***4. Multithreading:***
- Multithreading is used to speed up the software.
- Each thread is responsible for a specific area of the store.
- Each thread can be stopped individually without affecting the others by pressing 'q' with that particular video stream selected..

## References
- SSD paper: https://arxiv.org/abs/1512.02325
- MobileNet paper: https://arxiv.org/abs/1704.04861
- Centroid tracker: https://www.pyimagesearch.com/2018/07/23/simple-object-tracking-with-opencv/
- https://towardsdatascience.com/review-ssd-single-shot-detector-object-detection-851a94607d11

## Limitations
- Train the SSD on human data only with a top-down view for good accuracy.
- Most IP cameras work only with 2.4gHz so check network before using camera.
- Some Operating Systems will not be able to run the code for IP cameras as they dont support rtsp protocol videos.

<p>&nbsp;</p>

---

