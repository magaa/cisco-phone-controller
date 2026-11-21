# Cisco Phone Controller (Beta)
Web Browser plugin/addon/extension, which embeds a Remote Phone Control App on the Phone's Web Page

> **Version 2.0 Beta** – migrated to Manifest V3 and works on localized phone web pages (e.g. German), not only English ones. It is not published in the browser stores; install it locally as described below.

# Required Setup
1. You will need either a Cisco Unified Communications Manager (CUCM) End User or Application User
2. Associate one or more phones to the user under Controlled Devices (No groups/roles to assign!)

# Installation

First get the extension files: on GitHub click **Code → Download ZIP** and unzip it, or clone the repository:

```
git clone https://github.com/magaa/cisco-phone-controller.git
```

The extension itself is the `src` folder (it contains `manifest.json`).

## Chrome (and other Chromium browsers like Edge, Brave)
1. Open `chrome://extensions` (Edge: `edge://extensions`)
2. Turn on **Developer mode** (toggle in the top right; in Edge on the left)
3. Click **Load unpacked**
4. Select the `src` folder
5. "Cisco Phone Controller" now appears in the list. It stays installed after restarting the browser.

To update: replace the files in the `src` folder and click the reload icon on the extension's card.

Note: do not move or delete the `src` folder afterwards, Chrome loads the extension directly from it.

## Firefox
Firefox only installs signed add-ons permanently, so there are two options:

### Option A: Temporary (any Firefox version)
1. Open `about:debugging#/runtime/this-firefox`
2. Click **Load Temporary Add-on…**
3. Select the file `src/manifest.json`
4. The add-on is active until Firefox is closed. Repeat these steps after every restart.

### Option B: Permanent (Firefox Developer Edition, Nightly or ESR only)
1. Open `about:config`, search for `xpinstall.signatures.required` and set it to `false`
2. Zip the **contents** of the `src` folder (`manifest.json` must be at the top level of the ZIP, not inside a `src` folder) and rename the file to `cisco-phone-controller.xpi`
3. Open `about:addons`, click the gear icon → **Install Add-on From File…** and select the `.xpi` file

The regular Firefox release ignores `xpinstall.signatures.required`; there only Option A works.

### Firefox: allow site access
If "Control Me" does not show up in Firefox, the add-on may not have permission to run on the phone's page yet. Open `about:addons` → **Cisco Phone Controller** → **Permissions** and allow access to websites, or click the extensions button (puzzle icon) in the toolbar while on the phone's page and allow it there.

# Using the Add-on
1. Navigate to the phone's web page in your browser
2. If it's a supported phone model, you will see "Control Me" in red at the top of the screen
3. Click "Control Me" and then enter the username and password of your user with control of this phone

Tip: You can even click on the phone screen to access line, softkeys, and session buttons on most models!

# Screenshot
![Screenshot](https://i.imgur.com/TdkqKbx.png)

# Troubleshooting
1. This Add-on uses the Phone APIs for /CGI/Screenshot and /CGI/Execute.  While it's hard to test the /CGI/Execute, it does generally work or not work in tandem with /CGI/Screenshot.  Therefore, as a test, can you access the phone screenshot outside of this add-on by simply nagivating to: http://{phone ip}/CGI/Screenshot?  If not, it's not an Add-on problem then, you need to doublecheck the phone is reachable via IP, and that your user is properly controlling it, reboot the phone, all the normal stuff, etc.  Until you can get the screenshot to work in a vanilla browser (no add-ons required), the Add-on will not work either.
2. If you are controlling a phone which is MRA registered, and your Authentication URL is not HTTPS, make sure your Expressway-C has an HTTP Allow for the http://{cucm ip}:8080/ccmcip/authenticate.jsp URL.  HTTPS Auth works natively.
3. If you are controlling a phone which is MRA registered, you will need to be able to route to its real IP Address (e.g., be on the same LAN as the phone)
