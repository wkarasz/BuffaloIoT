# SensorTag Connectivity
## Overview

The TI SensorTag CC3200 is jam packed with sensors<br>
![CC3200stk-wifimk](img/cc3200.png "SensorTag Sensors")
<br>
For this workshop, all the data is sent to TIBCO Cloud Messaging over a secure websocket connection.  Each sensor is pumping out data once per second, tagged with its unique id (key).<br>
<br>
> For those looking for more details on how data is pulled off the SensorTag, check out this [page](polling.md).


```json
{
    "key":"value",
    "temperature":"value",
    "humidity":"value",
    "pressure":"value",
    "gyro_x":"value",
    "gyro_y":"value",
    "gyro_z":"value",
    "accel_x":"value",
    "accel_y":"value",
    "accel_z":"value",
    "light":"value",
    "mag_x":"value",
    "mag_y":"value",
    "mag_z":"value",
    "uptime":"value"
}
```
<br>
In this hands-on lab, you will import an existing TIBCO Cloud application that connects to the TIBCO Cloud Messaging service and filter on your SensorTag data.

## Get Started

Sign into TIBCO Cloud and open Extensions.  There are many ways to navigate to Extensions, but let's start with this:

1) Start at Welcome to your TIBCO Cloud
2) Select Integration
3) Select Flogo

## Load Pre-requisite External Extension Dependency

Before you import the application, we need to first import an external extension.  Once an extension is imported, it is available for all future applications.

1. Select **Extensions**
2. Select **Upload an extension** and paste into **Git repository URL**:<br>
   `github.com/project-flogo/contrib/activity/counter`<br>
  And select **Import** and then **Done**

<img src="img/tci_add_extension.png" width=600 alt="Add extension"/>

<img src="img/tci_import_extension.png" width=400 alt="Import extension"/>  

## Import Application

We are going to use a prebuilt application for this hands-on lab and modify it to filter on your SensorTag data.

1) Select **Apps**
1) Select **Create**
2) Give your new app a name, **UBIoT**, and select Create.
3) Select **Create a TIBCO Flogo App**
4) Select **+ Import app**
5) Navigate to where you downloaded the app artifact and choose or drag **[CC3200v2.json](https://raw.githubusercontent.com/wkarasz/BuffaloIoT/master/workshopfiles/CC3200v2.json)** (tip: ctrl+click and save file) into upload files and select Upload
6) Press continue when you get the warning dialog for passwords
7) You are now ready to reconfigure this App with your SensorTag filter key
 
In screenshots, the steps above:

![Create new app](img/create_flogo_app.png "Create Flogo App")

![Select Flogo App](img/create_flogo_app2.png "Select Flogo App")

![Select to Import an existing app](img/create_flogo_app3.png "Import App")

<img src="img/create_flogo_app4.png" alt="Select and upload CC3200v1.json" width=400)/>

### Configure the Application
--------

#### Edit the TCM Connector

The import automatically created the TIBCO Cloud Messaging (TCM) connector, however, the authentication key must be entered.

1) Select **Connections**
2) Select **TIBCO Cloud Messaging - SensorTag** and then **Edit**
3) Update the authentication key with the following value:
  <br>`84a1916b84e22b4d7a6ea75a3ed24936`
4) Select **Save**

![Edit TCM Connection](img/edit_tcm_connection.png "Edit TCM Connection")

<img src="img/configure_tcm_connector.png" alt="TCM Configuration" width=400/>

#### Filter To Your SensorTag Data

You'll open up the application and modify the logic to filter on your SensorTag.  A branch condition is used to process only tag data that matches the specified SensorTag key ID.

1) Select **Apps**
2) Select app **UBIoT**
3) Select flow **SensorRx**
4) Select branch transition and gear icon
5) Update **condition** to value of your SensorTag key ID

![Update transition](img/update_transition.png "Update transition expression")

![Update transition condition](img/update_transition2.png "Change expression to your SensorTag ID")

### Test the Application
--------

TIBCO Cloud enables you to unit test each application flow you develop.  The built-in tester enables you to create, configure, and reuse Launch Configurations to accelerate debugging of your application.

![Start Testing!](img/tester.png "Select 'Start testing'")

![Create a Launch Configuration](img/tester2.png "Create a Launch Configuration")

Drop in the following payload for the $flowInputs/stringValue:

```json
'{"key":"0", "accel_x": "0.02","accel_y": "0.03","accel_z": "0.95","gyro_x": "-0.58","gyro_y": "0.74","gyro_z": "-0.51","humidity": "67.85","light": "0.00","mag_x": "-613","mag_y": "1160","mag_z": "-613","pressure": "1000.40","temperature": "23.69","uptime": "13255"}'
```

Be sure to update the **key** with your SensorTag ID.

![Update stringValue](img/tester3.png "Paste in payload, don't forget to update your keyname")

Click **Next** and **Run** to try out your application.  If all is good, your output should look like the following:

![Successful output](img/tester4.png "Tester Flow output")

## Ready, Set, PUSH

If your application successfully executed in the prior step, then you are ready to Push the application into runtime mode.

Click on the **Push app**, give it a moment, and the application screen will switch to launching your application
![Push app](img/app_start.png "Push app")

![Push app](img/app_start2.png "App starting")

![App Started](img/app_start3.png "App Running")

### Review the Realtime Logs
--------

With the SensorTag continuously producing data, you can now go back and look at the realtime logs associated with your application.

Click back into the application and click on Log.

![Review Logs](img/app_log.png "Review Logs")

### Scale the Application
--------

Ready to cool things off or want to ramp up for more activity, scale it with a click.

![Scale](img/app_scale.png)

<img src="img/app_scale2.png" width=100/><img src="img/app_scale3.png" width=100/><img src="img/app_scale4.png" width=100/>

## Summary

In this lab you successfully demonstrated connecting to an IoT sensor and retrieving its data published to TIBCO Cloud Messaging service.  You did this by filtering only data that matched your SensorTag ID by using the conditional branching functionality.

## Let's Move On
In the next lab, you'll focus on creating a decision table to create rules on how to process the SensorTag data. 

[--- next lab ---](rulestable.md)
