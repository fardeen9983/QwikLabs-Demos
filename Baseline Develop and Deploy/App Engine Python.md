# App Engine : Python
App Engine allows developers to focus on doing what they do best, writing code. The App Engine standard environment is based on container instances running on Google's infrastructure. Containers are preconfigured with one of several available runtimes (Java 7, Java 8, Python 2.7, Go and PHP). Each runtime also includes libraries that support [App Engine Standard APIs](https://cloud.google.com/appengine/docs/about-the-standard-environment#index_of_features). For many applications, the standard environment runtimes and libraries might be all you need.

The App Engine standard environment makes it easy to build and deploy an application that runs reliably even under heavy load and with large amounts of data. It includes the following features:

* Persistent storage with queries, sorting, and transactions.
* Automatic scaling and load balancing.
* Asynchronous task queues for performing work outside the scope of a request.
* Scheduled tasks for triggering events at specified times or regular intervals.
* Integration with other Google cloud services and APIs.

Applications run in a secure, sandboxed environment, allowing App Engine standard environment to distribute requests across multiple servers, and scaling servers to meet traffic demands. Your application runs within its own secure, reliable environment that is independent of the hardware, operating system, or physical location of the server.

## Tasks
* Download an application
* Test the application
* Deploy the application

## Steps
### Enable Google App Engine Admin API
The App Engine Admin API enables developers to provision and manage their App Engine Applications.

1. In the left menu click APIs & Services > Library.
2. Type "App Engine Admin API" in search box.
3. Click App Engine Admin API.
4. Click Enable.
   
### Download the Hello World app
There is a simple Hello World app for Python you can use to quickly get a feel for deploying an app to Google Cloud Platform. Follow these steps to download Hello World to your Google Cloud instance.

1. Enter the following command to clone the [Hello World sample app repository](https://github.com/GoogleCloudPlatform/python-docs-samples) to your Google Cloud instance:
    ```sh
    git clone https://github.com/GoogleCloudPlatform/python-docs-samples
    ```
2. Goto the directory with the sample code
    ```sh
    cd python-docs-samples/appengine/standard/hello_world
    ```
## Test the application
Test the application using the Google Cloud development server (dev_appserver.py), which is included with the preinstalled App Engine SDK.

1. From within your helloworld directory where the app's app.yaml configuration file is located, start the Google Cloud development server with the following command:`
    ```sh
    dev_appserver.py app.yaml
    ```
    The development server is now running and listening for requests on port 8080.
2. View the results by clicking the Web preview > Preview on port 8080.
### Make a change
You can leave the development server running while you develop your application. The development server watches for changes in your source files and reloads them if necessary.

Let's try it. Leave the development server running. We'll open another command line window, then edit main.py to change "Hello, World!" to "Hello, Cruel World!".

1. Click the + next to your Cloud Shell tab to open a new command line session.
2. Enter this command to go to the directory that contains the sample code.
    ```sh
    cd python-docs-samples/appengine/standard/hello_world
    ```
3. Enter the following to open main.py in nano to edit the content.
    ```sh
    nano main.py
    ```
4. Change "Hello, World!" to "Hello, Cruel World!". Exit and save the file.

5. Reload the Hello World! Browser or click the Web Preview > Preview on port 8080 to see the results.
   
### Deploy your app
To deploy your app to App Engine, run the following command from within the root directory of your application where the app.yaml file is located:
```sh
gcloud app deploy
```
You will be prompted to enter where your App engine will be located.
```sh
Please choose the region where you want your App Engine application
located:

 [1] europe-west2  (supports standard and flexible)
 [2] us-east1      (supports standard and flexible)
 [3] us-east4      (supports standard and flexible)
 [4] asia-northeast1 (supports standard and flexible)
 [5] asia-south1   (supports standard and flexible)
 [6] australia-southeast1 (supports standard and flexible)
 [7] southamerica-east1 (supports standard and flexible)
 [8] us-central    (supports standard and flexible)
 [9] europe-west3  (supports standard and flexible)
 [10] europe-west   (supports standard and flexible)
 [11] cancel
Please enter your numeric choice:
```

Enter the number that represents your region. The App Engine application will then be created.

Enter Y when prompted to confirm the details and begin the deployment of service.

Example output
```sh
Beginning deployment of service [default]...
Some files were skipped. Pass `--verbosity=info` to see which ones.
You may also view the gcloud log file, found at
[/tmp/tmp.dYC7xGu3oZ/logs/2017.11.17/07.18.27.372768.log].
╔════════════════════════════════════════════════════════════╗
╠═ Uploading 5 files to Google Cloud Storage                ═╣
╚════════════════════════════════════════════════════════════File upload done.
Updating service [default]...done.
Waiting for operation [apps/qwiklabs-gcp-233dca09c0ab577b/operations/2e88ab76-33dc-4aed-93c4-fdd944a95ccf] to complete...done.
Updating service [default]...done.
Deployed service [default] to [https://qwiklabs-gcp-233dca09c0ab577b.appspot.com]

You can stream logs from the command line by running:
  $ gcloud app logs tail -s default

To view your application in the web browser run:
  $ gcloud app browse
```

### View your application
To launch your browser enter the following command, then click on the link it provides.
```sh
gcloud app browse
```

Your application is deployed and you can read the short message in your browser.

## Next Steps /Learn More
Lean more about an App Engine with [An Overview Of App Engine](https://cloud.google.com/appengine/docs/about-the-standard-environment)

Try something else with an App Engine with [Getting Started with Flask on App Engine Standard Environment](https://cloud.google.com/appengine/docs/standard/python/getting-started/python-standard-env)