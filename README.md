# Meshtastic-Takserver
Meshtastic/Takserver Integration through Node-Red

Goal is bi-directional data between a meshtastic mesh and Takserver. Current plan has a meshtastic gateway node with a network connection to Takserver passing MQTT messages to Node-Red where it is converted to CoT for Takserver and vice versa for outgoing messages. Want PLI/GPS/text capability for EUD's and ability to see remote sensors tirggering in Webtak. Video streaming while in wifi range seems like it will be pretty trivial, but would still like to confirm the correct buttons to push to make that happen.

7/28/24

Intermediate goal, bring in just sensor trigger alarm from meshtastic passive IR motion sensor. I've gotten a manually written CoT message to send into takserver. So I know my TCP connection is working.

The example manually written CoT message (stole this off the internet)

/* 
Example JSON containing the keys & values for popular cursor on target CoT 
fields, including time, point latitude & longitude, type, and more.
*/

/* Stale is Date.now() + miliseconds. 
 Ruberic: 1000 Miliseconds in 1 Second
 Example: 5 Minutes, in Miliseconds, is 300000
   (5 x 60 * 1000 )
*/
const cinco = 5 * 60 * 1000;
const diez = 2 * cinco;
const stale = new Date(Date.now() + diez).toISOString();

/*
Not all fields are required for display on most TAK Products, other systems may 
have different requirements. YMMV.
*/

msg.payload = {
    "event": {
        "_attributes": {
            "version": "2.0",
            "uid": "TACO MONSTER",
            "type": "a-f-G-U-S-T-A-C",
            "how": "m-p",
            "time": new Date(Date.now()).toISOString(),
            "start": new Date(Date.now()).toISOString(),
            "stale": stale
        },
        "point": {
            "_attributes": {
                "lat": "37.76",
                "lon": "-122.4975",
                "hae": "0.0",
                "ce": "9999999.0",
                "le": "9999999.0"
            }
        },
        "detail": {}
        }
}

return msg;

And below is the decoded alarm message coming in from the meshtastic alarm node. 

{"payload":{"packet":{"from":2823805675,"to":4294967295,"channel":0,"decoded":{"portnum":10,"payload":"sensor daeb detected\u0007","wantResponse":false,"dest":0,"source":0,"requestId":0,"replyId":0,"emoji":0},"id":840654889,"rxTime":1722206272,"rxSnr":13.5,"hopLimit":3,"wantAck":false,"priority":0,"rxRssi":-37,"delayed":0},"channelId":"otsMesh","gatewayId":"!7ed23018"},"_msgid":"81c727558de1f95e"}

There is also another "heartbeat" status message

{"payload":{"packet":{"from":2823805675,"to":4294967295,"channel":0,"decoded":{"portnum":10,"payload":"sensor daeb state: 0","wantResponse":false,"dest":0,"source":0,"requestId":0,"replyId":0,"emoji":0},"id":840654895,"rxTime":1722206573,"rxSnr":13.25,"hopLimit":3,"wantAck":false,"priority":0,"rxRssi":-37,"delayed":0},"channelId":"otsMesh","gatewayId":"!7ed23018"},"_msgid":"5a7b760cedf1c19f"}

WIll  set up some logic to manually assign static lat/long to the node when it's placed, I believe everything else is either already in the message or can be inferred
