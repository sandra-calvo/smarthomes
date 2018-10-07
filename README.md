# IBM Cloud :cloud: and Smart Homes:house_with_garden:
## Mimmitkoodaa workshop guide

In this guide:
  - [Introduction](#introduction)
  - [IoT devices](#iot-devices): Thingsee IoT sensors
  - [PHASE 1](#phase-1): Create a web application
  - [PHASE 2](#phase-2): Visualize your data
  - [PHASE 3](#phase-3): Add AI to your application - Watson Assistant -   
  - [PHASE 4](#phase-4): Connect with external APIs - Weather - 
  - [PHASE 5](#phase-5): Include rules and actions based on sensor data
  
  
  #### Prerequisites
- IBM Cloud account
  - Create a free account www.bluemix.net
  
  ## Introduction 
  
This guide shows how to create a Smart Home application using Thingsee sensors and IBM Cloud. 

**IBM Cloud** is a suite of cloud computing services from IBM that offers both platform as a service (PaaS) and infrastructure as a service (IaaS). 

<img src="/images/IBMCloud.png" width="90%" height="90%">

## IoT devices

In this lab we are going to use **Thingsee sensors** created by Haltian (https://thingsee.com/). Thingsee IoT devices are wireless and easy to plug & play. The sensors can be pre-configured to send data to any cloud.

<img src="/images/Sensors1.png" width="80%" height="80%">

There is three types of sensors distance, environment and presence. The gateway collects the data to send it to the cloud. 

Thingsee **DISTANCE** is a wireless IoT sensor for measuring container fill rates, asset presence on location and more.
Thingsee distance measures the sensor's distance to a surface in real time. You can use the sensor for various facility management applications, asset tracking, parking facility solutions and more.

Thingsee **ENVIRONMENT** sensor measures temperature, humidity, air pressure, light level, movement and impacts. You can also detect magnets and even get device location using network RSSI location.

Thingsee **PRESENCE** is a wireless IoT sensor for measuring people presence through the facility. Thingsee Presence IoT sensor measures the presence of people in real time. You can use the sensor for facility management and security applications, for example.

<img src="/images/Sensors.png" width="90%" height="90%">

# PHASE 1
## Create a web application

### Step 1. Create a Node-RED application

**Node-RED** is a visual tool for wiring the internet of things - connecting hardware devices, APIs and online services in a new and interesting way. Node-RED provides a browser-based flow editor that makes it easy to wire together flows using the wide range nodes in the palette. Flows can be then deployed to the runtime in a single-click.

In a browser navigate to https://bluemix.net
Select 'LOG IN' then enter your log in information and press 'SIGN IN'.  You should see your dashboard. 
Select the 'CATALOG' view.
![](/images/App1.png?raw=true)
Locate the Node-RED started service and click on it. 

<img src="/images/App2.png" width="30%" height="30%">

Enter a name for your application, as shown below (host will automatically be completed). The host name must be unique on IBM Cloud, so please choose a name with your company name or initials to try to make a unique name.  Press 'CREATE'. 

<img src="/images/App3.png" width="100%" height="100%">
 
Your application is now staging and will be up and running in a short while. Click 'OVERVIEW' to see information about your application. 
The application will be ready in a couple of minutes. If you want to check the progeress click on the _LOGS_ icon on the left side menu. 

<img src="/images/App3b.png" width="20%" height="20%">

*Note: If you are using Lite accounts your application will be in an awake mode. That means that if after 10 days your application has not been used IBM will stop it.*

When fully staged, click on the _Visit app link_, next to the green or half green circle, this launches the Node-RED main page.

<img src="/images/App4.png" width="90%" height="90%">
  
Configure your Node-RED editor. In this section, you will set up a username and password to protect your flow. 
<img src="/images/App5.png" width="40%" height="40%">

Write an username and a password of your choice and click 'Next'. Remember that it does not have to be related to your IBM Cloud ID. 

<img src="/images/App6.png" width="40%" height="40%">
 
#### Your Node-RED flow is all set! Enter your credentials to access the editor.

<img src="/images/App8.png" width="70%" height="70%">
 
Now click Go to your Node-RED flow editor to open the flow editor.

When using Node-RED we build our apps using this graphical editor interface to wire together the blocks we need. We can simply drag and drop the blocks from the left menu into the workspace in the center of the screen and connect them to create a new flow. 

### Step 2: Add new nodes to the Node-RED palette
We are going to add new nodes to the Node-RED palette directly from the Node-RED window. For this lab we need the following nodes:

      - node-red-dashboard

In the Node-RED window click on the three lines on the top right corner and in the menu, click on the "Manage palette". This will open the node menu where you can add new nodes to your application. 

<img src="/images/App23.png" width="20%" height="20%">

You will see the nodes that are installed by default and if you go to the 'install' tab you can search for any node package and add it directly to your app.

<img src="/images/App24.png" width="30%" height="30%">
             
Search for the dashboard nodes by writing 'dashboard'. This will return multiple node packages, you need to install the package 'node-red-dashboard'. Find it in the search results and click on install. 

<img src="/images/App25.png" width="30%" height="30%">
 
This will prompt a window to confirm the installation. Click on install and wait few minutes, the application may require a restart. Click "Done" to close the left side menu. 

<img src="/images/App26.png" width="50%" height="50%">

After few seconds you will see the new nodes in your Node-RED palette.

**Remember** to repeat this process to install the other packages.

# PHASE 2
## Visualize your data

### Step 3: Import the Node-RED application flow
In this section we will build a simple flow to connect with our sensor data and create a web visualization. 

Copy the content of the **UI_Dashboard.json** file. **-ADD PATH-**
Import the flow by simply clickcing on the 3 white lines on the top right corner of the Node-RED window.  Import - Clipboard.

<img src="/images/App27.png" width="50%" height="50%">

Paste the text you copied from the file. 

<img src="/images/App28.png" width="50%" height="50%">

This flow reads sensor data from the Watson IoT Platform and creates a visualization in your application's user interface. 

<img src="/images/App29.png" width="100%" height="100%">
 
You will need to do some editing. **EDITING ON THE NODES**

<img src="/images/App32.png" width="50%" height="50%">

Note that it is also possible to change the looks of your user interface in the dashboard tab. 

Deploy your application changes from the **Deploy** button on the top right side of the screeen. 

### Step 4. Check your webapp UI! 
The dashboard nodes added an UI to our Node-RED application. 

<img src="/images/App30.png" width="80%" height="80%">

To access the UI go to:
http://yourAppName.eu-gb.mybluemix.net/ui - UK

Remember that if you are in US, Germany Sydney the addredd will look slightly different:
http://yourAppName.mybluemix.net/ui - US South

http://yourAppName.eu-de.mybluemix.net/ui - Germany

http://yourAppName.au-syd.mybluemix.net/ui - Sydney

**Fantastic! Your web app is ready.** 
Now you can interact with your Smart Home dashboard. :+1:


# PHASE 3
## Add AI to your application 

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
 
Click on Log in with IBM ID and you will automatically access the service. It uses your IBM Cloud ID and password.

<img src="/images/WA4.png" width="30%" height="30%">

In the home tab you have videos and tutorials on how to get started building dialoges. Feel free to explore them. 
Let's move to the Workspaces tab.

<img src="/images/WA5.png" width="50%" height="50%">
 
### Step 6. Import a workspace
The natural-language processing happens inside a workspace, which is a container for all of the artifacts that define the conversation flow for an application.

You can create a workspace and start from scratch or import an existing conversation. 
Let's start by importing a conversation. Download the **bot_conversation.json** file located **PATH**. 

Click on the import icon shown in the image below. 

<img src="/images/WA6.png" width="30%" height="30%">

When you import a workspace, you can choose to import only the intents and entities, which can be useful if you want to build a new dialog using the same training data. In this case we will import everything.

<img src="/images/WA7.png" width="50%" height="50%">

### Step 7. Test your dialog
As you make changes to your dialog, you can test it at any time to see how it responds to input.
From the Dialog tab, click the conversation buble icon. In the chat panel, type some text and then press Enter.
Check the response to see if the dialog correctly interpreted your input and chose the right response. 

The chat window indicates what intents and entities were recognized in the input. In the dialog editor pane, the currently active node is highlighted
Feel free to create new intents for your bot.
![](/images/WA8.png?raw=true)

### Step 8. Get Watson Assistant credentials 
Since we will need your Watson Assistant credentials and your workspace ID in the next step, this is a good moment to save them. Go to the deploy tab in the Assistant window. There you will find your workspace ID, username and password. Copy the credentials and save them for later.
![](/images/WA9.png?raw=true)

### Step 9. Build a Node-RED flow to connect with Watson Assistant
**Back to Node-RED window**

Copy the content of **UI_Bot.json** and import the flow to Node-RED, same way you did in Step 15.
The file is located in the Box folder. 

This is the flow we are importing:

<img src="/images/WA10.png" width="100%" height="100%">

**EDIT THE NODE**

<img src="/images/WA11.png" width="100%" height="100%">

Double click on the conversation node to edit the node with your own credentials saved in the previous step. 
Add your username, passworkd and workspace id and click Done.

<img src="/images/WA12.png" width="40%" height="40%">

Click on the _Deploy_ button to save the changes in your application.

### Step 10. Check the final result! 
Go back to the UI and talk with your bot! 
You can ask the bot about IoT and even ask what is the temperature in the room. The bot is connected to the sensors in your "Smart Home" environment. 

Remember, to go back to your web app (in UK region)
http://yourAppName.eu-gb.mybluemix.net/ui - UK

![](/images/WA15.png?raw=true)


# PHASE 4
## Connect with external APIs like Weather

You can connect your application with any available API. In this case we are going to connect Watson Assistant to the Weather Company data. This way our bot will be able to tell us the weather anywhere in the world. 

**Weather Company Data** service lets you integrate weather data from The Weather Company into your application. You can retrieve weather data for an area specified by a geolocation. The data allows you to create applications that solve real business problems where weather has a significant impact on the outcome.

Go to your IBM Cloud account and open the catalog. Look for Weather Company service and click on it.

<img src="/images/Weather1.png" width="50%" height="50%">

Choose the region and space where you want the service to be created. Your organization will be filled by default.
There is a free plan that allows you to call the service 10.000 times per account. 
You don't need to change the name if you don't want to, just click on 'Create'. 
![](/images/Weather2.png?raw=true)

Once the service is created click on 'Launch tool' to access it. 

<img src="/images/Weather3.png" width="60%" height="60%">

GET CREDENTIALS


# PHASE 5
## Include rules and actions based on sensor data



**Congrats!** You finished the lab. :clap:
Here, take a :lollipop:. You deserve it!! 
