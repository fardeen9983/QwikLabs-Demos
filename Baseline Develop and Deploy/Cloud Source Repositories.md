# Cloud Source Repositories
[Google Cloud Source Repositories](https://cloud.google.com/source-repositories/) provides Git version control to support collaborative development of any application or service. 

## Objective
* Create a local Git repository that contains a sample file, add a Google Source Repository as a remote, and push the contents of the local repository.
* Use the source browser included in Source Repositories to view your repository files from within the Google Cloud Platform Console.

## Steps
### Create a new repository
Start a new session in Cloud Shell and run the following command to create a new Cloud Source Repository named REPO_DEMO:
```sh
gcloud source repos create REPO_DEMO
```
### Clone the new repository into your Cloud Shell session
1. Clone the contents of your new Cloud Source Repository to a local repo in your Cloud Shell session:
    ```sh
    gcloud source repos clone REPO_DEMO
    ```
 The gcloud source repos clone command adds Cloud Source Repositories as a remote named origin and clones it into a local Git repository.

### Push to the Cloud Source Repository
1. Go into the local repository you created:
    ```sh
    cd REPO_DEMO
    ```
2. Run the following command to create a file myfile.txt in your local repository:
    ```sh
    echo "Hello World!" > myfile.txt
    ```
3. Commit the file using the following Git commands:
    ```sh
    git config --global user.email "you@example.com"

    git config --global user.name "Your Name"

    git add myfile.txt

    git commit -m "First file using Cloud Source Repositories" myfile.txt
    ```
4. Once you've committed code to the local repository, add its contents to Cloud Source Repositories using the git push command:
    ```sh
    git push origin master
    ```
    Git pushes the sample application files from the master branch to the origin remote:
    ```sh
    Counting objects: 3, done.
    Writing objects: 100% (3/3), 247 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To https://source.developers.google.com/p/qwiklabs-gcp-ba5b4dcd/r/REPO_DEMO
    * [new branch]      master -> master
    ```
### Browse files in the Google Cloud Source repository
Use the Google Cloud Source Repositories source code browser to view repository files. You can filter your view to focus on a specific branch, tag, or comment.

Browse the sample files you pushed to the repository by opening the Navigation menu and selecting Source Repositories > Source Code.

The console shows the files in the master branch at the most recent commit.