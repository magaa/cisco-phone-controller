# Cisco Phone Controller (Beta)
Chrome extension, which embeds a Remote Phone Control App on the Phone's Web Page

> **Version 2.0 Beta** – migrated to Manifest V3 and works on localized phone web pages (e.g. German), not only English ones. It is not published in the browser stores; install it locally as described below.

# Required Setup (CUCM)
The extension needs a CUCM user that controls the phone. No roles or access control groups are required.

1. **Create the user** – either
   - Application User: *User Management → Application User → Add New*, set User ID and password, or
   - End User: use an existing one (*User Management → End User*).
2. **Assign phones** – in the user's *Device Information* section move the phone(s) from *Available Devices* to *Controlled Devices*, then *Save*.
3. **Enable web access** on each phone – *Device → Phone → (phone) → Product Specific Configuration Layout → Web Access: Enabled*, *Save* and *Apply Config*.

Log in with this user's ID and password when you click "Control Me".

# Installation

1. Download **[cisco-phone-controller.zip](https://github.com/magaa/cisco-phone-controller/releases/download/v2.0-beta/cisco-phone-controller.zip)** (all versions: [Releases](https://github.com/magaa/cisco-phone-controller/releases))
2. Unzip it to a permanent location, e.g. your Documents folder. You get a folder `cisco-phone-controller` that contains `manifest.json`.

## Chrome (and other Chromium browsers like Edge, Brave)
1. Open `chrome://extensions` (Edge: `edge://extensions`)
2. Turn on **Developer mode** (toggle in the top right; in Edge on the left)
3. Click **Load unpacked**
4. Select the unzipped `cisco-phone-controller` folder
5. "Cisco Phone Controller" now appears in the list. It stays installed after restarting the browser.

To update: download the new ZIP, replace the files in the folder and click the reload icon on the extension's card.

Note: do not move or delete the folder afterwards, Chrome loads the extension directly from it.

# Using the Extension
1. Navigate to the phone's web page in your browser
2. If it's a supported phone model, you will see "Control Me" in red at the top of the screen
3. Click "Control Me" and then enter the username and password of your user with control of this phone

Tip: You can even click on the phone screen to access line, softkeys, and session buttons on most models!

# Screenshot
![Screenshot](https://i.imgur.com/TdkqKbx.png)

# Troubleshooting
1. This extension uses the Phone APIs for /CGI/Screenshot and /CGI/Execute.  While it's hard to test the /CGI/Execute, it does generally work or not work in tandem with /CGI/Screenshot.  Therefore, as a test, can you access the phone screenshot outside of this extension by simply nagivating to: http://{phone ip}/CGI/Screenshot?  If not, it's not an extension problem then, you need to doublecheck the phone is reachable via IP, and that your user is properly controlling it, reboot the phone, all the normal stuff, etc.  Until you can get the screenshot to work in a vanilla browser (no extensions required), the extension will not work either.
2. If you are controlling a phone which is MRA registered, and your Authentication URL is not HTTPS, make sure your Expressway-C has an HTTP Allow for the http://{cucm ip}:8080/ccmcip/authenticate.jsp URL.  HTTPS Auth works natively.
3. If you are controlling a phone which is MRA registered, you will need to be able to route to its real IP Address (e.g., be on the same LAN as the phone)
