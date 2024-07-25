# Meshtastic-Takserver
Meshtastic/Takserver Integration through Node-Red

Goal is bi-directional data between a meshtastic mesh and Takserver. Current plan has a meshtastic gateway node with a network connection to Takserver passing MQTT messages to Node-Red where it is converted to CoT for Takserver and vice versa for outgoing messages. Want PLI/GPS/text capability for EUD's and ability to see remote sensors tirggering in Webtak. Video streaming while in wifi range seems like it will be pretty trivial, but would still like to confirm the correct buttons to push to make that happen.

*****7/25/24 notes
On a note from james that there was a mention of civtak preferring protobuf CoT to xml and taking a look at https://github.com/erichexter/Mestastic-Tak-Bridge/tree/main
(which doen't run, but I did access his node red flow) trying a different path. subscribed to what I believe is the protobuf topic instead of JSON coming from gateway node. running that through the meshtastic decode node looks like im getting some kind of string out. Current config below. Have loaded some debug output from several locations into the main directory here. Tak node is from here https://node-red-contrib-tak.readthedocs.io/en/latest/
![debug1](https://github.com/user-attachments/assets/4159df95-2232-4b18-afcf-34932f13227b)
