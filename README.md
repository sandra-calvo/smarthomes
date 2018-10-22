# IBM Cloud :cloud: and Smart Homes:house_with_garden:
## Mimmitkoodaa workshop guide 

In this guide:
  - [Introduction](#introduction)
  - [IoT devices](#iot-devices): Thingsee IoT sensors
  - [PHASE 1](#phase-1): Create a web application
  - [PHASE 2](#phase-2): Visualize your data
  - [PHASE 3](#phase-3): Add AI powered chatbot to your application using Watson Assistant 
  - [PHASE 4](#phase-4): Connect with external APIs using Weather Insights

  
  
  #### Prerequisites
- IBM Cloud account
  - Create a free account www.bluemix.net

  ## Introduction 

This lab was created for Smart Homes Mimmitkoodaa workshop fall 2018. The idea is to show how to create a smart home application that uses artificial intelligence and connects with external APIs. 
Video tutorial, including simulated data, will be available December 2018.

**IBM Cloud** is a suite of cloud computing services from IBM that offers both platform as a service (PaaS) and infrastructure as a service (IaaS). A full-stack cloud platform with over 170 products and services covering data, serverless, containers, AI, IoT and blockchain. https://www.ibm.com/cloud/

<img src="/images/IBMCloud.png" width="90%" height="90%">

## IoT devices

In this lab we are going to use **Thingsee sensors** created by Haltian (https://thingsee.com/). Thingsee IoT devices are wireless and easy to plug & play. The sensors can be pre-configured to send data to any cloud. For the purpose of this lab sensors are pre-configured to send data to Watson IoT Platform, part of IBM Cloud. 

<img src="/images/Sensors1.png" width="80%" height="80%">

There are three types of sensors distance, environment and presence. The gateway collects the data to send it to the cloud. 

Thingsee **DISTANCE** is a wireless IoT sensor for measuring container fill rates, asset presence on location and more.
Thingsee distance measures the sensor's distance to a surface in real time. You can use the sensor for various facility management applications, asset tracking, parking facility solutions and more.

Thingsee **ENVIRONMENT** sensor measures temperature, humidity, air pressure, light level, movement and impacts. You can also detect magnets and even get device location using network RSSI location.

Thingsee **PRESENCE** is a wireless IoT sensor for measuring people presence through the facility. Thingsee Presence IoT sensor measures the presence of people in real time. You can use the sensor for facility management and security applications, for example.

<img src="/images/Sensors.png" width="90%" height="90%">

# PHASE 1
## Create an application

### Step 1. Create a Node-RED application

**Node-RED** is a visual tool for wiring the internet of things - connecting hardware devices, APIs and online services in a new and interesting way. Node-RED provides a browser-based flow editor that makes it easy to wire together flows using the wide range nodes in the palette. Flows can be then deployed to the runtime in a single click.

In a browser navigate to https://bluemix.net
Select '_LOG IN_' then enter your login information and press 'SIGN IN'.  You should see your dashboard. 
Select the '_CATALOG_' view.
![](/images/App1.png?raw=true)
Locate the Node-RED starter service, under Starter Kit, and click on it. 

<img src="/images/App2.png" width="30%" height="30%">

Enter a name for your application, for example: *mysmarthome* (host will automatically be completed). The hostname must be unique on IBM Cloud, so please if you use the example name add your initials or a number. Be creative and try to make a unique name then click '_CREATE_'. 

<img src="/images/App3.png" width="100%" height="100%">
 
Your application is now staging and will be up and running in a short while. Click 'OVERVIEW' to see information about your application. 
The application will be ready in a couple of minutes. If you want to check the progress click on the  _LOGS_  icon on the left side menu. Go back to _Overview_ tab to see your app dashboard.

<img src="/images/App3b.png" width="20%" height="20%">

*Note: If you are using Lite accounts your application will be in an awake mode. That means that if after 10 days your application has not been used IBM will stop it.*

When fully staged, click on the _Visit app URL_, next to the green or half green circle, this launches the Node-RED main page.

<img src="/images/App4.png" width="90%" height="90%">
  
Configure your Node-RED editor. In this section, you will set up a username and password to protect your flow. We are working in the public cloud that means that anyone can access your application through a web browser, set a username and password to protect your code.

<img src="/images/App5.png" width="40%" height="40%">

Write an username and a password of your choice and click 'Next'. Remember that it does not have to be related to your IBM Cloud ID. Let the browser remember the password if you are using your own laptop, it will come in handy later. 

<img src="/images/App6.png" width="40%" height="40%">
 
#### Your Node-RED flow is all set! Enter your credentials to access the editor.

<img src="/images/App8.png" width="70%" height="70%">
 
Now click Go to your Node-RED flow editor to open the flow editor.

When using Node-RED we build our apps using this graphical editor interface to wire together the blocks we need. We can simply drag and drop the blocks from the left menu into the workspace in the center of the screen and connect them to create a new flow. 

### Step 2: Add new nodes to the Node-RED palette
We are going to add new nodes to the Node-RED palette directly from the Node-RED window. For this lab we need the following nodes:

      - node-red-dashboard
      - node-red-node-openweathermap

In the Node-RED window click on the three lines on the top right corner and in the menu, click on the "Manage palette". This will open the node menu where you can add new nodes to your application. 

<img src="/images/App23.png" width="20%" height="20%">

You will see the nodes that are installed by default and if you go to the 'install' tab you can search for any node package and add it directly to your app.

<img src="/images/App24.png" width="30%" height="30%">
             
Search for the dashboard nodes by writing 'dashboard'. This will return multiple node packages, you need to install the package 'node-red-dashboard'. Find it in the search results and click on install. 

<img src="/images/App25.png" width="30%" height="30%">
 
This will prompt a window to confirm the installation. Click on install and wait few minutes. Click "Done" to close the left side menu. 

<img src="/images/App26.png" width="50%" height="50%">

After few seconds you will see the new nodes in your Node-RED palette.

**Remember to repeat this process to install node-red-node-openweathermap package.**

# PHASE 2
## Visualize your data

### Step 3: Import the Node-RED application flow
In this section we will build a simple flow to connect with our sensor data and create a web visualization. 

Copy the content of the **visualization_UI.json** file. Open the file URL. [Visualization UI code](https://raw.githubusercontent.com/sandra-calvo/smarthomes/master/visualization_UI.json) 

Use the keyboard shortcuts to select all content and copy it.
    
  OSx
    <kbd>Cmd</kbd>+<kbd>A</kbd> -->
    <kbd>Cmd</kbd>+<kbd>C</kbd>

  Windows
    <kbd>Ctrl</kbd>+<kbd>A</kbd> -->
    <kbd>Ctrl</kbd>+<kbd>C</kbd>

Import the flow by simply clicking on the 3 white lines on the top right corner of the Node-RED window.  Import - Clipboard.

<img src="/images/App27.png" width="50%" height="50%">

Paste the text you copied from the file. 

<img src="/images/App28.png" width="50%" height="50%">

This flow reads sensor data from the Watson IoT Platform and creates a visualization in your application's user interface. 
It should look like this:

<img src="/images/flow23.png" width="80%" height="80%">

<img src="/images/flow24.png" width="60%" height="60%">

You will need to do some editing. Double click on the blue IBM IoT node and click on the pen icon. 

<img src="/images/iot1.png" width="40%" height="40%">

The sensors are pre-configured to send data to Watson IoT platform. At this moment all sensors send data to a service created by me (Sandra). Here the credentials to read the data coming from the sensors:

    API KEY: a-jwql3u-qmhoi8sdzy
    API TOKEN: OSxT5QVJYxItsV*K4y

Enter the credentials above to start reading the data from the IoT platform. Then click on _Update_.

<img src="/images/iot2.png" width="40%" height="40%">

If you want you can add a database node to store the sensor data in a database. This will give you the possibility to analyse data later and even predict when you need to turn off the heat during spring. 

To do this drag and drop the node **Cloudant out** located in the node pallette under storage. 
<img src="/images/node1.png" width="10%" height="10%">

Connect the node like this:

<img src="/images/flow25.png" width="60%" height="60%">

Double click on the node and select your Cloudant service from the drop-down menu. Then click _Done_.

<img src="/images/db0.png" width="40%" height="40%">

Deploy your application changes from the **Deploy** button on the top right side of the screen. 

Note that it is also possible to change the looks of your user interface in the dashboard tab. 

### Step 4. Check your web app UI! 
The dashboard nodes added an UI to our Node-RED application. 

<img src="/images/webApp1.png" width="80%" height="80%">

To access the UI go to:
http://yourAppName.eu-gb.mybluemix.net/ui - UK

Remember that if you are in US, Germany Sydney the address will look slightly different:
http://yourAppName.mybluemix.net/ui - US South

http://yourAppName.eu-de.mybluemix.net/ui - Germany

http://yourAppName.au-syd.mybluemix.net/ui - Sydney

**Fantastic! Your web app is ready.** 
Now you can observe your Smart Home dashboard. :+1:


# PHASE 3
## Add AI-powered chatbot to your application using Watson Assistant

In this phase we are going to add a chatbot to our application, powered by Watson Assistant. Through the chatbot you will be able to get information about the sensor data in your "Smart Home" environment. 

### Step 5. Create Watson Assistant service on IBM Cloud
With IBM Watson™ Assistant service you can build a solution that understands natural-language input and uses machine learning to respond to customers in a way that simulates a conversation between humans.

Go to your IBM Cloud account and open the catalog. Look for Watson Assistant service and click on it.

<img src="/images/WA1.png" width="50%" height="50%">

Choose the region and space where you want the service to be created. Your organization will be filled by default.
You don't need to change the name if you don't want to, just click on 'Create'. 
![](/images/WA2.png?raw=true)

Once the service is created click on 'Launch tool' to access it. 

<img src="/images/WA3.png" width="60%" height="60%">
 
Click on login with IBM ID and you will automatically access the service. It uses your IBM Cloud ID and password.

<img src="/images/WA4.png" width="30%" height="30%">

In the home tab you have videos and tutorials on how to get started building dialoges. Feel free to explore them. 
Let's move to the Workspaces tab.

<img src="/images/WA5.png" width="50%" height="50%">
 
### Step 6. Import a workspace
The natural-language processing happens inside a workspace, which is a container for all of the artifacts that define the conversation flow for an application.

You can create a workspace and start from scratch or import an existing conversation. 
Let's start by importing a conversation. Download the **assistant_conversation.json** file located [Assistant Conversation](https://raw.githubusercontent.com/sandra-calvo/smarthomes/master/assistant_conversation.json). 

Click on the import icon shown in the image below. 

<img src="/images/WA6.png" width="30%" height="30%">

When you import a workspace, you can choose to import only the intents and entities, which can be useful if you want to build a new dialog using the same training data. In this case we will import everything.

<img src="/images/WA7.png" width="50%" height="50%">

### Step 7. Test your dialog
As you make changes to your dialog, you can test it at any time to see how it responds to input.
From the Dialog tab, click the conversation bubble icon. In the chat panel, type some text and then press Enter.
Check the response to see if the dialog correctly interpreted your input and chose the right response. 

The chat window indicates what intents and entities were recognized in the input. In the dialog editor pane, the currently active node is highlighted
Feel free to create new intents for your bot.
![](/images/WA8.png?raw=true)

### Step 8. Get Watson Assistant credentials 
Since we will need your Watson Assistant credentials and your workspace ID in the next step, this is a good moment to save them. Go to the deploy tab in the Assistant window. There you will find your workspace ID, username and password. 

Copy the credentials and save them for later.
![](/images/WA9.png?raw=true)

### Step 9. Build a Node-RED flow to connect with Watson Assistant
**Back to Node-RED window**

Copy the content of the **assistant_UI.json** file. Open the file URL. [Assistant UI code](https://raw.githubusercontent.com/sandra-calvo/smarthomes/master/assistant_UI.json) 

Use the keyboard shortcuts to select all content and copy it. 
    
  OSx
    <kbd>Cmd</kbd>+<kbd>A</kbd> -->
    <kbd>Cmd</kbd>+<kbd>C</kbd>

  Windows
    <kbd>Ctrl</kbd>+<kbd>A</kbd> -->
    <kbd>Ctrl</kbd>+<kbd>C</kbd>

Import the flow by simply clicking on the 3 white lines on the top right corner of the Node-RED window. Import -> Clipboard. Paste the content.
This is the flow we are importing:

<img src="/images/flow21.png" width="100%" height="100%">

Time to do some editing! :smiley:

Double click on the conversation node to edit the node with your own credentials saved in the previous step. 
Add your username, password and workspace id and click Done.

<img src="/images/WA12.png" width="40%" height="40%">

Finally we need to confirm that the blue IoT node is reading the data correctly. Double click on the blue IBM IoT node and click on the pen icon. If you see the credentials all should work, if the credentials are missing add the API key and API token provided previously in this lab. 

Once you have edited all the nodes click on the _Deploy_ button to save the changes in your application.

### Step 10. Check the final result! 
Go back to the UI and talk with your bot! 
You can ask the bot about IoT and even ask what is the temperature in the room. The bot is connected to the sensors in your "Smart Home" environment. 

Remember, to go back to your web app (in UK region)
http://yourAppName.eu-gb.mybluemix.net/ui - UK

<img src="/images/webApp2.png" width="60%" height="60%">


# PHASE 4
## Connect with external APIs like Weather

You can connect your application with any available API. In this case we are going to connect Watson Assistant to the weather data. This way our bot will be able to tell us the weather anywhere in the world. 

Normally, I would use **Weather Company Data** service available on IBM Cloud. This service lets you integrate weather data from The Weather Company into your application. It has a free tier, but it is not available for Lite accounts. 
If you have an upgraded account you can use the Weather Company service. Feel free to ask me for the code. :blush: 

For this lab we are using Open Weather Map data https://openweathermap.org/. 
Note: An API key is required to use these nodes. You can register and obtain your own API key, or use the one available for this workshop. 

Copy the content of the **weather_UI.json** file. Open the file URL. [Weather UI code](https://raw.githubusercontent.com/sandra-calvo/smarthomes/master/weather_UI.json) 

Use the keyboard shortcuts to select all content and copy it. 
    
  OSx
    <kbd>Cmd</kbd>+<kbd>A</kbd> -->
    <kbd>Cmd</kbd>+<kbd>C</kbd>

  Windows
    <kbd>Ctrl</kbd>+<kbd>A</kbd> -->
    <kbd>Ctrl</kbd>+<kbd>C</kbd>

Import the flow to Node-RED by simply clicking on the 3 white lines on the top right corner of the Node-RED window. 
Import -> Clipboard. Paste the content.
This is the flow we are importing:

<img src="/images/flow27.png" width="70%" height="70%">

This flow gets weather information from Open Weather Map API. The location comes through the chatbot from the user. Then the city name goes to Google Maps API to get the coordinates and longitude & latitude are sent to the weather service. Finally it is visualized in the UI. 

**Remember** Connect the node "Weather response" with the node "Bot response".

We need to edit the yellow Open Weather Map node and add the API key. 

    API KEY: 3a1ac87a062142df79f4177302bd7ab9

Click on _Deploy_ and go to the UI to check the changes! Now your UI should look like this:

<img src="/images/webApp3.png" width="70%" height="70%">

**Congrats!** You finished the lab. :clap:
Here, take a :lollipop:. You deserve it!! 
