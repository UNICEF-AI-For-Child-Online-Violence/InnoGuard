# InnoGuard

**N.B: More details and patches coming soon...**

InnoGuard is a child protection tool that provides protection for children by classifying violence against children through texts and audio, and determining age inappropriate images and links.

[![InnoGuard](./assets/innoguard_title.png)]()

## Table of Contents

- [InnoGuard Tools](#innoguard-tools)
    - [OCR Text Detection and Recognition](#ocr-text-detection-and-recognition)
    - [Safe Browsing](#safe-browsing)
    - [Tisane API](#tisane-api)
    - [Google Vision API](#google-vision-api)
    - [Google Speech API](#google-speech-api)
- [Usage](#usage)
    - [Configuration](#configuration)
    - [OCR Usage](#ocr-usage)
    - [Safe Browsing Usage](#safe-browsing-usage)
    - [Tisane API Usage](#tisane-api-usage)
    - [Google Vision Usage](#google-vision-usage)
    - [Google Speech Usage](#google-speech-usage)
- [Future Work](#future-work)
- [License](#license)
- [Links](#links)

## InnoGuard Tools

InnoGuards Overall Architecture is shown below.
[![InnoGuard-Architecture](./assets/Architecture_Diagram.jpg)]()

### OCR Text Detection and Recognition

Extracts text from images through screenshots.

Example WhatsApp Screenshot   |  OCR Text Extraction
:----------------------------:|:-------------------------:
![Ocr-Screenshot](./assets/ocr_screenshots_before.png)  |  ![Text-Extraction](./assets/ocr_screenshots_after.png)

### Safe Browsing

BrowserHistory Module and SafeBrowsing API are used to extract one’s browsing history from a user's local computer into a csv or pandas array for analysis of age inappropriate links.

The links are stored within a Mongo Database and are determined as **malicious** or not.

![Safe-browsing](./assets/safe-browsing.gif)

### Tisane API

Classifies violence against children [Cyberbulling, Sexual Comments and Harassment, Grooming, Emotional Abuse and Suicidal Tendencies] through texts.

Personal Attack  |  Death Threats  
:----------:|:----------:
![Personal-Attack](./assets/tisane_personal_attack_appearance.gif)  |  ![Death-Threats](./assets/tisane_personal_attack_death_threats.gif)  

Bigotry  |  Sexual Harassment
:----------:|:----------:
![Bigotry](./assets/tisane_bigotry.gif)  |  ![Sexual-Harassment](./assets/tisane_sexual_advances.gif)

### Google Vision API

Determines child inappropriate images.

![vision-api](./assets/racyimg.gif)

### Google Speech API

Allows audio analysis by turning speech to text.

The recorded audio is turned into text and then analysed through Tisane API for violence against children as shown below.

![speech-api](./assets/speechtotext.gif)


## Usage

### Configuration

#### Requirements:

*APIs Installation*: 

- To get your **Google API Key**, [click here.](https://developers.google.com/maps/documentation/maps-static/get-api-key)
- To get your **Tisane API Key**, [create an account by clicking here.](https://tisane.ai/signup/)
  - Then go to **API** or **[https://dev.tisane.ai/developer](https://dev.tisane.ai/developer)** to get your primary and secondary Tisane API keys.

*MongoDB Creation*:
- To create a Mongo Database, [click here.](https://www.mongodb.com/basics/create-database)

#### Project Installation:

**Step 1**\
To clone and run this application, you'll need [Git](https://git-scm.com) installed on your computer. From your command line:

```bash
# Clone this repository
git clone https://github.com/InnoGuard/InnoGuard.git

# Go into the repository
cd InnoGuard

```
Create new Python virtual environment [Optional]
- To get the commands to create your virtual environment, [click here.](https://uoa-eresearch.github.io/eresearch-cookbook/recipe/2014/11/26/python-virtual-env/)


```bash
# Upon activating the new virtual environment, at root directory, run
pip3 install -r requirements.txt

```

**Step 2 - Set up the Constants.py File**\
This is where your API keys are needed, as well as any necessities for the APIs.
Create a **Constants.py** file under the path scripts/libs/ with the content below:

```bash

GC_API_KEY = 'your_google_api_key_here'
MONGODB = "your_mongodb_address"

# Used for Google Vision API
likelihood_name = ('UNKNOWN', 'VERY_UNLIKELY', 'UNLIKELY', 'POSSIBLE',
                   'LIKELY', 'VERY_LIKELY')


TISANE_API_KEY_1 = 'primary_api_key'
TISANE_API_KEY_2 = 'secondary_api_key'

FILE_PATH = "local path to images and audio, for testing e.g. D:\pythonProjects\InnoGuard\"

```

**Step 3**\
The following demonstrates how to run the various aspects of InnoGuard after Setup.

### OCR Usage

- Open in Google Colab - https://colab.research.google.com/gist/rajeevratan84/45ca3d6c74175a204ca644ae1605daa4/ocr-on-screenshots
- Click on **Runtime**, then **Run all** or just press **Ctrl + F9**.

### Safe Browsing Usage

```bash

# From the root folder (InnoGuard), go to the Scripts Folder 
cd scripts

# Execute the following Python script:
python getBrowserHistory.py

# Output from this command will be displayed via the mongodb created.

```

### Tisane API Usage

```bash

# From the root folder (InnoGuard), go to the Scripts Folder 
cd scripts

# Execute the following Python script:
python text_detect.py

# A prompt to enter a sentence will appear:
# Example Sentence
You are gorgeous.

# Output from these commands will be displayed via the terminal.

```

### Google Vision Usage

```bash

# Attach an image called "test.png" to the root folder

# From the root folder (InnoGuard), go to the Scripts Folder
cd scripts

# Execute the following Python script:
python getImageResults.py

# A prompt to enter an Image Path will appear:
# Example of image path:
D:\uploads\test.png

# Output from these commands will be displayed via the terminal.

```

### Google Speech Usage

More coming soon...

This requires .wav files. To convert files, [click here!](https://cloudconvert.com/mp3-to-wav).

```bash

# Attach an audio .wav file called "test.wav" to the root folder

# From the root folder (InnoGuard), go to the Scripts Folder
cd scripts

# Execute the following Python script:
python speechToText.py

# Output from these commands will be displayed via the terminal.

```

## Future Work

The team at InnoGuard plans to implement:

- **Notification and Reporting System**: Upon identification, InnoGuard shall create a report of all instances mentioned above and send this report to the child’s parents or guardian via email or the police if the danger is high, with varying levels (colours) of danger and importance. 

- **Caribbean Lingo Dataset**: Currently, the APIs used to not consider Caribbean Lingo as shown in the gif below where it detects the Caribbean Phrase "Buss ah wine" as a person.
  - Thus, the new model would be emphasized and trained against Caribbean Speech Datasets to detect harmful Caribbean Lingo.

- **Chatbot Assistant**:  InnoGuard shall provide real-time emotional support via a chatbot to give tips and consolation.

## License

InnoGuard is licensed under the terms of the MIT Open Source license and is available for free.

## Links
* [YouTube Pitch](https://youtu.be/Ncit5I1Bsxo)
* Live Website Link Coming soon ...

