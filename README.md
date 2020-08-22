
# UDControl-Streamdeck - Stream Deck Plugin for Universal Devices

This Stream Deck plugin allows the control of your Universal Devices ISY
Nodes and Programs.  This plugin includes actions for controlling Nodes,
Programs, and some Debugging tools used to help find IDs for configuring
the Nodes & Programs.  This implements the Universal Devices ISY REST API.
Its main features include:

 - Relay Devices (Toggle On/Off)
 - Dimmer Devices (Off/25%/50%/75%/On)
 - Programs (Run, RunThen, RunElse, Stop, Enable, Disable)
 - Long Push implemented
 - JavaScript Based (Tested on Windows)
 - Display Nodes & Programs in ISY
 - Display Node Status
 - No subscription required (Doesn't use ISY Portal)

## Installation / Update

 1. Download the "/Release/com.mazecreator.udcontrol.streamDeckPlugin"
 2. Double click on that file (make sure you have Stream Deck software installed)
 3. Find the desired actions and add them to your Deck as desired

To Update to a newer version, first use the "More Actions..." in the bottom
right corner of the Stream Deck software.  Find "Universal Devices Control"
and "Uninstall...". The older version has to be removed before you can install
a newer version.

## Configure Universal Devices

There are a few items you will need to access your Universal Devices ISY
with the Stream Deck plugin.

 - Device IP address or Name
 - Device Login & Password
 - RestAPI-Link (generally in the form: http://IPAddress/rest/)

These are required for all features.  **IMPORTANT**: Please note, this uses
HTTP not HTTPS and for the Display Actions, the password is passed in plain
text in the URL to a browser so it can be discovered.  This information is
passed in the header of the URLs to control the Nodes & Programs, so again,
it can be intercepted.
### Display Nodes
This opens a URL in your browser using the REST API to dump all known Nodes
for your convenience.  This can be removed from your Stream Deck after
configuration.  These are the required parameters during button configuration:

 - RestAPI-Address: Only enter the IP address of your ISY (eg. 192.168.0.90), this is not a URL
 - User Name: ISY account name (eg. admin)
 - Password: ISY account password, CAUTION plain text so it can be discovered (eg. admin)

Use this to find devices of interest, here is a snippet example of what is
displayed, so you can use a text search to find nodes of interest:

    <node flag="128" nodeDefId="KeypadDimmer_ADV">
    <address>2A 3 EC 1</address>
    <name>Upstairs Hall</name>
    <parent type="3">47504</parent>

This shows the device is in the "Upstairs Hall", it is also a KeypadDimmer
and has a NODE Name "2A 3 EC 1".  You can guess at the Node Name from using
the Device ID for the ADMIN control panel by using the device ID.
For example, this one was listed as 2A 03 EC 1 (some views will not include
the "1", but you need to add it).  Also note, the "3" in the NODE Name does
not contain the leading "0", this needs to be left off.
### Display Programs
This opens a URL in your browser using the REST API to dump all known
Programs for your convenience.  This can be removed from your Stream Deck
after configuration.  These are the required parameters during button
configuration:

 - RestAPI-Address: Only enter the IP address of your ISY (eg. 192.168.0.90), this is not a URL
 - User Name: ISY account name (eg. admin)
 - Password: ISY account password, CAUTION plain text so it can be discovered (eg. admin)

Use this to find program of interest, here is a snippet example of what is
displayed, so you can use a text search to find the name of interest:

    <program id="0006" parentId="0019" status="false" folder="false" enabled="false" runAtStartup="false" running="idle">
    <name>Flash Front Livingroom</name>
    <lastRunTime>2020/08/22 5:18:33 PM</lastRunTime>
    <lastFinishTime>2020/08/22 5:18:35 PM</lastFinishTime>
    </program>

This shows the program "Flash Front Livingroom".  The Program ID is "0006".
It needs to be entered with the leading zeros unlike in the Nodes.  This
information can be found in the Administrative Console as well in the
"Programs -> Summary -> ID" column.

### Node Control
This action is used to control Lights, Relays, Scenes, and dimmers.
The status of these devices is feedback to the button for visual
notification.  These are the required parameters during button
configuration:

 - RestAPI-link: URL to the ISY REST API, usually http://{IPADDRESS}/rest/
 - NODE Name: Contains the Node ID or Scene ID (Do not include leading 0's in hex addresses)
 - Toggle Only?: set to '0' to allow for dimmers to range from Off, 25%, 50%, 75%, On with push of button, '1' will make the button act as On/Off only (Relays detected automatically will be set to toggle)
 - User Name: ISY account name (eg. admin)
 - Password: ISY account password, CAUTION plain text so it can be discovered (eg. admin)

It will detect if the device is a Relay so it will only Toggle between
On/Off after configured.  "Toggle Only?" will automatically be set to
"1" upon detection.  The NODE Name can be an ID as shown in the Display
Nodes feature, or it can be a scene ID as well which is an integer number.
Both are valid.  Scenes should be set to "Toggle Only?".

A **Long push**, that is holding the button down for 1 second or more,
will toggle that device OFF.  This is useful for Dimmers where you just
want to shut off a device without increasing the brightness first.

### Program Control
This action is used to control Lights, Relays, Scenes, and dimmers.  The
status of these devices is feedback to the button for visual notification.
These are the required parameters during button configuration:

 - RestAPI-link: URL to the ISY REST API, usually http://{IPADDRESS}/rest/
 - Program ID: Four digit code of the program to configure (eg. 000D)
 - Push Command: What action should be taken for that Program ID
 - Long Push Command: What action should be taken for that Program ID when a Long Push is used
 - User Name: ISY account name (eg. admin)
 - Password: ISY account password, CAUTION plain text so it can be discovered (eg. admin)

A push of a configured button will execute the action under "Push Command"
for that Program ID.  A Long Push (hold down for 1 second or more and
release) will cause the associated "Long Push Command" to be executed.
Programs might be able to be used to configure devices that are not
supported as Nodes.

### Display Nodes Status
This opens a URL in your browser using the REST API to dump the status of
all known nodes.  This can be removed from your Stream Deck after
configuration if desired.  These are the required parameters during
button configuration:

 - RestAPI-Address: Only enter the IP address of your ISY (eg. 192.168.0.90), this is not a URL
 - User Name: ISY account name (eg. admin)
 - Password: ISY account password, CAUTION plain text so it can be discovered (eg. admin)

Use this to find the status of your nodes.  Please see Universal Devices
Forum and Developer help for an explanation of what is shown on this screen.
## Contact / Issues

Please open an Issue if you have any Issues, Feature request or Questions.
This is a first release so there are bound to be issues and certainly
improvements.  Feel free to issue a Push if you have a new feature of fix.
It has only been tested with Insteon Dimmers/Switches on Windows 10, but
programs might help you get around this limitation if your device doesn't work.

