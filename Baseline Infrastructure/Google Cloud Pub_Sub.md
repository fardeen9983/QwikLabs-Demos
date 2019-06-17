# Google Cloud Pub/Sub

[Video: Simplify Event Driven Processing with Cloud Pub/Sub ](https://youtu.be/oKU2wbTXMTY)

Google Cloud Pub/Sub is a messaging service for exchanging event data among applications and services. A producer of data publishes messages to a Cloud Pub/Sub topic. A consumer creates a subscription to that topic. Subscribers either pull messages from a subscription or are configured as webhooks for push subscriptions. Every subscriber must acknowledge each message within a configurable window of time.

## Tasks
* Set up a topic to hold data.
* Subscribe to a topic to access the data.
* Publish and then consume messages with a pull subscriber.

## Steps
### Setting up Pub/Sub
You can use the Google Cloud Shell console to perform operations in Google Cloud Pub/Sub.

To use a Pub/Sub, you create a topic to hold data and a subscription to access data .published to the topic.

1. Click Navigation menu > Pub/Sub > Topics.
2. Click Create a topic.
3. The topic must have a unique name. For this lab, name your topic MyTopic. Append MyTopic to Name in the Create a topic dialog, then click CREATE.
### Add a subscription
Now you'll make a subscription to access the topic.

1. In the Topics dialog, for the topic you just made click the three dot icon > New subscription.
2. Type a name for the subscription, such as MySub, set the Delivery Type to Pull, then click Create.

### Publish a message to the topic
1. In the Topics dialog, for the topic you just made click the three dot icon > Publish message.
2. Enter Hello World in the Message field and click Publish.
   
### View the message
To view the message you'll use the subscription (MySub) to pull the message (Hello World) from the topic (MyTopic).

Enter the following command in command line.
```sh
gcloud pubsub subscriptions pull --auto-ack MySub
```
