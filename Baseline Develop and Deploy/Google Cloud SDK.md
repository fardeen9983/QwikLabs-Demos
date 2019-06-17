# Google Cloud SDK
[Video : Cloud SDK - Essential Command-Line Tools for Google Cloud Platform](https://youtu.be/69MdTXgA6Ws)

## Objective
Install Google Cloud SDK to a virtual machine, initialize it and run core gcloud commands from the command-line.

## Steps
### Set up a VM to use
Create a VM with either Centos or Redhat. You can choose which one to use, the steps will be the same.

1. In the GCP Console, go to Compute Engine > VM instances, then click Create.
2. In the Boot disk section, click Change to begin configuring your boot disk:
3. Choose CentOS7, then click the Select button.
4. In the Firewall section, select Allow HTTP traffic.
5. Click Create.
6. Click on the SSH button for your instance.
   
### Update the Cloud SDK RPM packages
The Cloud SDK RPM packages are supported for Red Hat Enterprise Level 7 and CentOS 7. They may also work on Fedora systems using yum or dnf, but this has not been tested.

Run the following in the SSH window to set up Google Cloud SDK:
```sh
# Update YUM with Cloud SDK repo information:
sudo tee -a /etc/yum.repos.d/google-cloud-sdk.repo << EOM
[google-cloud-sdk]
name=Google Cloud SDK
baseurl=https://packages.cloud.google.com/yum/repos/cloud-sdk-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
       https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOM

# The indentation for the 2nd line of gpgkey is important.

# Install the Cloud SDK
sudo yum install google-cloud-sdk
```
### Initialize the SDK in your instance
Use the gcloud init command to perform several common SDK setup tasks. These include authorizing the SDK tools to access Google Cloud Platform using your user account credentials and setting up the default SDK configuration.

To initialize the SDK, run the following:
```sh
gcloud init --console-only
```
Note: This prevents the gcloud init command from launching a web browser. Choose option 2, to log in with a new account.

You will get confirmation that you're running on virtual machine. Type Y to allow the credentials you logged into the lab with (this is your personal account for this lab) to be used to authenticate your account.

Type the number for adding a new account.

You'll then be asked to confirm that you want to use your personal account, which is the lab cedentials you're using right now. All you need to do is type Y to confirm.

You'll be given a long URL click on it or paste it into paste into a new browser. You may be asked to select your lab credials again, and Allow access to your account.

This URL will give you your authentication code. Copy the code and paste it into the SSH window at the command prompt, then press Enter.

Now type the number corresponding to you GCP Project ID.

### Run core gcloud commands
Run these gcloud commands to view information about your SDK installation:

List accounts whose credentials are stored on this VM:
```sh
gcloud auth list
```

This command will list the properties in your active SDK configuration:
```sh
gcloud config list
```

Run the following to view information on your Cloud SDK installation and the active SDK configuration:
```sh
gcloud info
```

The summary includes information about:

* your system
* the installed SDK components
* the active user account and current project
* the properties in the active SDK configuration

You can see information about gcloud commands and other topics from the command line by running the following:
```sh
gcloud help
```

In Help you can specify a command. For example, the help for gcloud compute instances create wold be this:
```sh
gcloud help compute instances create
```
