**Compute:**

 houses a variety of machine types that support any type of workload. The different computing options let you decide how involved you want to be with operational details and infrastructure amongst other things.

**Storage:**

 data storage and database options for structured or unstructured, relational or non relational data.
Networking: services that balance application traffic and provision security rules amongst other things.

**Stackdriver:**

a suite of cross-cloud logging, monitoring, trace, and other service reliability tools.

**Tools:**

 services for developers managing deployments and application build pipelines.

**Big Data:**

 services that allow you to process and analyze large datasets.

**Artificial Intelligence:**

 a suite of APIs that run specific artificial intelligence and machine learning tasks on the Google Cloud platform.

 [Cloud Documentation](https://cloud.google.com/docs/overview/cloud-platform-services#top_of_page)

 **IAM**

 GCP also houses a collection of permissions and roles that define who has access to what resources. We can use the [Cloud Identity and Access Management (IAM)](https://cloud.google.com/iam/) service

 ## **Roles**

**Role Name**|**Permissions**
-|-
roles/viewer |Permissions for read-only actions that do not affect state, such as viewing (but not modifying) existing resources or data.
roles/editor |All viewer permissions, plus permissions for actions that modify state, such as changing existing resources.
roles/owner|All editor permissions and permissions for the following actions: Manage roles and permissions for a project and all resources within the project. Set up billing for a project.

[Documentation](https://cloud.google.com/iam/docs/understanding-roles#primitive_roles)


## **API**

[API design Guide](https://cloud.google.com/apis/design/)

 You can view API information by opening the navigation menu and clicking on **APIs & Services > Library**

 **[API Explorer QwikLabs](https://google.qwiklabs.com/focuses/4673?parent=catalog)**

 **[Googel API explorer](https://developers.google.com/apis-explorer/#p/)**

## **Cloud Shell**

**[Features](https://cloud.google.com/shell/docs/features)**

In the top-right corner of the console, click on the **Activate Cloud Shell** button and then click **Start Cloud Shell** if prompted:

Besides pre-installed toolkits, Cloud Shell also comes with the standard unix command line interface (CLI) tools and text editors like nano. We can use these to create and edit files right inside Cloud Shell.

**Commands**

[gcloud command line tool guide](https://cloud.google.com/sdk/gcloud/)

1. List out all users
    ```
    gcloud auth list
    ```
    Credentialed Accounts
ACTIVE  ACCOUNT
    googlefree125044_student@qwiklabs.net
    To set the active account, run:
    ```
    $ gcloud config set account `ACCOUNT`
    ```
    To take a quick anonymous survey, run:
    ```
    $ gcloud alpha survey
    ```
2.  gcloud config list project
    
    List out the projects with their IDs
2. Create a file
    ```
    touch test.txt
    ```
3. Fetch diles list in current directory
    ```
    ls
    ```
4. Edit files in nano editor
    ```
    nano test.txt
    ```

    To save the file hold **ctrl + X** and then press **Y** followed by **Enter**
5. Cat a similar command like nano

    *  View the contents of a file
        >cat test.txt
    * Write to a file
        >cat > test.txt