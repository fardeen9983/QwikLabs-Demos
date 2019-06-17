# Data Loss Prevention
The [Data Loss Prevention API](https://cloud.google.com/dlp/) provides programmatic access to a powerful detection engine for personally identifiable information and other privacy-sensitive data in unstructured data streams.

The DLP API provides fast, scalable classification and optional redaction for sensitive data elements like credit card numbers, names, social security numbers, passport numbers, and phone numbers. The API supports text and images – just send data to the API or specify data stored on your Google Cloud Storage, BigQuery, and Cloud Datastore instances.

## Objective
* Set up the Data Loss Prevention API and and use the API to inspect a string of data for sensitive information.

## Steps
### Download the DLP API
1. Let's download the DLP API files. Run the following command in Cloud Shell to clone the [Node JS DLP repo](https://github.com/googleapis/nodejs-dlp):
    ```sh
    git clone https://github.com/googleapis/nodejs-dlp.git
    ```
2. Go ahead and set the environment variable GCLOUD_PROJECT to your Qwiklabs project ID:
    ```sh
    export GCLOUD_PROJECT=[YOUR_PROJECT_ID]
    ```
### Install dependencies
`. Now that we have our files downloaded and environment variable set, let's install the app's dependencies by running the following commands:
    ```sh
    npm install --save @google-cloud/dlp
    npm install yargs
    ```
    You may see some warnings in the gcloud console-you can ignore them.
### Inspect a string for sensitive information
Now that our dependencies are installed, let's use the DLP API to inspect a string for sensitive information.

1. Run the following command to go into the nodejs-dlp/samples directory:
    ```sh
    cd nodejs-dlp/samples
    ```
2. Run the following command to inspect the string "My email address is joe@example.com." for sensitive information:
    ```sh
    node inspect.js string "My email address is joe@example.com."
    ```
You should receive the following output:
```sh
Findings:
       Quote: joe@example.com
       Info type: EMAIL_ADDRESS
       Likelihood: LIKELY
```
The result shows what the piece of sensitive data was found, what type of information it is, and how sure the API is that the string contains sensitive information.

You're welcome to try running additional tests in your remaining lab time. The following are a couple samples to get you started:

node inspect.js string "My phone number is 555-555-5555"

node inspect.js string "My phone# is 555-555-5555"