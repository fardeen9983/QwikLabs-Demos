# Video Intelligence
[Google Cloud Video Intelligence: Search every moment of every video in your catalog](https://youtu.be/Z2eOfK2rzbs)

Google Cloud Video Intelligence makes videos searchable and discoverable by extracting metadata with an easy to use REST API. You can now search every moment of every video file in your catalog. It quickly annotates videos stored in Google Cloud Storage, and helps you identify key entities (nouns) within your video; and when they occur within the video. Separate signal from noise by retrieving relevant information within the entire video, shot-by-shot, -or per frame.

## Steps
### Enable the Video Intelligence API

For this lab the Cloud Video Intelligence API should be enabled so you can use it right away. 

1. In the left-hand navigation menu, select APIs & Services > Library
2. Then search for "video".
3. Click on the Cloud Video Intelligence API in the results that are returned, then click Enable if it is not enabled.

### Set up authorization

1. In Cloud Shell run the following command to create a new service account named quickstart:
    ```sh
    gcloud iam service-accounts create quickstart
    ```
2. Create a service account key file, replacing <your-project-123> with your Qwiklabs GCP Project ID:
    ```sh
    gcloud iam service-accounts keys create key.json --iam-account quickstart@<your-project-123>.iam.gserviceaccount.com
    ```
3. Now authenticate your service account, passing the location of your service account key file:
    ```sh
    gcloud auth activate-service-account --key-file key.json
    ```
4. Obtain an authorization token using your service account:
    ```sh
    gcloud auth print-access-token
    ```
    The token will print in the output, and you'll be using it in a future step.

### Make an annotate video request
1. Use the editor of your choice (nano, vi, etc. or the gcloud editor) to create a JSON request file with the following text, and save it as request.json :
    ```json
    {
    "inputUri":"gs://cloud-ml-sandbox/video/chicago.mp4",
    "features": [
        "LABEL_DETECTION"
    ]
    }
    ```

2. Use curl to make a videos:annotate request, replacing ACCESS_TOKEN with the access token you printed, and passing the filename of the entity request:
    ```sh
    curl -s -H 'Content-Type: application/json' \
        -H 'Authorization: Bearer ACCESS_CODE' \
        'https://videointelligence.googleapis.com/v1/videos:annotate' \
        -d @request.json
    ```
3. The Video Intelligence API creates an operation to process your request. You should now see a response that includes your operation name, which should look similar to this one:
    ```json
    {
    "name": "us-west1.18358601230245040268"
    }```
    You will use this name in a future step.
4. Use this script to request information on the operation by calling the v1.operations endpoint. Replace the ACCESS_TOKEN as before, and replace the OPERATION_NAME with the operation name value you just received:
    ```sh
    curl -s -H 'Content-Type: application/json' \
        -H 'Authorization: Bearer ACCESS_CODE' \
        'https://videointelligence.googleapis.com/v1/operations/OPERATION_NAME'
    ```
    You'll now see information related to your operation. If the operation has completed, a done field is included and set to true:
    ```json
    {
    "name": "OPERATION_NAME",
    "metadata": {
        "@type": "type.googleapis.com/google.cloud.videointelligence.v1.Annota
    tionProgressMetadata",
        "progressMetadata": [
        {
            "inputUri": "gs://cloud-ml-sandbox/video/chicago.mp4",
            "startTime": "2016-09-22T21:41:56.766091Z",
            "lastUpdateTime": "2016-09-22T21:42:03.889743Z"
        }
        ]
    },
    ...
    }
    ```

4. After giving the request some time (about a minute, typically), re-run the command and the same request returns annotated results:
    ```json
    {
    "name": "OPERATION_NAME",
    "metadata": {
        "@type": "type.googleapis.com/google.cloud.videointelligence.v1.AnnotateVideoProgress",
        "annotationProgress": [
        {
            "inputUri": "/cloud-ml-sandbox/video/chicago.mp4",
            "progressPercent": 100,
            "startTime": "2017-02-17T22:39:00.333942Z",
            "updateTime": "2017-02-17T22:39:11.414399Z"
        }
        ]
    },
    "done": true,
    "response": {
        "@type": "type.googleapis.com/google.cloud.videointelligence.v1.AnnotateVideoResponse",
        "annotationResults": [
        {
            "inputUri": "/cloud-ml-sandbox/video/chicago.mp4",
            "segmentLabelAnnotations": [
            {
                "entity": {
                "entityId": "/m/01yrx",
                "languageCode": "en-US"
                },
                "segments": [
                {
                    "segment": {
                    "startTimeOffset": "0s",
                    "endTimeOffset": "14.833664s"
                    },
                    "confidence": 0.98509187
                }
                ]
            },
            ...
    ```