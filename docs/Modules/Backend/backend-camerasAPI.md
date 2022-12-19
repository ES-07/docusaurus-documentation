---
sidebar_label: "Cameras API"
---

# Cameras API

[Cameras API](https://github.com/ES-07/es_gap_2022_helpers/blob/main/HumanDetection/camera/master.py) was developed with a single endpoint responsible to send the videos to Intrusion Management API.
It will get the intrusion timestamp and then will get the video 3 minutes before and 3 minutes after the intrusion. This processes a video file and send the frames to a message queue.

The `VideoProducer` class is defined in the code, which has a constructor that sets the connection details for the message queue and some other parameters. The **createConnection** method sets up the connection to the message queue and declares the exchange and queue. The processVideo method reads the frames from a video file, processes them, and sends them to the message queue using the `kombu_producer` object.

The `sendVideo` function is then defined as a FastAPI endpoint that can be accessed via an HTTP request. This function creates an instance of the `VideoProducer` class and calls its **createConnection** and **processVideo** methods to send the video frames to the message queue.
