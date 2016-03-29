# arduimaton
Arduino Library and example sketch to aid in easy deployment of arduimaton nodes

- Inherits the RF24Network class, adds a 'secure' message signing and authentication functionality.
- Uses Blake2s keyed hash algorithm to sign the messages
- Can, and should encode payloads as json strings using ArduinoJson
- Raw payload is comprised of two base64 encoded strings delimeted by a period
 - payload.hash `WyJzd2l0Y2hlcyIsIjAuMC4xIiwxNSwxNDU5MjkyMDM0XQ==.NWI2NDdiNDFlNDU3`
 - Similar structure to a [JWT](http://jwt.io/)
  - arduimaton signs the raw payload rather than encoded payload

## Installation

1. Download required dependencies and place them in your `Arduino Libraries` folder
 - Available on Arduino Library Manager:
  - [RF24](https://github.com/TMRh20/RF24)
  - [RF24Network](https://github.com/TMRh20/RF24Network)
  - [ArduinoJson](https://github.com/bblanchon/ArduinoJson)
 - Not on library manager, need to get straight from Github:
  - [CryptoLibs by rweather](https://github.com/rweather/arduinolibs)
  - [Base64](https://github.com/adamvr/arduino-base64)
2. `git clone` this repository into your `Arduino Libraries` folder (for easy updates via `git pull`) 

## Configuration `arduimaton_config.h`
A Arduimaton node must have the same secret key configuration as the Automatond master node.
```
 #define SECRET_KEY "thisisaverysecretkey"
 #define DIGEST_SIZE 6
```

## TODO
- Shrink Arduimaton class somehow... 
- More example sketches