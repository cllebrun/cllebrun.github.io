![](./images/iotp_icon_64.png)

# Introduction

This tutorial demonstrates how to connect a simulated device to the Watson IoT platform, visualize its live data, store its data into a database and leverage [Node-RED](http://www.nodered.org){:target="_blank"} tool for wiring together hardware devices, APIs and online services.



# Objectives
* You will simulate a temperature sensor.
* You will collect sensor data from a Watson IoT service.
* You will discover how to leverage Node-RED to connect IoT.
* You will store the collected data into a NoSQL database.
* You will use Watson to translate messages.


# Pre-Requisites
* An [IBM Cloud Platform](http://console.bluemix.net/){:target="_blank"} account


# Start the simulated device

We will use a simulator of a temperature sensor. This sensor also simulates Humidity and Object Temperature.<br />
This way, we don't require an actual hardware device to test our application.

1. In a new browser window or on a smartphone, browse to [IoT Sensor](http://quickstart.internetofthings.ibmcloud.com/iotsensor){:target="_blank"}.
<br />Alternatively, enter this short URL: http://ibm.biz/iotsensor

   <img alt= "IoT sensor simulator" src="./images/iotsensor.png" width="40%"/>

1. Note the Device Id (displayed in the top right corner).


# View the live sensor data

1. In a new browser window, browse to [Watson IOT Platform quickstart](https://quickstart.internetofthings.ibmcloud.com){:target="_blank"}.
<br />Alternatively, enter this short URL: http://ibm.biz/iotquickstart

    ![IoT Quickstart](./images/iot-quickstart.png)

1. Enter the device id. 

1. Vizualise the live sensor data and play with the dynamic graph. 


# Connect your device to the Watson IoT Platform

You've seen your data, what next? Now you will see how to use theses sensors data in an application created with the IBM Cloud Platform.

1. Login to the [IBM Cloud Platform](http://console.bluemix.net/){:target="_blank"}.

1. Browse the catalog under the "Boilerplates" category

    ![catalog](./images/catalog.png)

1. Double click on the **Internet of Things Platform Starter** Boilerplate to create your own <br /> instance of this IoT starter application.

    ![iotstarter](./images/boilerplate-iotstarter.png)

1. Provide the application name, leave the same namefor the host, and click **Create**.
<br /> *Note: Wait for a few minutes for your app to start running.*

1. When your app is running (green status), select the app URL or type it into the browser to open the **Node-RED flow editor**

    ```
    https://<appname>.mybluemix.net
    ```
1. You have the possibility to secure your Node-RED environment. If you decide not to do it, your Node-RED app (code editor) will be public and accessible by anyone who have the URL. It's recommanded to set a username and password.

    ![Secure Node-RED](./images/secure.png)

    Note that the settings will be persisted in the CloudantDB bound to this application. You can override them at any time by setting the following environment variables via the Bluemix console:
    ```
    NODE_RED_USERNAME - the username
    NODE_RED_PASSWORD - the password
    NODE_RED_GUEST_ACCESS - if set to `true`, allows anyone read-only access to the editor
    ```
1. Click on the red button "Go to your Node-RED flow editor" to access the flow editor.

1. You see ready-made flows. The first one simulate a device publishing an event on your Watson IoT organization (the service has been created when you deployed the app).
The second one that can process temperature readings from the Watson IoT platform events.

    ![](./images/nodered-defaultflow.png)

# Use Node-RED to read the sensor data

1. In the second flow ("Temperature Monitor"), double-click the **IBM IoT App In** node to open the configuration dialog.

    ![IoT App IN node](./images/iot-appnode.png)

1. In the Authentication type field, select **Quickstart** from the pull-down list. Enter the Device ID field (you get it from the web simulator) and click OK.
<br />*Make sure that the device id is entered in lowercase, and that there are no leading or trailing space characters.*

1. Look for the **Deploy** button in the upper right hand corner of your Node-RED workspace. The deploy button is now red; click it to deploy your flow.

    ![Node-RED Deploy](./images/nodered-deploy.png)
 
1. Open the debug pane on the right. You will see that the flow is generating Temperature Status messages.

1. Increase the temperature value on the simulator to see the messages change in the debug pane. 
<br /> *Note that a different message appears if the temperature exceeds 40 degrees.*

# Store the device data into a No SQL database

1. In Node-RED flow editor, add a **Cloudant out** node 

    ![Cloudant out node](./images/nodered-cloudant.png)

1. In the Service type field, select the name of Cloudant service bound to Node.js runtime from the pull-down list.
<br />Enter a dabatase name in lowercase. Keep the default operation insert and finally give a name to the node.

    ![Cloudant config](./images/nodered-cloudantconfig.png)

1. Deploy the flow. Return to the IBM Cloud Platform console, on the app overview, click on "Connections" and on to the Cloudant service. Click on the green button to "Launch" the Cloudant web UI. Navigate into the DB records.

    ![Cloudant console](./images/cloudant-console.png)

In your Node-RED flow editor, you can then delete the link between your IoT node and your Cloudant node if you want to stop storing data.

# Connect with the Watson IoT Platform.

The first flow simulate a device publishing an event. To visualize the data in you Watson IoT platform organization you need to register the simulated device in your organization.

1. Return to the IBM Cloud Platform console, from the "Connections" tab in your application dashboard, click on the IoT service -> launch it.

1. From the Internet of Things service dashboard, access your IoT organisation and add your device to it: Select the Devices tab on the left.

1. Select the "Device Types" tab.

    ![device types](./images/device-type.png)

1. Add Device Type (up and right).

1. Give it a name: "thermostat". Click "Next"

1. Leave the other options by default and click "Done".

1. Now you are going to register a device. Click "Register Devices"

    <img src="./images/register-device.png" width="40%"/> 

1. Enter a device ID: "LivingRoomThermo1". Click Next, Next

1. At the security step, chose an identification token (8 characters minimum)

1. Click "Done"

1. Go to Node-RED, open and modify the inject node to publish events continuously (repeat -> onterval -> every 3 seconds): 

    <img src="./images/repeat-inject.png" width="40%"/> 

1. You can see events in the Watson IoT dashboard

   ![Watson IoT dashboard](./images/events-iot.png)


# Translate messages with Watson.

The warning messages generated in Node-RED uses English by default. You may want to translate those messages into your oww language.

1. In the IBM Cloud Platform console, create a new service **Language Translator** (from the catalog) 

    ![Watson Language Translator catalog](./images/translator-catalog.png)

1.  Connect it to your app to your app (from the Connection tab in your app dashboard). Restage your app.

    ![Watson Language Translator connect](./images/translator.png)

1. Wait for your app to start again. In Node-RED flow editor, add a new **Language Translator** node to the flow.

1. Modify the flow accordingly to translate those messages.

    ![Watson Language Translator](./images/nodered-translationflow.png)

1. Deploy the updated flow. 

1. Observe the translated output based on the selected language.


# Resources

For additional resources pay close attention to the following:

- [Real Time Data Analysis Using IoT Platform Analytics](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics){:target="_blank"}

