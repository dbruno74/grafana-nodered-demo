# grafana-nodered-demo
Grafana snap for IoT Device nodered demo

## Description
Grafana snap which come with the MQTT plugin and all the required configurations to run
the IoT Device nodered demo. The snap is supposed to be installed on a local pc.
Once installed, point your browser to http://localhost:3000 to access the grafana dashboard.

The Grafana snap includes a Data source configured to connect to hivemq public MQTT broker.
To change the broker, login to grafana with admin/admin and go to "Data Sources/MQTT".

The grafana.ini file is located in $SNAP_DATA/conf/grafana.ini. Edit with root permissions to change the configuration
(e.g. to change the grafana http port, search for "http_port" and change the port accordingly.

The snap provides a content interface slot called "writable".
The "writable" slot allows r/w on $SNAP_DATA/conf. Tipical usage is to add/modify a custom grafana.ini file.

To connect to the interface, your snap should declare a "writable" slot as described below:
```
plugs:
   writable:
     interface: content
     content: writable-data
     target: <your target dir>
```
More info on content interface here: https://snapcraft.io/docs/content-interface

## How to use it
Use the following command to connect the interface:
```
snap connect <your-snap-name>:writable grafana-nodered-demo:writable
```

# Grafana plugins
To include Grafana plugin, add the following to snapcraft.yaml

```
<plugin_id>:
    plugin: dump
    source: <link to zip file of the plugin
    source-type: zip
```
Then configure the install hook to copy the plugin in the grafana plugin directory:
```
cp -r ${SNAP}/<plugin id> ${SNAP_COMMON}/data/plugins
```

