# arduimaton
Arduino Library and example sketch to aid in easy deployment of arduimaton nodes

- Adds functionality which leverages RF24Network fragmented payload feature that allows for 144 byte payloads send as fragments
- Uses [Blake2s](https://blake2.net/) keyed hash algorithm to sign the messages with a symmetric key
- Can, and should encode payloads as json strings using ArduinoJson
- Raw payload is comprised of three base64 encoded strings delimeted by periods
    - heartbeat.payload.hash:
    - `MTQ1OTU3MDUzNA==.MTQ1OTU3MDUzNA==.MzNkZWNlYTFkOTRm`
    - `1459570534.1459570534.33decea1d94f` 
        - This example is a heartbeat payload, broadcasted by the master on a regular interval
    - Heartbeat payloads are 50 bytes, which is atleast 3 RF24Packets. TODO: if it was 48 could be reduced to 2 packets... 
    - Header will always be 16 bytes, could probably be smaller if handled padding better...
    - By default calculates a short 6 byte signed hash of the payload, encodes it and appends it to the end, same as [JWT](http://jwt.io/).
    - Size of hash digest, and the symmetric secret message signing key can be configured.
- Payloads currently expire within `1` second of being sent, to protect against replay attacks
- Relays message published to specified MQTT Topics to the addressed nodes, to be explained in usage section

## Installation
Download required dependencies and place them in your `Arduino/libraries` folder

- Available on Arduino Library Manager:
    - [RF24](https://github.com/TMRh20/RF24)
    - [RF24Network](https://github.com/TMRh20/RF24Network)
    - [ArduinoJson](https://github.com/bblanchon/ArduinoJson)
- Not on library manager, need to get straight from Github:
    - [CryptoLibs by rweather](https://github.com/rweather/arduinolibs)
    - [Base64](https://github.com/adamvr/arduino-base64) 
      *Not the same as the base64 on Arduino Library*

clone this repository into your `Arduino/libraries` folder (for easy updates via `git pull`)
`git clone git@github.com:arduimatons/arduimaton.git`

## Configuration `arduimaton_config.h`
Arduimaton nodes must have the same secret key configuration as the Automatond master node.
```
 #define SECRET_KEY "thisisaverysecretkey"
 #define DIGEST_SIZE 6
```

## TODO
- Shrink Arduimaton class somehow... 
- More example sketches
