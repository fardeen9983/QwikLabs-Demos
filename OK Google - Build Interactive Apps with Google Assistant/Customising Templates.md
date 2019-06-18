# Google Assistant: Customizing Templates

## Overview
[Actions templates](https://developers.google.com/actions/templates/) allow you to build Google Assistant applications like trivia games or flashcard generators without writing a single line of code. You can integrate [Speech Synthesis Markup Language (SSML)](https://developers.google.com/actions/reference/ssml) to give your application more character and make responses seem more life-like. Google Assistant has also [added multilingual capabilities](https://techcrunch.com/2018/08/30/the-google-assistant-is-now-bilingual/), which allows you to expand your application to a much a wider audience.

In this lab, you will build a trivia Assistant application from an Actions template that utilizes SSML responses and multilingual capabilities. This will give your Assistant application unique sound effects and an option to be used in another language. You will add these features by leveraging GCP services like Cloud Storage and the Cloud Translation API and by the end you will have built a robust Assistant application.
## Objective
* Build an Assistant application with the flash cards template.
* Host custom MP3 files in Google Cloud Storage and integrate them with your Assistant application.
* Generate flash card questions and answers in different languages with the Cloud Translation API and add them to your template.
* Test your application and the features you added with the Actions simulator.

## Steps
### **Create an Actions project**
Regardless of the Assistant application you're building, you will always have to create an Actions project so your app has an underlying organizational unit.

1. Open a new tab in your browser and go to the Actions on Google Developer Console. 
2. Then sign in with your Qwiklabs credentials if prompted. 
3. Click Add/import project and agree to Actions on Google's terms of service when prompted. Then click into the project field and select your Qwiklabs GCP Project ID. Then click IMPORT PROJECT.
4. Scroll down and find the "More options" header. Then click on the Templates card.

### **Add the Flash cards template**
1. From the three options of templates, select Flash cards. You have now added a flash card template as an Action to your project.

2. In the Personality section, listen to the personality options. Select the one you like the most and click Next.

3. Now that you're in the content section, click the GET STARTED button and then click the link to the Flash Cards Template sheet. Then click Make a copy when prompted.
4. Now add the following questions, answers, and hints to the bottom of this spreadsheet:
   
    Question|Answer|Hint
    -|-|-
    What's the baby animal name for Bat?|pup|This is similar to a baby dog.
    What's the baby animal name for Cow?|calf|This baby animal name starts with a "C".
    What's the baby animal name for Snake?|hatchling|This name is the same as a baby alligator.

These will be rows 39-41 in the spreadsheet. Now that you've added some new flashcard questions, you will learn how to integrate custom sounds with your Actions template. Keep this Google Sheet tab open.
### **Create a Cloud Storage bucket**
For this part of the lab you are going to switch gears and work with Google Cloud Storage so you can host custom sound effects used by the application.

The flashcard template has [additional configuration parameters](https://developers.google.com/actions/templates/flash-cards#configuration_parameters) that we can use to make our application more personalized. In this section we will be working on integrating our own sounds for AudioGameIntro, AudioGameOutro, and AudioDing parameters.

1. If you haven't already, head over to the Google Cloud Platform console and login with your Qwiklabs credentials.

2. Once there, open the navigation menu and click Storage > Browser > Create bucket. 
3. Enter in a [unique name](https://cloud.google.com/storage/docs/naming) for your bucket and keep all the other default settings the way they are. 
4. Then click Create:
### **Copy MP3 files to your Cloud Storage bucket**
The [Youtube Audio Library](https://www.youtube.com/audiolibrary/music) lets you browse and download royalty free music and sound effects. [Learn more](https://support.google.com/youtube/answer/3376882?hl=en&visit_id=636776560337099470-1576632230&rd=1) about the YouTube Audio Library and read the terms of service below:

Three MP3 sample files have been downloaded from the Youtube Audio Library and are stored in a Cloud Storage bucket. You will now copy these files to the Cloud Storage bucket you just created.

1. Start a new session in Cloud Shell and run the following commands to copy and unzip the MP3 file folder into your home directory:
    ```sh
    gsutil cp gs://spls/gsp280/gsp280-mp3-files.zip .
    unzip gsp280-mp3-files.zip
    ```
2. Now copy the unzipped folder to your Cloud Storage bucket by running the following command, replacing <YOUR_BUCKET_NAME> with the name of your Cloud Storage bucket:
    ```sh
    gsutil cp -r gsp280-mp3-files gs://<YOUR_BUCKET_NAME>
    ```
    You should receive a similar following output:
    ```
    Copying file://gsp280-mp3-files/.DS_Store [Content-Type=application/octet-stream]...
    Copying file://gsp280-mp3-files/Banjo_Short.mp3 [Content-Type=audio/mpeg]...
    Copying file://gsp280-mp3-files/Beep_Short.mp3 [Content-Type=audio/mpeg]...
    Copying file://gsp280-mp3-files/Country_Cue_1.mp3 [Content-Type=audio/mpeg]...
    | [4 files][  1.1 MiB/  1.1 MiB]
    Operation completed over 4 objects/1.1 MiB.
    ```
### **Add MP3 files to the template**
1. Go back to your Copy of Flash Cards Game sheet (where you previously added three new trivia questions and answers.) 
2. At the bottom of the page find and click the Configuration tab. Now add the following values to the Key column:

   * AudioGameIntro
   * AudioGameOutro
   * AudioDing
   * 
3. For the values you will be using the MP3 files that you uploaded to Cloud Storage. Run through the following steps to add the MP3 files as configuration parameter values:

* In your Cloud Storage bucket click on the name Banjo_Short.mp3. This will open an audio player in a new tab.

* Copy the URL.
* Paste the URL in for the AudioGameIntro value in Copy of Flash Cards Game.

Once that's done:

* In your Cloud Storage bucket click on the name Country_Cue_1.mp3. This will open an audio player in a new tab.
* Copy the URL.
Paste the URL in for the AudioGameOutro value in the Copy of Flash Cards Game.

Finally:

* In your Cloud Storage bucket click on the name Beep_Short.mp3. This will open an audio player in a new tab.
* Copy the URL.
* Paste the URL in for the AudioDing value in the Copy of Flash Cards Game.

### **Build and test your Action**
1. Once you're finished modifying the sheet, copy the url of Copy of Flash Cards Game and return to the Actions console. 
2. Click Next and paste in the URL for the Copy of Flash Cards Game Sheet that you've been editing. Then click Upload. Your sheet will be validated
3. Click on the CREATE APP button. Actions is now building an Assistant application from the trivia spreadsheet. It might take a couple minutes for the application to build. You can move on to the next step in the meantime.

### **Check your Google permission settings**
To test the Action, you need to enable the necessary permissions.

1. Go to the Activity Controls page and sign in with your Qwiklabs credentials if prompted.

2. Ensure that the following permissions are enabled by sliding the toggles and selecting TURN ON for the following cards:

    * Web & App Activity
    * Device Information
    * Voice & Audio Activity
   Now close the Activity Controls page.

### **Test the application with the Actions simulator**
1. Return to the Actions console and verify that your application has been built. 
2. Click on the GO TO SIMULATOR button. This will bring you to the Actions Simulator page, where you can test your Assistant application without the need of a device like a Google Home.

3. Be sure to use headphones or turn up the volume on your speakers to hear the the new MP3 samples you just added!

4. To invoke the Action, hit enter in the Talk to my test app box near the bottom of the simulator console. You will be asked if you want to play a round of flashcards:
    
You should hear Banjo_Short.mp3 play after "Alright. Getting the test version of my test app". Now enter Yes when prompted if you are ready to play. You will then be given a baby animal flashcard:

You should have heard Beep_Short.mp3 play after the "What's the baby animal name for ?" Go through the short Flashcard game, answering the questions to the best of your abilities.

At the end you will be prompted with "Would you like to go forth to another set?" Enter in No and hit enter. After some brief dialogue, you will hear the AudioGameOutro loop Country_Cue_1.mp3.

By using the Youtube Audio Library and Cloud Storage you were able to add custom MP3 files to your Assistant application, which gives it a unique, personalized touch.

### **Add a flashcard template in another language**
Now that you've gotten hands-on practice integrating audio files with your Assistant application, you will take it to the next level by adding a version in another language.

1. In the Actions console, select Build > Actions from the left-hand menu.

2. Click the Modify languages button in the top right corner. Select Spanish and then click Save in the top right corner.

3. Now click Actions from the left-hand menu. Your flash card Action should now resemble the following (note the Spanish tab)
4. Click on the Spanish language tab and select Beeps the Robot as your personality. Then click Next.

5. Now that you are in the content section, click the GET STARTED button and then click the link to the Flash Cards Template sheet. Then click Make a copy when prompted. You should now be on the following Sheets (es) page:

### **Enable the Translation API**
To keep our application versions consistent with one another, we will need to translate the three trivia questions we added to the English template to Spanish. You will use the Cloud Translation API to accomplish this.

1. Return to the GCP console. From the Navigation menu select APIs & Services > Library.

2. Then search for the Cloud Translation API and select the API from the results. If the API is disabled, enable it. Your page should resemble the following:

### **Create a service account key**
Before we can use the Cloud Translation API, we will need to create a service account key.

1. Open the Navigation menu and select APIs & Services > Credentials. Then click the Create credentials dropdown menu and select Service account key.

2. From the Service account drop down menu select New service account. For the service account name, type in a translation-api. For the role field, select Project > Editor.

3. Once filled in, click Create
   
    The service account key will now be downloaded to your local machine as a JSON file. Note the file's location.

### **Test Completed Task**
Click Check my progress to verify your performed task.

### **Create a service account key**
1. Open up a Cloud Shell session and in the right-hand corner select the menu item (three dots) and click Upload file.

2. Select the JSON service account file that you downloaded in the previous step (name should resmble qwiklabs-gcp-xxxxxxxxxxxxxxxx-xxxxxxxxxx.json) and click Open. You now have your service account key in the right place and you are ready to use it with the translation API.

3. Run the following command in Cloud Shell to get the complete path to your service account file, replacing <YOUR-SERVICE-ACCT-KEY> with the file's name:
    ```sh
    readlink -f <YOUR-SERVICE-ACCT-KEY>
    ```
    Your output should resemble the following:
    ```sh
    /home/gcpstaging22049_student/qwiklabs-gcp-8dd23d7d0eeec9e7-209abe66b302.json
    ```
4. Now run the following command to set the environment variable GOOGLE_APPLICATION_CREDENTIALS to the path of the service account key. Replace [PATH] with the output of the previous step:
    ```sh
    export GOOGLE_APPLICATION_CREDENTIALS="[PATH]"
    ```
5. Use the Translation API
6. Now that your service account credentials are in the proper place, you are ready to make translation API requests. You will be translating the English flash card questions we added earlier into Spanish.

    Be sure to keep your Copy of Flash Cards Game (es) sheet handy since you will be copying text that is outputted from the translation API and adding it to the sheet. Here are the questions and answers that we added before:

    Question|Answer|Hint
    -|-|-
    What's the baby animal name for bat?|pup|This is similar to a baby dog.
    What's the baby animal name for cow?|calf|This baby animal name starts with a "C".
    What's the baby animal name for snake?|hatchling|This name is the same as a baby alligator.

7. Run the following command in Cloud Shell to translate the flash card questions into Spanish using the Cloud Translation API:
    ```sh
    curl -X POST \
        -H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
        -H "Content-Type: application/json; charset=utf-8" \
        --data "{
    'q': 'What\'s the baby animal name for bat?',
    'q': 'What\'s the baby animal name for cow?',
    'q': 'What\'s the baby animal name for snake?',
    'target': 'es'
    }" "https://translation.googleapis.com/language/translate/v2"
    ```
    You should receive the following output:
    ```json
    {
        "data": {
            "translations": [
            {
                "translatedText": "¿Cuál es el nombre del animalito para el murciélago?",
                "detectedSourceLanguage": "en"
            },
            {
                "translatedText": "¿Cuál es el nombre del animalito para la vaca?",
                "detectedSourceLanguage": "en"
            },
            {
                "translatedText": "¿Cuál es el nombre del animalito para serpiente?",
                "detectedSourceLanguage": "en"
            }
            ]
        }
    }
    ```
    And just like that your questions have been translated from English to Spanish! You will notice that the output doesn't exactly match the questions in the spreadsheet, but that's not much of a concern since these translations are still grammatically correct.

1. Go ahead and copy over your newly translated questions (translatedText fields in the output) and add them as three new rows to the Question column in the Copy of Flash Cards (es) sheet.

2. Now run the following command in Cloud Shell to translate the answers:
    ```sh
    curl -X POST \
        -H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
        -H "Content-Type: application/json; charset=utf-8" \
        --data "{
    'q': 'pup',
    'q': 'calf',
    'q': 'hatchling',
    'target': 'es'
    }" "https://translation.googleapis.com/language/translate/v2"
    ```
    You should receive the following output:
    ```json
    {
        "data": {
            "translations": [
            {
                "translatedText": "cachorro",
                "detectedSourceLanguage": "en"
            },
            {
                "translatedText": "becerro",
                "detectedSourceLanguage": "en"
            },
            {
                "translatedText": "cría",
                "detectedSourceLanguage": "en"
            }
            ]
        }
    }
    ```
3. Copy those values into their respective Answer columns. Now run the following command to translate the Hint values:
    ```sh
    curl -X POST \
        -H "Authorization: Bearer "$(gcloud auth application-default print-access-token) \
        -H "Content-Type: application/json; charset=utf-8" \
        --data "{
    'q': 'This is similar to a baby dog.',
    'q': 'This baby animal name starts with a C.',
    'q': 'This name is the same as a baby alligator.',
    'target': 'es'
    }" "https://translation.googleapis.com/language/translate/v2"
    ```
    You should receive the following output:
    ```json
    {
        "data": {
            "translations": [
            {
                "translatedText": "Esto es similar a un perro bebé.",
                "detectedSourceLanguage": "en"
            },
            {
                "translatedText": "Este nombre animal de bebé comienza con una C.",
                "detectedSourceLanguage": "en"
            },
            {
                "translatedText": "Este nombre es lo mismo que un cocodrilo bebé.",
                "detectedSourceLanguage": "en"
            }
            ]
        }
    }
    ```
5. Copy those values into the Hints column. The bottom of your spreadsheet should now resemble the following:

By leveraging the Translation API, you were able to convert your questions, answers, and hints into another language (and all from Cloud Shell!) As you continue building more intricate Assistant applications, you will begin to see just how important and necessary APIs are for accessing external services and data.

### **Build the Action**
Now that you're done modifying the sheet, copy the URL of Copy of Flash Cards Game (es) and return to the Actions console. You should have left off on the following page:

1. Click Next and enter in the URL for the Copy of Flash Cards Game (es) sheet that you've been editing. Then click Upload. Your sheet will be validated 
2. Now click the CREATE APP button. Actions is now building an Assistant application from the Spanish trivia spreadsheet. It might take a couple minutes for the application to build, be patient.
3. Once your application has been built successfully, your page should resemble the following:

### **Test the application**
1. Now click on the GO TO SIMULATOR button. This will bring you to the Actions Simulator page, where you can test your Assistant application without the need of a device like a Google Home.

2. To invoke the Action, type enter in the Hablar con mi aplicación de prueba box near the bottom of the simulator console. When prompted to begin, enter in Sí:
3.You will be prompted with an animal baby flashcard in Spanish:

3. You can go through the baby animal flash cards in Spanish if you are up to the challenge or you can end your lab here.