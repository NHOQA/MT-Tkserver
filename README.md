# Meshtastic-Takserver
Meshtastic/Takserver Integration through Node-Red

Goal is bi-directional data between a meshtastic mesh and Takserver. Current plan has a meshtastic gateway node with a network connection to Takserver passing MQTT messages to Node-Red where it is converted to CoT for Takserver and vice versa for outgoing messages. Want PLI/GPS/text capability for EUD's and ability to see remote sensors tirggering in Webtak. Video streaming while in wifi range seems like it will be pretty trivial, but would still like to confirm the correct buttons to push to make that happen.
