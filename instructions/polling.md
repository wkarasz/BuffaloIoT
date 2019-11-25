# Polling for SensorTag Data

The CC3200 SensorTag has a built-in webserver which displays various bits of useful information.  Props to wtremmel and the repo, [https://github.com/wtremmel/wifi-sensortag](https://github.com/wtremmel/wifi-sensortag) for documenting the various pages available.

For this workshop, we're specifically polling for data from /param_sensortag_poll.html.  The page source will look something like below:
```html
<html>
<body>
<p id="tmp">07DC 0BD8 15.72 23.69</p>
<p id="hum">A290 630C 63.50 23.84</p>
<p id="bar">59E640 7EF500 24.28 1020.21</p>
<p id="gyr">FFA8 005B FFB1 -0.67 0.69 -0.60</p>
<p id="acc">FC5F FF5B EF65 -0.23 -0.04 -1.04</p>
<p id="opt">051D 13.09</p>
<p id="mag">FDF2 0041 F9BA -526 65 -1606</p>
<p id="key">0</p>
<p id="syn">176</p>
</body>
</html>
```

The following Flogo Enterprise,[IoTWorkshopBuffalo.json](../workshopfiles/IoTWorkshopBuffalo.json) application polls param_sensortag_poll.html once a second and shoots off the data to TIBCO Cloud Messaging service.

- 
