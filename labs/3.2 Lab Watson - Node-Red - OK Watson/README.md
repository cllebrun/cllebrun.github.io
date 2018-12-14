
# 3.2 Lab Watson - Node-Red - OK Watson - Introduction

This hands-on, technically-oriented lab demonstrates the key capabilities of IBM Cloud Platform, Node-RED and Watson services. Attendees will first learn how to play with Node-RED and Watson services such as Text to Speech, Speech to Text, Conversation and Tone Analyzer. Then they will learn how to integrate Watson services in a web application with an interface using Node.js. This lab will give attendees a jump-start on each of these APIs.

# Objective

In the following lab, you will learn:


+ How to use Node-RED to develop quickly
+ How to use Watson services


# Pre-Requisites

+ Get an [IBM Cloud Platform account](https://console.bluemix.net/registration/), or use an existing account.


# Steps

1. Create a Node-RED instance
2. Watson Text To Speech
3. Watson Speech To Text
4. Watson Visual Recognition
5. Watson Tone Analyser


# Step 1 - Create a Node-RED instance

1.  Make sure to work in the same space during the lab. Chose the US-South region to work in.

1.  Browse the catalog on IBM Cloud and look for the "Node-RED Starter". Create it. It comes with an instance of Cloudant DB. Give it a unique name.

<img src="./images/nodered.png"/>

1.  Wait for your application to start and browse the URL.

1. Follow the instructions to secure your Node-RED application


# Step 2 - Watson Text To Speech

1.  Browse the catalog on IBM Cloud and look for the "Watson Text To speech". Create it.

1.  Bind it to your Node-RED app. Restage

1.  In your Node-RED app, Menu -> Manage Palette -> Install the "node-red-contrib-play-audio" package.
<img src="./images/playaudio.png"/>

1.  Drag and drop the following nodes from the palette:
<img src="./images/tts.png"/>
1.  Configure the inject node to send a string data: "Hello, how are you doing today ?"
1.  Configure the Watson node (language).

1.  Deploy with red button up and right. Trigger the inject node.

# Step 3 - Watson Speech To Text

1.  Browse the catalog on IBM Cloud and look for the "Watson Speech To Text". Create it.

1.  Bind it to your Node-RED app. Restage.

1.  In your Node-RED app, Menu -> Manage Palette -> Install the "node-red-contrib-browser-utils" package.
<img src="./images/browserutil.png"/>

1.  Drag and drop the following nodes from the palette:
<img src="./images/stt.png"/>

1.  Configure the Watson node (language).
1.  Deploy with red button up and right. Trigger the microphone and speak.
# Step 4 - Watson Assistant

1.  You already worked with Watson Assistant, drag and drop the node "Watson Assistant" in Node-RED.

1. Build the following flow:
<img src="./images/assistant.png"/>

1. Configure the Assistant node with the info from your Assistant service in the Watson assistant tool:
<img src="./images/assistant-cred.png"/>

1. Configure the input node to test your flow with the function you created about Weather forecast in the last lab:
<img src="./images/weatherinput.png"/>

1. Change your flow to mix the services in the same flow:
<img src="./images/mixandmatch.png"/>

1. Test it

# Step 5 - Watson Visual recognition

1. You may already have an instance of Visual Recognition.

1.  You just need to drag and drop the visual recognition node to your node-RED

1. Import the solution on your dashboard: https://github.com/cllebrun/cllebrun.github.io/blob/master/labs/3.3%20Lab%20Watson%20-%20Visual%20Recognition/solution.json

  Menu -> Import -> clipboard

  <img src="./images/visu.png"/>

1. Configure the Visual reco with your api key and your service ENDPOINT

1. Deploy

1. Launch [yourappname]/people and give an image url of a person. Check the results.
