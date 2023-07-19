# Industrial IoT Gateway using Ignition Edge with HiveMQ and balena

This is a reference architecture to run on your IIoT Edge Gateway with HiveMQ MQTT broker and Ignition Edge on a balena device.


![](/assets/balena-ignition-hivemq.png)


The example application is reading from Modbus and OPC UA sensors using a variation of the MING stack (MQTT, InfluxDB, Ignition Edge and Grafana) to use the advantages of the Edge Computing to digitalize a factory. In this case, we are using Ignition Edge, HiveMQ and balena to add a UNS (Unified Name Space) for data modeling and MQTT Sparkplug B to format the data being sent over MQTT to Ignition in the cloud through HiveMQ cloud instance.


## Disclaimer

This project is for educational purposes only. Do not deploy it into your premises without understanding what you are doing. USE THE SOFTWARE AT YOUR OWN RISK. THE AUTHORS AND ALL AFFILIATES ASSUME NO RESPONSIBILITY FOR YOUR SECURITY.

We strongly recommend you to have some coding and networking knowledge. Do not hesitate to read the source code and understand the mechanism of this project or contact the authors.


## Deploy the code

Running this project is as simple as deploying it to a balenaCloud application. You can do it in just one click by using the button below:

[![](https://www.balena.io/deploy.png)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/mpous/hivemq4-ignition-balena)

Follow instructions, click Add a Device and flash an SD card with that OS image dowloaded from balenaCloud. Enjoy the magic 🌟Over-The-Air🌟!

## Configure Ignition Edge

Access to the Ignition UI using your local ip address with the `9088` port and install Ignition Edge. Create a username and password for Ignition and once the Ignition Edge is successfully installed, access to the Ignition Edge.

To receive the data from the edge IIoT gateway with HiveMQ and balena you will need to install the MQTT module packages on Ignition Edge made by Cirrus Link. For this project we will only need to install the `MQTT engine` and the `MQTT Transmission` modules. Download the [MQTT Cirrus Link modules](https://inductiveautomation.com/downloads/third-party-modules/8.1.27) for Ignition here.

When the MQTT Modules are successfully installed, you can go to the left menu on MQTT and create the servers (`Engine` and `Transmission`). Remember that the URL starts with tcp:// and add the port 1883 or your MQTT port from the edge machine MQTT broker.


## Configure the HiveMQ MQTT broker

These variables you can set them in the balenaCloud `Device Variables` tab for the device (or globally for the whole application). None of them are mandatory and the MQTT broker in the edge might work without any variable defined.

Variable Name | Value | Description | Default
------------ | ------------- | ------------- | -------------
**`HIVEMQ_BRIDGE_EXTENSION`** | `boolean` | Enable bridge extension and delete the `DISABLED` file on the bridge-extension folder | `false`
**`HIVEMQ_HOST_URL`** | `STRING` | URL of the Host connected via the Bridge Extension. | ```HIVEMQ_HOST_URL```
**`HIVEMQ_HOST_PORT`** | `STRING` | Port of the host connected via the Bridge Extension. | ```HIVEMQ_HOST_PORT```
**`HIVEMQ_HOST_USERNAME`** | `STRING` | Username of the MQTT simple authentication to connect the Bridge Extension. | ```HIVEMQ_HOST_USERNAME```
**`HIVEMQ_HOST_PASSWORD`** | `STRING` | Password of the MQTT simple authentication to connect the Bridge Extension. | ```HIVEMQ_HOST_PASSWORD```
**`HIVEMQ_TLS_ENABLED`** | `boolean` | Adds the TLS tags to use the MQTT over TLS through the Bridge Extension. | ```false```
**`HIVEMQ_TOPICS_CONFIGURATION`** | `STRING (XML)` | Topic tag XML definition on the bridge-extension.xml file. | ```<topics><topic> What it goes here </topic></topics>```
**`HIVEMQ_LICENSE`** | `STRING` | Your license file cntent in one unique line separated by \| Automatically the system will generate a `license.lic` file with the base64 content from this variable. | 
**`HIVEMQ_REST_API_ENABLED`** | `boolean` | Enables to change the config.xml file with the `rest-api` tag. | `false`
**`HIVEMQ_REST_API_CONFIGURATION`** | `STRING (XML)` | REST API tag XML definition on the config.xml file. | ```<rest-api><enabled>true</enabled><listeners><http><port>8888</port><bind-address>0.0.0.0</bind-address></http></listeners></rest-api>```
**`HIVEMQ_INFUXDB_ADDRESS`** | `STRING` | URL of the InfluxDB local database. | ```HIVEMQ_INFLUXDB_ADDRESS```
**`HIVEMQ_INFUXDB_PORT`** | `STRING` | Port of the InfluxDB local database. | ```HIVEMQ_INFLUXDB_PORT```
**`HIVEMQ_INFUXDB_DATABASE`** | `STRING` | Name of the database of the InfluxDB local database. | ```HIVEMQ_INFLUXDB_DATABASE```


## Log in

The services are exposed in different ports. On the default configuration they use the default port and credentials to access them. Check the documentation for each of them to know how to change them using variables.

|Service|Port|Username|Password|
|:--|---|---|---|
|HiveMQ|8080 (http)|admin|hivemq|
|Ignition|9088 (http)|balena|balena|
|Grafana|3000 (http)|admin|admin|
|InfluxDB|8086 (http) |balena|balenabalena|


## Attribution

- This is in part working thanks of the work of [Kudzai Manditereza](https://github.com/kmanditereza) from HiveMQ and Marc Pous from balena.io.

## Troubleshooting

If you detect any issue using this block, feel free to contact us at the [forums.balena.io](https://forums.balena.io).

