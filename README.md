# Multi-Account Containers

[What is Multi-Account Containers?](https://blog.mozilla.org/firefox/introducing-firefox-multi-account-containers/)

The Firefox Multi-Account Containers extension lets you carve out a separate box for each of your online lives – no more opening a different browser just to check your work email!

[Available on addons.mozilla.org](https://addons.mozilla.org/en-GB/firefox/addon/multi-account-containers/)

**Note:** Firefox 57 users should Install from our [latest GitHub Release](https://github.com/mozilla/testpilot-containers/releases/latest)

For more info, see: 

* [Test Pilot Product Hypothesis Document](https://docs.google.com/document/d/1WQdHTVXROk7dYkSFluc6_hS44tqZjIrG9I-uPyzevE8/edit#)
* [Shield Product Hypothesis Document](https://docs.google.com/document/d/1vMD-fH_5hGDDqNvpRZk12_RhCN2WAe4_yaBamaNdtik/edit#)


## Requirements

* node 7+ (for jpm)
* Firefox 53+


## Development

### Web Extension Development

Since Firefox 57, this extension can now be run without any of the legacy components that were previously needed.

1. Install web-ext with npm
2. cd webextension; web-ext run -f Nightly

This will work in other builds of Firefox however certain features won't work and you will need to manually flip preferences to enable containers. All other sections of this guide talk about using the legacy setup with jpm.


## Legacy Development

### Development Environment

Add-on development is better with [a particular  environment](https://developer.mozilla.org/en-US/Add-ons/Setting_up_extension_development_environment). One simple way to get that environment set up is to install the [DevPrefs add-on](https://addons.mozilla.org/en-US/firefox/addon/devprefs/). You can make a custom Firefox profile that includes the DevPrefs add-on, and use that profile when you run the code in this repository. 

1. Make a new profile by running `/path/to/firefox -P`, which launches the profile editor. "Create Profile" -- name it whatever you wish (e.g. 'addon_dev') and store it in the default location. It's probably best to deselect the option to "Use without asking," since you probably don't want to use this as your default profile.

2. Once you've created your profile, click "Start Firefox". A new instance of Firefox should launch. Go to Tools->Add-ons and search for "DevPrefs". Install it. Quit Firefox.

3. Now you have a new, vanilla Firefox profile with the DevPrefs add-on installed. You can use your new profile with the code in _this_ repository like so:

#### Run the `.xpi` file in an unbranded build
Release & Beta channels do not allow un-signed add-ons, even with the DevPrefs. So, you must run the add-on in an [unbranded build](https://wiki.mozilla.org/Add-ons/Extension_Signing#Unbranded_Builds):

1. Download and install an un-branded build of Firefox
2. Download the latest `.xpi` from this repository's releases
3. Run the un-branded build of Firefox with your DevPrefs profile
4. Go to `about:addons`
5. Click the gear, and select "Install Add-on From File..."
6. Select the `.xpi` file

#### Correct prefs

Whilst this is still using legacy code to test you will need the following in your profile:

Change the following prefs in about:config:

- extensions.legacy.enabled = true
- xpinstall.signatures.required = false


#### Run the TxP experiment with `jpm`

1. `git clone git@github.com:mozilla/testpilot-containers.git`
2. `cd testpilot-containers`
3. `npm install`
4. `./node_modules/.bin/jpm run -p /Path/To/Firefox/Profiles/{junk}.addon_dev -b FirefoxBeta` (where FirefoxBeta might be: ~/<reponame>/obj-x86_64-pc-linux-gnu/dist/bin/firefox or ~/<downloadedFirefoxBeta>/firefox)

Check out the [Browser Toolbox](https://developer.mozilla.org/en-US/docs/Tools/Browser_Toolbox) for more information about debugging add-on code.

### Building .xpi

To build a local testpilot-containers.xpi, use the plain [`jpm
xpi`](https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/jpm#jpm_xpi) command,
or run `npm run build`.

### Signing an .xpi

To sign an .xpi, use [`jpm
sign`](https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/jpm#jpm_sign)
command.

Note: You will need to be [an author on the AMO
add-on](https://addons.mozilla.org/en-US/developers/addon/containers-experiment/ownership).

### Testing
TBD

### Distributing
TBD

### Links

- [Licence](./LICENSE.txt)
- [Contributing](./CONTRIBUTING.md)
- [Code Of Conduct](./CODE_OF_CONDUCT.md)
