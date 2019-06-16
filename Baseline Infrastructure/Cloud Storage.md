# Cloud Storage
Allows storage and retrieval of data across the internet anytime anywhere using GCP cloud storage.

**Various uses :**
1. Serving Website content
1. Data Backup
1. Downloadable content
 
Primary storage Unit : Buckets

## **Create a Bucket**
1. Login to GCP
1. In the Console, go to **Navigation menu > Storage > Browser. Click Create Bucket:**
1. Select storage class 

    * Each bucket has a default storage class, which you can specify when you create your bucket.
        * Multi-region
        * Regional
        * Nearline
        * Coldline
1. Select region

____
 Bucket naming rules:

* Do not include sensitive information in the bucket name, because the bucket namespace is global and publicly visible.
* Bucket names must contain only lowercase letters, numbers, dashes (-), underscores (_), and dots (.). Names containing dots require verification.
* Bucket names must start and end with a number or letter.
* Bucket names must contain 3 to 63 characters. Names containing dots can contain up to 222 characters, but each dot-separated component can be no longer than 63 characters.
* Bucket names cannot be represented as an IP address in dotted-decimal notation (for example, 192.168.5.4).
* Bucket names cannot begin with the "goog" prefix.
* Bucket names cannot contain "google" or close misspellings of "google".
* Also, for DNS compliance and future compatibility, you should not use underscores (_) or have a period adjacent to another period or dash. For example, ".." or "-." or ".-" are not valid in DNS names.
___

## **Uploading Objects**
Drag files to the Drop section to place them in the bucket.
s
Or you can use the **Upload Files** option

Object names must be unique only within a given bucket

Attributes of an objectstored in the bucket 
* Name
* Size
* Type
* Storage-class
* Last modified
* Public access 
* Encryption : using Google managed key or key as customer managed or customer supplied
* Retention Expiration Date
* Holds - Temperoray/Event based hold on deletion

To share an object publically through a public URL we need to edit the permission and provide public access
* Go to Options > Edit Permissions
* Add a user Entity with allUsers for name and giver Reader access
* A public URL will now appear for the Object 

## **Create Folders**
You can either create a folder or upload an existing one.

## **To do so all in the cloud shell**

Use Tab to autocomplete Bucket name

1. Create a bucket
    ```
    gsutil mb gs://BUCKET_NAME/
    ```
2. Download a file to cloud shell
    ```
    wget --output-document FILE_NAME URL

    ```
3. Copy the file to the cloud bucket using the cp command
    ```
    gsutil cp FILE_NAME gs://BUCKET_NAME/
    ```
4. To download a file form the bucket to the shell
    ```
    gsutil cp -r gs://BUCKET_NAME/FILE_NAME LOCAL_PATH
    ```
5. Copy objects to folders in the same bucket    
    ```
    gsutil cp gs://BUCKET_NAME/FILE_PATH gs://BUCKET_NAME/DESTINATION_FOLDER/
    ```
6. List all the contents of a bucket
    ```
    gsutil ls gs://BUCKETNAME/[DIRECTORY_PATH/]    
    ```
6. List details of an object
    ```
    gsutil ls -l gs://BUCKETNAME/FILE_PATH    
    ```
7. Make project gloabally accessible
    ```
    gsutil acl ch -ENTITY_TYPE ENTITY_NAME:ACCESS_RIGHT gs://BUCKET_PATH
    ```
    acl - Access Control Mechanism

    ENTITY_TYPE :
    * User
    * Domain
    * Group
    * Project
    
    ENTITY_NAME : For all to access use 

    ACCESS_RIGHT: Owner or Reader
7. Remove public access
    ```
    gsutil acl ch -d ENTITY_NAME:ACCESS_RIGHT gs://BUCKET_PATH
    ```
8. Delete an object
    ```
    gsutil rm gs://BUCKET_PATH
    ```