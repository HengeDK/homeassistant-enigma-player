
  - Change channel (Selecting from source list or via Right/Left - from remote controller)
  - Change channel (using channel number)
  - Current channel and current event
  - Picon from current channel (default)
  - Screenshot from current channel
  - Supports authentication and multiple receivers
  - Sending notifications to the box (timeout and type of message can be selected)
  from picon)
    
# Minimum Requirements
  - Homeassistant 0.88

# Tested with OpenWebif versions:
  - 0.2.7
  - 1.3.0

# Install:
To use the enigma custom component, place the file `enigma` directory from the root of
the repositorie in to the folder `~/.homeassistant/custom_components/` where
you have your home assistant installation

The custom components directory is inside your Home Assistant configuration directory.

This is how your custom_components directory should be:
```bash
custom_components
├── enigma
│   ├── __init__.py
│   ├── media_player.py
│   └── notify.py
```
# Configuration Example:
By Default will load all channels from first bouquet

```yaml 
enigma: 
  devices:
    - host: 192.168.1.200
      port: 80
      name: Vu
      timeout: 20
      username: root
      password: your_password
      picon: picon

notify:
  - platform: enigma
    host: 192.168.1.200
    port: 80
    username: root
    password: your_password
    name: Vu
```

# Configuration Example 2 (using multiple devices and a pre-defined bouquet and icon from screenshot):
To get your bouquet references, open in your browser : http://box.ip/web/getservices


You can find your bouquet reference from as follows:

Example
	```
	1:7:1:0:0:0:0:0:0:0:FROM BOUQUET "userbouquet.favourites.tv" ORDER BY bouquet BOUQUET_NAME_HERE
	```
 
In my case, if I want to load all channels from bouquet Sky Deutschland I have to look for:
	```
	1:7:1:0:0:0:0:0:0:0:FROM BOUQUET "userbouquet.dbe1e.tv" ORDER BY bouquet Sky Deutschland
	```
 
Then copy the entire string, removing the bouquet name from the end
 
Example, where I want to load all bouques from the Sky Deutschalnd bouquet:
```yaml 
enigma: 
  devices:
    - host: 192.168.1.200
      port: 80
      name: Gigablue
      timeout: 20
      username: root
      password: your_password
      picon: picon
    - host: 192.168.1.210
      port: 80
      name: Dreambox 
      username: root
      password: your_password
      timeout: 20
      bouquet: '1:7:1:0:0:0:0:0:0:0:FROM BOUQUET "userbouquet.dbe1e.tv" ORDER BY bouquet' 
      picon: screenshot
```

# Notifications
To send notification you can use your HA services page (see screenshot below).
Choose your service `notify.dreambox` and add the following service data:

```js
{ "message" : "Test 123",
  "data" : { 
      "displaytime" : "10",
      "messagetype" : "2"
      }
}
```

# Change channel
To change channel you can use your HA services page (see screenshot below).
Choose the service `media_player.play_media`, choose yourt entity
`media_player.dreambox` and add the following service data (`media_content_id` is
you channel number):

```js
{ "entity_id" : "media_player.dreambox",
  "media_content_id" : "5",
  "media_content_type" : "channel"
}
```

# Custom updater
If you want this custom component to be auto updated, please add the
configuration below to your configuration.yaml
Make sure you've the custom_updater component installed and working - https://github.com/custom-components/custom_updater/ 

Add a new reference under component_urls in your custom_updater configuration in configuration.yaml.
```yaml
custom_updater:
  component_urls:
    - https://raw.githubusercontent.com/HengeDK/homeassistant-enigma-player/master/custom_components.json
```


# Screenshots
Current channel (example 1)

![Channel example 1](../master/screenshots/1.png)


Current channel (example 2)

![Channel example 2](../master/screenshots/2.png)


Current channel options

![In detail](../master/screenshots/3.png)


Change channel from bouquet list

![Change source](../master/screenshots/4.png)


Call service to send a notification

![Send notification](../master/screenshots/5.png)


Call service to change to specified channel number

![Change channel number](../master/screenshots/6.png)



# Contact


# License

# References

[1]: https://home-assistant.io

