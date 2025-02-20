# Discord-bot-that-utilizes-fifteen.ai
This is a python discord bot that utilises POST requests made to https://fifteen.ai/app/getAudioFile5 which responds with links to wav files that are posted onto the server,  which can then be called via a GET request to https://cdn.15.ai/audio/XYZ.wav.

# Prerequisites
To use the voice-chat based features, you will also need to install ffmpeg: https://ffmpeg.org/download.html 

If you would prefer not to, you can remove the 2 phrases within the `characters.json` file starting with "Hey X, in VC, say " to prevent accidental usage.

# Installation 
1. Clone/ download the repo
2. Edit the file named "Tokenconfig.json" file found within the program's location (default location is in the root directory)

3. Get the keys/ tokens from the following site to use a bot: https://discord.com/developers/applications

4. In `TokenConfig.json`, enter the following: 
```json
{
  "Token": "Your Discord bot token",
  "Prefix": ";",
  "CharacterInfoFile": "C:\\ProgramLocation\\characters.json",
  "SingleAudiofilepath": "C:\\Test Directory\\"
}
```

# Custom API configuration:
1. Add a new quote to the `characters.json` file and add the following:
```json
{
  "Phrase": "Custom Quote",
  "Character": "Character (Exact reference)",
  "Function": "2",
  "Emotion":"Neutral",
  "APIReference":"CustomAPIReference"
}
```

3. Go to the `CustomAPIConfig.json` file and create a new object. 
4. Enter in the relevant information as follows:

```json
{
  "ObjectReference":"API reference to use in the character.json file ",
  "ReqType":"GET",
  "BaseAPICall":"APICall{0}",
  "OutputType":"JSON or XML",
  "JSONPath":"JSON.Path[0].Value1",
  "XMLPath":"XPath"
},
```

5. If you want the text after the quote to be used within the API simalar to that of the one used for the wikipedia API. Add A "{0}" into the string for it to be replaced by the text entered afterwards.

6. Example uses of a custom API are below:

* "Hey GLaDOS, give me a random quote" (Will call the 1st custom API listed within the customAPIconfig file, in order to make sure that the single call can be made, white space after it must be trimmed in the character quote section)
* "Hey GLaDOS, Give me an extract from a bibliography" (Will call the 2nd custom API listed within the customAPIconfig file)
* "Hey GLaDOS, give me a random quote about technology" (Will call the 3rd custom API listed within the customAPIconfig file.)

# Custom command phrases
1. Open the file named `characters.json`
2. Edit the "Phrases" object array to include another object to hold your information, below are what each "function" correlates to also:

* **Make sure that if the object you are adding is within or at the end of the array, that it either has "," after the obect or doesn't have it if it is at the end and that a "," is added to the previous object**

  '0'. Simple pass of the message text into 15.ai
  
  '1'. Passes message text to wikipedia API and outputs the wikipedia API extract.
  
  '2'. Uses a refered custom API output to make a request to 15.ai (see above for configuration)

  '3'. Will pass a message to 15.ai, get the audio response and play the audio in a voice chat.

* JSON for uses of functions 0/1/3

```json
{
  "Phrase": "Command phrase that will be said in discord message ",
  "Character": "Character (Exact reference)",
  "Function": "0/1/3",
  "Emotion":"Emotion"
},
``` 

 * JSON for using function 2, if the custom API is not using the rest of the message, trim the trailing space from the phrase
 
 ```json
{
  "Phrase": "Command phrase that will be said in discord message ",
  "Character": "Character (Exact reference)",
  "Function": "2",           
  "Emotion":"Emotion",
  "APIReference":"Custom API Reference string"
}
 ```

3. Save the file.

## Example uses of a custom API are below:

* "Hey GLaDOS, give me a random quote" (Will call the 1st custom API listed within the customAPIconfig file, in order to make sure that the single call can be made, white space after it must be trimmed in the character quote section)

* "Hey GLaDOS, Give me an extract from a bibliography" (Will call the 2nd custom API listed within the customAPIconfig file)

* "Hey GLaDOS, give me a random quote about technology" (Will call the 3rd custom API listed within the customAPIconfig file.)

* "bot join vc" Makes the bot join the current voice channel the user is in.

* "bot leave vc" Makes the bot leave the current voice channel the user is in.

* "Hey GLaDOS, in VC, say " (If in a voice chat, the converted text you enter into the message will be played in the voice chat)
  * The above requires the bot to currently be in a voice channel using the above join/ leave command messages.

# What commands I will probably try to do:

[Done] "Hey x, say y"

[Done] "Hey x, tell me about" (retrieves a section of a wikipedia page and says it)

[To be done] "Hey x, [question] Text/ link to text/pdf link" 
Example Hey GlaDOS, tell me what you learned about the Spanish inquisition? https://en.wikipedia.org/wiki/Spanish_Inquisition
/\ From this I will try to parse the plain text and then run it through https://machinereading.azurewebsites.net/ (If allowed, gotta look into the legals of it)

[To be done] (Verbal) "Hey x, say y" (Voice chat version of "hey x say y")

[To be done] Again if its ok to do so I may look into using some things from https://www.microsoft.com/en-us/ai/ai-lab

# For the love of God, don't missuse this in a stupid way. Please.


