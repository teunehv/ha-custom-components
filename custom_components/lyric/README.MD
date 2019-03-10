# General
##### Code originally realized by
https://github.com/bramkragten/

##### Community forum
https://community.home-assistant.io/t/honeywell-lyric-thermostat/

# Steps to perform 
Here is a summary of the installation steps for those who follow. If you find any errors, please send me a message and I will amend the text. Originally [summarized](https://community.home-assistant.io/t/honeywell-lyric-thermostat/3520/487) by [rwpalmer](https://community.home-assistant.io/u/rwpalmer), edited by [teunvh](https://community.home-assistant.io/u/teunehv).

### Part 1: Obtain client key & secret from Honeywell
1. Visit [Honeywell Developers](http://developer.honeywell.com/), and sign in. Create an account if you don’t have one already.
2. Fill in account details and submit changes
3. Click “My Apps 1” at top of page, under your account.
4. Click “Create New App ” Fill in details:
* App name. Can be anything, I use Home Assistant.
* In the “Callback URL” enter the IP address to your Home Assistant instance, ie: http://192.168.1.215:8123/api/lyric/authenticate
5. Click “Save Changes”
6. On the apps page, click on the just created app.
7. The “Consumer Key” and “Consumer Secret” are shown now. Be sure to copy these fields before you leave the Honeywell site. You’ll need to insert them into the configuration.yaml or secrets.yaml file.

### Part 2: Download Lyric files and install them in Home Assistant
Download the following 3 files from the [repo](https://github.com/teunehv/ha-custom-components/tree/master/custom_components/lyric).

And store them in your home assistant custom_components folder. The “custom_components” folder must exist in the same Home Assistant root folder where your configuration.yaml resides. The custom_components must contain a subfolder lyric. It should look like below
```
<home-assistant-config-folder>/custom_components/lyric/__init__.py
<home-assistant-config-folder>/custom_components/lyric/climate.py
<home-assistant-config-folder>/custom_components/lyric/services.yaml
```

## Part 3: Modify Home Assistant YAML files:
Store the key and secret that you obtained from Honeywell in your secrets.yaml file. example below:
```
lyric_client_key: your-key-here
lyric_client_secret: your-secret-here
```
Add the Lyric Thermostat to your configuration.yaml file. example below:

```
###############################################
#         Honeywell Lyric Thermostat          #
###############################################
lyric:
  client_id: !secret lyric_client_key
  client_secret: !secret lyric_client_secret
```

Check “base_url” in your configuration.yaml. To authenticate with Honeywell, your “base_url” must concatenate with “/api/lyric/authenticate” to produce the “Callback URL” that you registered with Honeywell.

```
###############################################
#                    http                     #
###############################################
http:
  base_url: https://192.168.1.215:8123
```

## Part 4: Reboot Home Assistant

After a reboot, Home Assistant should present a card to configure the Lyric Thermostat. You will be asked to authenticate with the Honeywell Developer’s site, and ultimately, the Home Assistant front-end should display a Climate card for the Lyric Thermostat.

## Known issues:
* Lyric fan controls are not currently supported
* Lyric outdoor temperature sensors are not currently supported
* Lyric indoor humidity sensor is not currently supported
* Advanced features, like the control of dual heating systems are not supported.
