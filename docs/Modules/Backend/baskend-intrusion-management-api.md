---
sidebar_label: "Intrusion Management API"
---

# Intrusion Management API

[This API](https://github.com/ES-07/intrusion-management-api) will be used to act whenever an intrusion is detected. It will get the intrusion video clips from the cameras, activate the alarms, and trigger a new notification in the Notifications API. The last API wasn't developed due to lack of time, but the cameras are sending the video to this API, the alarms are being activated and the video is stored in **S3 Bucket**.
The alarm activation consists in a message that is sent through Rabbit MQ with the **intrusion timestamp**. Thus, there is nothing to show beyond a print in terminal.
This Api has also an endpoint used by Cameras API to post the video on the S3 bucket.
