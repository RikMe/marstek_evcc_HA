# Integrating a Marstek Venus-E V3 with Home assistant and EVCC
This repository has the sole purpose of describing my personal integration of the Marstek Venus-E V3 with Home Assistant and EVCC trough modbus. 

*Please note that there are many alternatives and different approaches. There is no single 'right' approach.*

## Hardware
- Marstek Venus V3
  - Firmware version (EMS) : 145
  - BMS : 110
- Home Assistant Green
- Home Wizard P1 meter
- Home network on the Unifi platform

## Software
- Marstek app (only for initial config & software update)
- Home assistant OS (updated to the latest version)
- EVCC running as add-on in Home Assistant (updated to the latest version)
### Home Assistant add-ons
- EVCC : https://github.com/evcc-io/hassio-addon
- B2500 meter by Tom Quist : https://github.com/tomquist/b2500-meter
### Home Assistant integrations
- Marstek Modbus by Viper : https://github.com/viperrnmc/marstek_venus_modbus
- HA-EVCC by Matthias Marquardt : https://github.com/marq24/ha-evcc

## Configuration
### Battery
The Marstek app is not a textbook example of stability. It is however sufficient for initial configuration. Personally i don't use the app for anything after that. In order to access the modbus interface, the battery needs to have a wired connection to the network. No specfic settings are required for the modbus connection.
### Updating Marstek firmware
The Marstek app will not propose firmware updates by itself. You can request to push updates manually trough the support section in the app. Manually update only if you require new features that are not available to you yet or in case of security iccues. 
*If it ain't broken, don't fix it.*
### Modbus connection
The Venus-E V3 contains 2 RJ45 ports
- RS485 for direct modbus
- Ethernet

The RS485 can be used to connect dedicated modbus hardware (ex. LILYGO or Elfin). As from firmware V144 however, the modbus interface is also available on the standard ethernet port over modbus TCP (Port 502). A hard wired connection to the home network is sufficient to access the modbus interface. For most use cases the RS485 port becomes obsolete. In some cases (ex. when no wired network is available) i might still be usefull to use a modbus-WiFi converter.
### Virtual P1 meter
During testing I found most Wi-Fi connectecions to P1 meters to be unstable. (tested with Marstek CT003 dongle & Home Wizard P1) The [B2500 Meter](https://github.com/tomquist/b2500-meter) add-on for Home Assistant allows you to create a virtual shelly device on your network based on any power sensor available. This virtual device can be assigned to the Marstek Venus. In my case the add-on is pointed towards the "Power" entity of the Home Wizard P1 dongle.

<img width="529" height="380" alt="Screenshot 2026-01-17 at 10 37 18" src="https://github.com/user-attachments/assets/eefc7fbb-bee4-4d0c-b79d-9beeff2e5b95" />


### Home assistant
The configuration of the [Marstek Modbus integration](https://github.com/viperrnmc/marstek_venus_modbus) in Home Assistant should be straight forward. Simply point the integration towards the the modbus interface.
- When using the ethernet port this is simply the IP of the Marstek Venus-E
- When using the dedicated RS485 port with a dedicated modbus dongle this is the IP of the modbus dongle.


<img width="451" height="587" alt="Screenshot 2026-01-17 at 10 40 53" src="https://github.com/user-attachments/assets/a6b62bca-26e9-43a8-b9c1-17cc86966ea6" />


### EVCC

