---
sidebar_label: "Intrusion Management API"
---

# Intrusion Management API

[This API](https://github.com/ES-07/intrusion-management-api) will be used to act whenever an intrusion is detected. It will get the intrusion video clips from the cameras, activate the alarms, and trigger a new notification in the Notifications API. The last API wasn't developed due to lack of time, but the cameras are sending the video to this API, the alarms are being activated and the video is stored in **S3 Bucket**.
The alarm activation consists in a message that is sent through Rabbit MQ with the **intrusion timestamp**. Thus, there is nothing to show beyond a print in terminal.
This Api has also an endpoint used by Cameras API to post the video on the S3 bucket.

The code defines several classes, including the `Intrusion` class, which appears to represent an intrusion event. This class has three attributes: `timestamp`, `building_id`, and `device_id`.

The `VideoStore` class represent a video file stored in a cloud storage service. It has three attributes: `path_to_video`, `bucket_name`, and `video_name`.

Finally, it is defined several endpoints for the API, including a root endpoint that returns a welcome message, and a post endpoint for receiving and processing intrusion data.
