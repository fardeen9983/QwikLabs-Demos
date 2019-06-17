# Cloud Functions
## Overview
Google Cloud Functions is a serverless execution environment for building and connecting cloud services. With Cloud Functions you write simple, single-purpose functions that are attached to events emitted from your cloud infrastructure and services. Your Cloud Function is triggered when an event being watched is fired. Your code executes in a fully managed environment. There is no need to provision any infrastructure or worry about managing any servers.

Cloud Functions are written in Javascript and execute in a Node.js environment on Google Cloud Platform. You can take your Cloud Function and run it in any standard Node.js runtime which makes both portability and local testing a breeze.

## Connect and Extend Cloud Services
Cloud Functions provides a connective layer of logic that lets you write code to connect and extend cloud services. Listen and respond to a file upload to Cloud Storage, a log change, or an incoming message on a Cloud Pub/Sub topic. Cloud Functions augments existing cloud services and allows you to address an increasing number of use cases with arbitrary programming logic. Cloud Functions have access to the Google Service Account credential and are thus seamlessly authenticated with the majority of Google Cloud Platform services such as Datastore, Cloud Spanner, Cloud Translation API, Cloud Vision API, as well as many others. In addition, Cloud Functions are supported by numerous [Node.js client libraries](https://cloud.google.com/nodejs/apis), which further simplify these integrations.

## Events and Triggers
Cloud events are things that happen in your cloud environment.These might be things like changes to data in a database, files added to a storage system, or a new virtual machine instance being created.

Events occur whether or not you choose to respond to them. You create a response to an event with a trigger. A trigger is a declaration that you are interested in a certain event or set of events. Binding a function to a trigger allows you to capture and act on events. For more information on creating triggers and associating them with your functions, see [Events and Triggers](https://cloud.google.com/functions/docs/concepts/events-triggers).

## Serverless
Cloud Functions removes the work of managing servers, configuring software, updating frameworks, and patching operating systems. The software and infrastructure are fully managed by Google so that you just add code. Furthermore, provisioning of resources happens automatically in response to events. This means that a function can scale from a few invocations a day to many millions of invocations without any work from you.

## Use Cases
Asynchronous workloads like lightweight ETL, or cloud automations like triggering application builds now no longer need their own server and a developer to wire it up. You simply deploy a Cloud Function bound to the event you want and you're done.

The fine-grained, on-demand nature of Cloud Functions also makes it a perfect candidate for lightweight APIs and webhooks. In addition, the automatic provisioning of HTTP endpoints when you deploy an HTTP Function means there is no complicated configuration required as there is with some other services. See the following table for additional common Cloud Functions use cases:

Use Case |Description
-| -
Data Processing / ETL|Listen and respond to [Cloud Storage](https://cloud.google.com/storage) events such as when a file is created, changed, or removed. Process images, perform video transcoding, validate and transform data, and invoke any service on the Internet from your Cloud Function.
Webhooks|Via a simple [HTTP trigger](https://cloud.google.com/functions/docs/calling/http), respond to events originating from 3rd party systems like GitHub, Slack, Stripe, or from anywhere that can send HTTP requests.
Lightweight APIs|Compose applications from lightweight, loosely coupled bits of logic that are quick to build and that scale instantly. Your functions can be event-driven or invoked directly over HTTP/S.
Mobile Backend|Use Google's mobile platform for app developers, Firebase, and write your mobile backend in Cloud Functions. Listen and respond to events from Firebase Analytics, Realtime Database, Authentication, and Storage.
IoT|Imagine tens or hundreds of thousands of devices streaming data into Cloud Pub/Sub, thereby launching Cloud Functions to process, transform and store data. Cloud Functions lets you do in a way that's completely serverless.

## Tasks
* Create a cloud function

* Deploy and test the function

* View logs

## Steps
Go to GCP console
### Create a new cloud function
1. In the console, click the Navigation menu > Cloud Functions.
2. Click Create function.
3. In the Create function dialog, enter the following values:

    Field|   Value
    -|-
    Name|    GCFunction
    Memory allocated|    Default
    Trigger|    HTTP trigger
    Source code|    Inline editor (use the default helloWorld function implementation already provided for index.js.)

### Deploy the function
1. Still in the Create function dialog, at the bottom, click Create to deploy the function.

2. After you click Create, the console redirects to the Cloud Functions Overview page.

3. While the function is being deployed, the icon next to it is a small spinner. When it's deployed, the spinner is a green check mark.

### Test the function
Test the deployed function.

1. In the Cloud Functions Overview page, display the menu for your function, and click Test function.
2. In the Triggering event field, enter the following text between the brackets {} and click Test the function.
In the Output field, you should see the message Success: Hello World!

In the Logs field, a status code of 200 indicates success. (It may take a minute for the logs to appear.)

### View logs
View logs from the Cloud Functions Overview page.

1. Click the blue arrow to go back to the Cloud Functions Overview page.
2. Display the menu for your function, and click View logs.
