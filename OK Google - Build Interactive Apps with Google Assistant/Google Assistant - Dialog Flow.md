# Google Assistant: DialogFlow

## Overview
Google Assistant is a personal voice assistant that offers a host of actions and integrations. From sending texts and setting reminders, to ordering coffee and playing your favorite songs, the 1 million+ actions available suit a wide range of voice command needs. Google Assistant is offered on Android and iOS, but it can even be integrated with other devices like smartwatches, Google Homes, and Android TVs.

As you will soon find out, Actions is the central platform for developing Google Assistant applications. Actions work with a number of human-computer interaction suites, which simplifies conversational app development. Out of all the platforms, the most popular is Dialogflow, which uses an underlying machine learning (ML) and natural language understanding (NLU) schema to build rich Assistant applications.

In this lab you will get hands-on practice with Actions and Dialogflow by building an Assistant application that generates quotes when prompted by a user. You will gain practical knowledge of computer-human interaction suites and by the end of this lab, you will have successfully built a fully-fledged Google Assistant application.

## Objective 
* Differentiate between the basic components and services that make up an Assistant application.
* Create an Actions project.
* Integrate Dialogflow with an Actions project.
* Build a Dialogflow intent that handles quotation responses.
* Update your Google permission settings.
* Test your application with the Actions simulator.

## Steps
### **Create an Actions project**
Before we start building our quotation generator, let's review the following terms one more time.

Google Assistant is the virtual assistant that's found on smartphones, homes, and a host of other devices. It's the application that takes in voice commands and completes tasks based on user input.

Actions on Google is the developer platform that allows you to build applications for Google Assistant. This is going to be the central console for conversational application development.

Let's take our first step by building an Actions project.

1. Open a new tab in your browser and go to the Actions on Google Developer Console. Then sign in with your Qwiklabs credentials.
2. Click Add/import project and agree to Actions on Google's terms of service when prompted. Then click into the project field and select your Qwiklabs GCP project ID. Then click IMPORT PROJECT:

### **Set up Dialogflow**
1. From the left-hand menu click Build > Actions > ADD YOUR FIRST ACTION. Then select Custom Intent > BUILD. This will take you to the Dialogflow console.

2. Select your Qwiklabs account and click Allow when Dialogflow prompts you for permission to access your Google Account.

3. When you land on the Dialogflow page, check the box next to Yes, I have read and accept the agreement and click Accept
4. You will then be brought to the Dialogflow agent page. Click CREATE in the top right corner.

In the last few steps you were introduced to some new terms. Let's take a moment to review them:

* Action: an interaction built for Google Assistant that performs specific tasks based on user input.
* Intent: the goal of the Action (e.g. generate quotes). An intent takes user input and channels it to trigger an event.
* Agent (Dialogflow): a module that uses NLU and ML to transform user input into actionable data to be used by an Assistant application.
  
Here is a [*handy cheat sheet*](https://developers.google.com/actions/glossary) that you can reference if you run into any unfamiliar terms.

### **Build a custom Dialogflow intent**
1. From the left-hand menu select Intents and then click on CREATE INTENT in the top right corner.

2. This will bring you to a fresh Intent template that's ready to be filled in.

3. For the Intent name enter in Quote generator.

4. Then click on ADD TRAINING PHRASES and add the following user expressions:

    * Give me a quote.
    * How about a quote?
    * Give me some inspiration.
    * Supply me with a quote.
5. At the bottom in the Responses section click ADD RESPONSE. Now add the following Shakespeare quotes as Text responses (or feel free to add your own!):

    * If music be the food of love, play on.
    * This above all; to thine own self be true.
    * Some are born great, some achieve greatness, and some have greatness thrust upon them.
    * Love all, trust a few, do wrong to none.
    * The course of true love never did run smooth.
    * But if the while I think on thee, dear friend, all losses are restor'd and sorrows end.
6. Now click SAVE in the top right corner.
### **Check your Google Permission Settings**
To test the quote generator, you will need to enable the necessary permissions.

1. Go to the Activity Controls page and sign in with your Qwiklabs credentials if prompted.

2. Ensure that the following permissions are enabled by sliding the toggles and selecting TURN ON for the following cards:

    * Web & App Activity
    * Device Information
    * Voice & Audio Activity
    * Now close the Activity Controls page.
### **Test the quote generator**
1. Return to the Actions console and from the left-hand menu under the Test header click on Simulator:
2. Now go ahead and type in one of the training phrases (for example "Give me a quote") in the input box. You should receive one of the Shakespeare quotes that you added in the response section:
You can keep repeating this process—entering in one of the training phrases to get a random Shakespeare quote—as many times as you want!

>When we create an Intent, Dialogflow uses it's ML and NLU processing to auto generate prompts that are similar to the training phrases you entered in. This is a nice feature to have because your user's prompts don't have to exactly match your training phrases. This also simplifies development because you don't have to add every possible prompt to your training phrases—Dialogflow intelligently handles all of this behind the scenes.

3. To see this in action, type in a prompt that isn't in our training phrases (but still gets the same message across.) For example, try typing in new quote or more inspiration into the input box. You will be returned with a Shakespeare quote:


