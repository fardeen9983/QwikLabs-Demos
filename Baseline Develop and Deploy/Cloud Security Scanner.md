# Cloud Security Scanner
The Cloud Security Scanner identifies security vulnerabilities in your Google App Engine web applications. It crawls your application, following all links within the scope of your starting URLs, and attempts to exercise as many user inputs and event handlers as possible.

The scanner is designed to complement your existing secure design and development processes. To avoid distracting developers with false positives, the scanner errs on the side of under reporting and will not display low confidence alerts. It does not replace a manual security review, and it does not guarantee that your application is free from security flaws. For more information on web security, see the [OWASP Top Ten Project](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

## Steps
### **Before you begin, you need an app to scan**
In this lab, you will deploy a sample [Hello World application](https://github.com/GoogleCloudPlatform/python-docs-samples/tree/master/appengine/standard/hello_world) to run Security Scanner on. 

1. Run the following command in Cloud Shell to clone the Hello World sample app repository:
    ```sh
    git clone https://github.com/GoogleCloudPlatform/python-docs-samples
    ```
2. Then go to the directory that contains the sample code:
    ```sh
    cd python-docs-samples/appengine/standard/hello_world
    ```
### **Test App**
1. From within the hello_world directory where the app's [app.yaml](https://cloud.google.com/appengine/docs/standard/python/config/appref) configuration file is located, start the local development server with the following command:
    ```sh
    dev_appserver.py app.yaml
    ```
2. The local development server is now running and listening for requests on port 8080. Click on the web preview button in Cloud Shell, and select Preview on port 8080 to see it:


    (If you cannot see the web preview icon, close the Navigation menu, top left corner.)

3. Press Ctrl+c to stop the local app and return to the command line.

### **Deploy App**
1. Deploy your app to App Engine by running the following command from within the root directory of your application (hello_world):
    ```sh
    gcloud app deploy
    ```
2. You'll be asked to select a region. Choose the number for one that is near where you are.

3. After the app is created in your lab, you'll be asked if you want to continue. Click Y to continue.

4. Deployment of your app will then begin.

### **View App**
1. To launch the app in your browser, run the following command:
    ```sh
    gcloud app browse
    ```
There will be a link in Cloud Shell that you can use, or view the app at http://[YOUR_PROJECT_ID].appspot.com. This is the URL you'll scan for vulnerabilities and it will be added to your scan parameters in the next step.
### **Run the scan**
The scan does not run immediately, but is queued for later execution; it can take hours before the scan executes, depending on current load. For more information about these form settings, see [Using Cloud Security Scanner](https://cloud.google.com/security-scanner/docs/using-the-scanner).

1. Go to Navigation menu > App Engine > Security scans:
2. Click Enable API > Create scan.
3. Confirm that the URL for your app has been auto-populated in the Starting URLS field. Use all other default settings
4. Click Create to create the scan.
5. Click Run to start scanning

The scan will be queued, and you can watch the status bar progress as it scans. After a couple minutes, you should receive the following output:




