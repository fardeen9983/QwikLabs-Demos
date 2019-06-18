# Cloud Endpoints

## Overview
In this lab you will deploy a sample API with [Google Cloud Endpoints](https://cloud.google.com/endpoints/docs/frameworks/about-cloud-endpoints-frameworks), which are a set of tools for generating APIs from within an App Engine application. The sample code will include:

A REST API that you can query to find the name of an airport from its three-letter IATA code (for example, SFO, JFK, AMS).
A script that uploads the API configuration to Cloud Endpoints.
A script that deploys a Google App Engine flexible backend to host the sample API.
After you send some requests to the sample API, you can view the Cloud Endpoints Activity Graphs and Logs. Theses are tools that allow you to monitor your APIs and gain insights into their usage.

## Steps
### **Getting the sample code**
1. Enter the following command in Cloud Shell to get the sample API and scripts:
    ```sh
    git clone https://github.com/GoogleCloudPlatform/endpoints-quickstart
    ```
2. Change to the directory that contains the sample code:

    ```sh
    cd endpoints-quickstart
    ```

### **Deploying the Endpoints configuration**
To publish a REST API to Endpoints, an OpenAPI configuration file that describes the API is required. The lab's sample API comes with a pre-configured OpenAPI file called openapi.yaml.

Cloud Endpoints uses Google Service Management, an infrastructure service of Cloud Platform, to create and manage APIs and services. To use Endpoints to manage an API, you deploy the API's OpenAPI configuration to Service Management.

Now you'll deploy the Endpoints configuration.

1. In the endpoints-qwikstart directory, enter the following:
    ```sh
    cd scripts
    ```
2. Run the following script, which is included in the sample:
    ```sh
    ./deploy_api.sh
    ```
Cloud Endpoints uses the host field in the OpenAPI configuration file to identify the service. The deploy_api.sh script sets the ID of your Cloud project as part of the name configured in the host field. (When you prepare an OpenAPI configuration file for your own service, you will need to do this manually.)

The script then deploys the OpenAPI configuration to Service Management using the command: gcloud endpoints services deploy openapi.yaml

As it is creating and configuring the service, Service Management outputs some information to the console. You can safely ignore the warnings about the paths in openapi.yaml not requiring an API key. On successful completion, you see a line like the following that displays the service configuration ID and the service name:
```sh
Service Configuration [2017-02-13-r2] uploaded for service [airports-api.endpoints.example-project.cloud.goog]
```
### **Deploying the API backend**
So far you have deployed the OpenAPI configuration to Service Management, but you have not yet deployed the code that will serve the API backend. The deploy_app.sh script included in the lab sample creates an App Engine flexible environment to host the API backend, and then the script deploys the API to App Engine.

1. To deploy the API backend, make sure you are in the endpoints-quickstart/scripts directory. Then, run the following script:
    ```sh
    ./deploy_app.sh
    ```
    The script runs the following command to create an App Engine flexible environment in the us-central region: gcloud app create --region="$REGION"

It takes a couple minutes to create the App Engine flexible backend. You'll see the following displayed in Cloud Shell after the App Engine is created:

Success! The app is now created. Please use `gcloud app deploy` to deploy your first app.

The script goes on to run the gcloud app deploy command to deploy the sample API to App Engine.

You'll then see a line like the following in Cloud Shell:
    ```sh
    Deploying ../app/app_template.yaml...You are about to deploy the following services:
    ```
It takes several minutes for the API to be deployed to App Engine. You'll see a line like the following when the API is successfully deployed to App Engine:
    ```sh
    Deployed service [default] to [https://example-project.appspot.com]
    ```
### **Sending requests to the API**
1. After deploying the sample API, you can send requests to it by running the following script:
    ```sh
    ./query_api.sh
    ```
    The script echoes the curl command that it uses to send a request to the API, and then displays the result. You'll see something like the following in Cloud Shell:
    ```sh
    curl "https://example-project.appspot.com/airportName?iataCode=SFO"
    San Francisco International Airport
    ```

2. The API expects one query parameter, iataCode, that is set to a valid IATA airport code such as SEA or JFK.
To test, run this example in Cloud Shell:
    ```sh
    ./query_api.sh JFK
    ```
You just deployed and tested an API in Cloud Endpoints!

### **Tracking API activity**
With APIs deployed with Cloud Endpoints, you can monitor critical operations metrics in the Google Cloud Platform Console and gain insight into your users and usage with Stackdriver Logging.

1. Run this traffic generation script in Cloud Shell to populate the graphs and logs.
    ```sh
    ./generate_traffic.sh
    ```
2. Note This script generates requests in a loop and automatically times out in 5 minutes. To end the script sooner, enter Ctrl-c in Cloud Shell.
3. In the Console, click on Endpoints in the Tools section to look at the activity graphs for your API. It may take a few moments for the requests to be reflected in the graphs. You can do this while you wait for data to be displayed:

4. If the Permissions side panel is not open, click +Permissions. The Permissions panel allows you to control who has access to your API and the level of access.

5. Click the Deployment history tab. This tab displays a history of your API deployments, including the deployment time and who deployed the change.

6. Click the Overview tab. Here you'll see the traffic coming in. After the traffic generation script has been running for a minute, scroll down to see the three lines on the Total latency graph (50th, 95th, and 98th percentiles). This data provides a quick estimate of response times.

7. At the bottom of the Endpoints graphs, under Method, click the View all logs link for GET/airportName. The Logs Viewer page displays the request logs for the API.

8. Enter Ctrl-C in Cloud Shell to stop the script.

### **Add a quota to the API**
NOTE: This is a beta release of Quotas. This feature might be changed in backward-incompatible ways and is not subject to any SLA or deprecation policy.
Cloud Endpoints lets you set quotas so you can control the rate at which applications can call your API. Quotas can be used to protect your API from excessive usage by a single client.

1. Deploy the Endpoints configuration that has a quota:
    ```sh
    ./deploy_api.sh ../openapi_with_ratelimit.yaml
    ```
2. Redeploy your app to use the new Endpoints configuration (this may take a few minutes):
    ```sh
    ./deploy_app.sh
    ```
3. In the Console, navigate to Navigation menu > API & Services > Credentials.

4. Click Create credentials and choose API key. A new API key is displayed on the screen.

5. Click the double rectangle icon to copy it to your clipboard.

6. In Cloud Shell, type the following. Replace YOUR-API-KEY with the API key you just created:
    ```sh
    export API_KEY=YOUR-API-KEY
    ```
7. Send your API a request using the API key variable you just created:
    ```sh
    ./query_api_with_key.sh $API_KEY
    ```
    You'll see something like the following on the console:
    ```sh
    curl -H 'x-api-key: AIzeSyDbdQdaSdhPMdiAuddd_FALbY7JevoMzAB' "https://example-project.appspot.com/airportName?iataCode=SFO"
    San Francisco International Airport
    ```

8. The API now has a limit of 5 requests per second. Run the following command to send traffic to the API and trigger the quota limit:
    ```sh
    ./generate_traffic_with_key.sh $API_KEY
    ```
9. After running the script for 5-10 seconds, enter Ctrl-c in Cloud Shell to stop the script.

10. Send another authenticated request to the API:
    ```sh
    ./query_api_with_key.sh $API_KEY
    ```
    You'll see something like the following on the console:
    ```json
    {
        "code": 8,
        "message": "Insufficient tokens for quota 'airport_requests' and limit 'limit-on-airport-requests' of service 'example-project.appspot.com' for consumer 'api_key:AIzeSyDbdQdaSdhPMdiAuddd_FALbY7JevoMzAB'.",
        "details": [
            {
            "@type": "type.googleapis.com/google.rpc.DebugInfo",
            "stackEntries": [],
            "detail": "internal"
            }
        ]
    }
    ```
    If you get a different response, try running the generate_traffic_with_key.sh script again and retry.

## Next Steps/Learn More
For more information about quotas, see the following:
* [Quotas for OpenAPI](https://cloud.google.com/endpoints/docs/openapi/quotas-overview)
* [Quotas for Endpoints Frameworks](https://cloud.google.com/endpoints/docs/frameworks/quotas-overview)
* [Quotas for gRPC](https://cloud.google.com/endpoints/docs/grpc/quotas-overview)