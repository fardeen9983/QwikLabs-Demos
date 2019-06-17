# StackDriver
Stackdriver Monitoring provides visibility into the performance, uptime, and overall health of cloud-powered applications. Stackdriver collects metrics, events, and metadata from Google Cloud Platform, Amazon Web Services, hosted uptime probes, application instrumentation, and a variety of common application components including Cassandra, Nginx, Apache Web Server, Elasticsearch, and many others. Stackdriver ingests that data and generates insights via dashboards, charts, and alerts. Stackdriver alerting helps you collaborate by integrating with Slack, PagerDuty, HipChat, Campfire, and more.

## Task :
Monitor a Google Compute Engine virtual machine (VM) instance with Stackdriver

## Steps

### Create a Compute engine instance
1. In the GCP Console dashboard, go to Navigation menu > Compute Engine > VM instances, then click Create.
2. Fill in the fields as follows, leaving all other fields at the default value:

    Name: lamp-1-vm

    Region: us-central1 (Iowa) or asia-south1 (Mumbai)

    Zone: us-central1-a or asia south1-a

    Machine type: n1-standard-2

    Firewall: Select Allow HTTP traffic
3. Click Create.

### Add Apache2 HTTP Server to your instance
1. In the Console, click SSH to open a terminal to your instance.
2. Run the following commands in the SSH window to set up Apache2 HTTP Server:
    ```sh
    sudo apt-get update
    sudo apt-get install apache2 php7.0
    sudo service apache2 restart
    ```
3. Back in the console, on the VM instances page, is the External IP for lamp-1-vm instance. Click the link to see the Apache2 default page for this instance.

### Create a Stackdriver account
To use Stackdriver, your project must be in a Stackdriver account.
1. In the Google Cloud Platform Console, click on Navigation menu > Monitoring.
Your Stackdriver workspace will be ready when you see the Stackdriver dashboard.
2. Click Install Agents in the top banner. Run the commands shown on screen in the SSH window to install the Stackdriver monitoring agent and Stackdriver logging agent for your instance.
    ```sh
    curl -sSO https://dl.google.com/cloudagents/install-monitoring-agent.sh
    sudo bash install-monitoring-agent.sh

    curl -sSO https://dl.google.com/cloudagents/install-logging-agent.sh
    sudo bash install-logging-agent.sh
    ```
### Create an uptime check
Uptime checks verify that a resource is always accessible. In this lab, for practice, you create an uptime check to verify the Google website is up.
1. On the Stackdriver console click Create Check button on the dashboard. You can also go to Uptime Checks in the left-hand menu, then select Uptime Checks Overview and then click Create an Uptime Check on the new page.
2. Edit the New Uptime Check panel by adding the following:

    Title: Lamp Uptime Check

    Check type: HTTP

    Resource Type: Instance

    Applies to: Single, lamp-1-vm

    Path: leave at default

    Check every: 1 min

    Note: if the instance doesn't auto-populate after selecting "single", Cancel this uptime check, refresh the Stackdriver page and try again.
3. Click Test to verify that your uptime check can connect to the resource.

4. When you see a green check mark everything can connect. Click Save.

5. Click No thanks to create an alerting policy for this check.

The uptime check you configured takes a while for it to become active. Continue with the lab, you'll check for results later. While you wait, create an alerting policy for a different resource.

### Create an alerting policy
Use Stackdriver to create one or more alerting policies.

In the Stackdriver console, refresh your screen.

1. In the left menu, click Alerting > Create a Policy. You'll next configure Conditions, Notifications, and Documentation.
2. Conditions: click Add Condition.
    Set the following in the panel that opens, leave all other fields at the default value.

    Target Start typing "GCE" in the resource type and metric field, then select:

    Resource Type: GCE VM Instance (gce_instance)

    Metric: Type "network" then select Network traffic
3. Configuration

    Condition: is above

    Threshold: 500 bytes

    For: 1 minute

    CLick save
3. Notifications: Select Email Address, then enter your personal email address in the Email field.
4. Documentation: Add a message in documentation, which will be included in the emailed alert.
5. Name this policy: type the name Inbound Traffic Alert.
Click Save.
### Create a dashboard and chart
You can display the metrics collected by Stackdriver Monitoring in your own charts and dashboards. In this section you create the charts for the lab metrics and a custom dashboard.
1. In the left-hand menu of Stackdriver Monitoring Console, select Dashboards > Create Dashboard.

2. Click Add Chart in the upper right of the screen.

3. Click into the Find resource type and metric field and start typing "CPU", then select CPU Load (1m).
   
   The GCE VM instance is automatically selected as the Resource type. The chart names itself after the metric you're using, but you can rename it whatever you want.
4. Click save
   
#### Now create a second chart.

1. Select Add Chart in the upper-right menu of the new dashboard.
2. In the Find resource type and metric field start typing "Network", then choose "Received Packets". Leave the other fields with their default values. You see the chart data in the Preview section.

3. Click Save.

4. You still need to name your new Dashboard! Change Untitled Dashboard to Stackdriver LAMP Qwik Start Dashboard.

### View your logs
Stackdriver Monitoring and Stackdriver Logging are closely integrated. Check out the logs for your lab.

In the Stackdriver left-hand menu, click Logging to see the Logs Viewer. Now change the focus to see the logs you want:
* Select GCE VM Instance > lamp-1-vm in the first drop-down menu.
* Select syslog in the second drop-down menu, and click OK.
* Leave the other fields with their default values.
* Click the Start streaming logs icon.

### Check out what happens when you start and stop the VM instance.
1. Click and move the Logs Viewer browser tab so that the Compute Engine console and the Stackdriver Logging console are side by side. 
2. In the Console, in the VM instance window, click on the lamp-1-vm instance.

3. In the VM instance details window and click Stop at the top of the screen, and then confirm to stop the instance. It will take a few minutes for the instance to stop.

4. Watch in the Logs View tab for when the VM is stopped.

5. In the VM instance details window, click Start at the top of the screen, and then confirm. It will take a few minutes for the instance to re-start. Watch the log messages to monitor the start up.
6. Check the uptime check results and triggered alerts
Time to check the uptime check results and see if alerts have been triggered!

### Check the uptime check results in Stackdriver
1. In the left pane, click Uptime Checks > Uptime Check Overview. This view provides information about all active uptime checks, including the status of web site at different locations.
2. Click the name of the uptime check.
If you see in Location results the message "No checks have run yet", wait a few minutes and refresh your page.

### Check if alerts have been triggered
1. In the Stackdriver console, in the left page click Alerting > Incidents. If you don't see an open incident, be sure you look in the RESOLVED tab.

2. Still in the Stackdriver console, click Alerting > Events. You should see a number of Events listed.

3. Check your email account. You should see Stackdriver Alerts.

## Google Cloud Training & Certification

...helps you make the most of Google Cloud technologies. [Our classes](https://cloud.google.com/training/courses) include technical skills and best practices to help you get up to speed quickly and continue your learning journey. We offer fundamental to advanced level training, with on-demand, live, and virtual options to suit your busy schedule. [Certifications](https://cloud.google.com/certification/) help you validate and prove your skill and expertise in Google Cloud technologies.