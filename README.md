[![license-badge][]][license] ![version] [![stars][]][stargazers] ![hit-count] [![github-issues][]][issues]

# tthRelay
This is Time, Temperature and Humidity Relay.

![alt text][relay_config_page_image]

- manual mode on/off
- time mode from hh:mm to hh:mm
- temperature mode (cooling/heating) with adjustable hysteresis and time priority from hh to hh
- humidity mode (humidifier/dehumidifier) with adjustable hysteresis and time priority from hh to hh
- support Normally Open/Normally Closed relay
- support single shot to simulate momentary button press with adjustable time from 150 milliseconds to 500 milliseconds in 50 millisecond steps
- in case of sensor failure, the relay goes into the off state - only manual and switching by time will work
- if two sensors with different addresses are connected and one of them fails during boot, the second sensor will be used automatically
- you can have as many relays on the network as you want as long as they all have different hostnames

**The software is provided "AS IS" without warranty of any kind. Don't leave it unattended.**

- Download **Flash Download Tools** from https://www.espressif.com/en/support/download/other-tools
- Download tthRelay *.bin files
- In Flash Download Tools:
    - set SPI speed **80MHz**
    - set SPI Mode **QIO**
    - set Flash Size **32Mbit**
    - check **DoNotChgBin**
    - **fw_latest.bin** at address **0x00000**
    - **fs_latest.bin** at address **0x200000**
- Connect any ESP8266 with **QIO 4MB** flash to USB, select COM port and baud rate than press **Start**

![alt text][flash_download_tools_image]

- Connect HTU2xD/SHT2x/Si70xx or AHT1x/AHT2x digital humidity and temperature Sensor as follows:
    - ESP-01 **(1)**:
      - GPIO3/RX to SCL
      - GPIO2/D4/LED to SDA
      - Vcc
      - Gnd
    - ESP-12, NodeMCU, Snoff Basic, WeMos:
      - GPIO5/D1 to SCL
      - GPIO4/D2 to SDA
      - Vcc
      - Gnd

- Connect relay as follows:
    - ESP-01 **(1)**:
      - GPIO0/D3
    - Snoff Basic:
      - GPIO12/D6
    - ESP-12, NodeMCU, WeMos:
      - GPIO0/D3
      - GPIO12/D6
      - GPIO13/D7
      - GPIO14/D5
    - recommended to add a 680ohm/220uF RC filter to prevent accidental switching on startup, see [ESP8266 GPIO Behaviour at Boot](https://rabbithole.wwwdotorg.org/2017/03/28/esp8266-gpio.html)

**(1)** To work on the ESP-01, the flash memory must be replaced with 4MB/16Mbit.

![alt text][gpio_rc_mode]
![alt text][wifi_relay_module]
![alt text][wifi_relay_schematic_mode]

- Connect to **tthRelay** WiFi access point using password **12345678**
- Type in browser http://192.168.4.1/
- Put **User Name**: _admin_ and **Password**: _12345678_
- For security purposes, please change login/password for the access point **Settings -> Access Point Config** and **Settings -> Server Config** page then click **Save**
- Set WiFi Network name and password in **Settings -> Station Config** page than click **Save** and **Reboot**
- The tthRelay will connect to the WiFi network and **tthRelay** access point will disappear
- Type in browser http://tthRelay.local/ (use IP address instead of mDNS on Android and Win7 devices, address can be found in the UART logs at speed 115200bps)
- Go to **Time** or **Settings -> NTP Config** and set your timezone than click **Save** and **Reboot**
- Test relay in manual mode **Relay -> Manual** or **Settings -> Relay Config -> Manual**, if it doesn't switch then click on **Advance** and rearrange **Relay Pin**, **Relay Type** then **Save** and **Reboot**

Used frameworks, libraries:
- [Arduino ESP8266](https://github.com/esp8266/Arduino)
- [ArduinoJson](https://github.com/bblanchon/ArduinoJson)
- [ArduinoStreamUtils](https://github.com/bblanchon/ArduinoStreamUtils)
- [AHT1x/AHT2x](https://github.com/enjoyneering/AHTxx)
- [HTU2xD/SHT2x/Si70xx](https://github.com/enjoyneering/HTU2xD_SHT2x_Si70xx)


[license-badge]: https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg
[license]:       https://creativecommons.org/licenses/by-nc-nd/4.0/
[version]:       https://img.shields.io/badge/Version-1.0.0-green.svg
[stars]:         https://img.shields.io/github/stars/enjoyneering/tthRelay.svg
[stargazers]:    https://github.com/enjoyneering/tthRelay/stargazers
[hit-count]:     https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fenjoyneering%2FtthRelay&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false
[github-issues]: https://img.shields.io/github/issues/enjoyneering/tthRelay.svg
[issues]:        https://github.com/enjoyneering/tthRelay/issues/

[relay_config_page_image]:    https://github.com/enjoyneering/tthRelay/blob/main/images/tthRelay_relay_config_advance_heater.png
[flash_download_tools_image]: https://github.com/enjoyneering/tthRelay/blob/main/images/flash_download_tools.png
[gpio_rc_mode]:               https://github.com/enjoyneering/tthRelay/blob/main/images/gpio_rc_mode_esp8266.png
[wifi_relay_module]:          https://github.com/enjoyneering/tthRelay/blob/main/images/wifi_relay_module_ESP-01.jpg
[wifi_relay_schematic_mode]:  https://github.com/enjoyneering/tthRelay/blob/main/images/wifi_relay_module_schematic_mode_ESP-01.png
