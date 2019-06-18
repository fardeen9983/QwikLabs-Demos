# Google Assitant : Templates

[Google Assistant](https://assistant.google.com/#?modal_active=none) is a personal voice assistant that offers a host of actions and integrations. From sending texts and setting reminders, to ordering coffee and playing your favorite songs, the 1 million+ actions available suit a wide range of voice command needs. Google Assistant is offered on Android and iOS, but it can even be integrated with other devices like smartwatches, Google Homes, and Android TVs.

As you will soon find out, [Actions](https://developers.google.com/actions/extending-the-assistant) is the central platform for developing Google Assistant applications. Actions work with a number of human-computer interaction suites, which simplifies conversational app development. [Actions templates](https://developers.google.com/actions/templates/) allow you to build custom Assistant applications within minutes—an ideal choice to get up and running quickly.

In this lab you will get hands-on practice with Actions and templates by building an Assistant application that generates trivia questions. You will gain experience with the fundamentals of this computer-human interaction suite and by the end you will have built a fully-fledged Google Assistant application.

## Tasks
* Differentiate between the basic components and services that make up an Assistant application.
* Create an Actions project.
* Integrate templates with an Actions project.
* Customize templates with Google Sheets.
* Build a trivia generator Assistant application using all that you've learned.

## Steps
### **Create an Actions Project**
Before we start building our trivia application, let's review the following terms one more time:

Google Assistant is the virtual assistant that's found on smartphones, homes, and a host of other devices. It's the application that takes in voice commands and completes tasks based on user input.

Actions on Google is the developer platform that allows you to build applications for Google Assistant. This is going to be the central console for conversational application development.

Let's take our first step by building an Actions project.

1. Open a new tab in your browser and go to the [Actions on Google Developer Console](http://console.actions.google.com/). Then sign in with your Qwiklabs credentials. 
2. Click Add/import project and agree to Actions on Google's terms of service when prompted. Then click into the project field and select your Qwiklabs GCP project ID. Then click IMPORT PROJECT

### **Add a Template to the Actions Project**
1. Scroll to the bottom of the welcome page and select the Templates card. Then select Trivia from the template options. You have now added a Trivia Template as an Action to your project.

2. Now click Actions from the left-hand menu (under the BUILD category). An Action is an interaction built for Google Assistant that performs specific tasks based on user input. You should see the Trivia Action instantiated 
3. In the Personality section, listen to the personality options. Select the one you like the most and click Next.

4. Now that you're in the content section, select UPLOAD SHEET > Make a copy of the pre-filled Google Sheet for editing > Make a copy. 

### **Customizing Templates**
Take a moment to familiarize yourself with the sheet. Note the column values, particularly the question, correct answer, and incorrect answer columns.

The template allows us to create multiple choice questions as well as true/false trivia (note the Wikipedia question in the final row.)

 Let's we add a few of our own questions. 
1. Add the following Trivia questions to the sheet:

    Question|Correct Answer|Incorrect Answer 1|Incorrect Answer 2
    -|-|-|-    
    How many bones does an adult human have?|Two hundred and six|One hundred and twelve|One hundred and fifty two
    What is Buenos Aires the capital of?|Argentina|Spain|Brazil
    What country eats the most chocolate, which comes to about 10 kilos per person per year?|Switzerland|Italy|France
    What country covers 50% of the South American continent?|Brazil|Argentina|Chile
3. Once those are filled in, select the Configuration tab at the bottom of the page. You should now be on the following page:
4. Change the Title value to Templates Trivia Game. Change the QuestionsPerGame value to 5.

4. Once you're finished modifying the sheet, return to the Actions console. 
5. Click Next and enter in the URL for the "Copy of Trivia Game Multiple Choice" Sheet that you've been editing. Then click UPLOAD. 
6. Click on the CREATE APP button. Actions is now building an Assistant application from the trivia spreadsheet. It might take a couple minutes for the application to build—feel free to move on to the next step in the meantime.

### **Check your Google Permission Settings**
To test the trivia application, you will need to enable the necessary permissions.

1. Go to the Activity Controls page and sign in with your Qwiklabs credentials if prompted.

2. Ensure that the following permissions are enabled by sliding the toggles and selecting TURN ON for the following cards:

   * Web & App Activity
   * Device Information
   * Voice & Audio Activity
   * Now close the Activity Controls page.
### **Test the Application**
Back in the Actions console, verify that your application has been built. 


1. Click on the TEST ACTION button. This will bring you to the Actions Simulator page, where you can test your Assistant application without the need of a device like a Google Home.

    Note: turn your volume up or try using headphones to hear your Google Assistant speak to you!
2. To invoke the Action, type enter in the Talk to my test app box near the bottom of the simulator console. You will the be prompted to answer one of the Trivia questions from the spreadsheet, which will resemble the following:
3. Go through the five question trivia quiz and answer the questions to the best of your abilities. Once you get through the five questions, the questions should end and you should get a score back
4. You can go through another round of trivia by entering Yes or exit the session by entering in No.
