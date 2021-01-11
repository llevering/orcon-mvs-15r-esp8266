# Orcon MVS-15R Wifi control
By default the Orcon mechanical ventilation unit doesn't support any 'smart' connectivity. With help from a forum a topic on Tweakers (dutch)[^1] I gathered a good deal of information and ideas on how to make this device 'smart'.

In the file 'MV-control schema.pdf' you will find the different blocks that together form the schema of the control board. I intended to design a pcb therefore the drawings were made in EasyEDA, but in the end I decided to solder everything myself.

Most components should be clear from the schematics, but a few are not self-explainatory:
1. The connector female to the mainboard of the MV unit itself should be a 'JST PH 4-pin female' (recommendation from Gerard33: https://nl.aliexpress.com/item/33024685895.html).
2. The connector header where the female plug from the fan should connect to is a JST PH 4-pin female (again the unit I ordered didn't fit to well).
3. Any 5v low-active relay will work, 5v or 3.3 high active would work as well. You just need to readjust the 'Bypass relay block' (I used: https://www.tinytronics.nl/shop/nl/diversen/relais/5v-relais-1-channel-laag-actief)
4. For the ESP board I use the Wemos D1 mini v3.1.0, but any ESP8266 will do as long as you can wire it up in one-way or the other.

In the mv.yaml you find an Esphome config file. Esphome can be used to compile the binary and let it upload the binary to the ESP8266. Esphome is a great solution if you want to connect to Home Assistant. In case you like a different home automation solution firmwares like Tasmota, Espeasy and Espurna might be suited to you.

When you use the provided configuration you will notice that the `mv_unit_speed` entity is defined as light. This is done so you can 'dim' the fan from over the full PWM range (from about 15% the fan will start turning). A normal fan component in Esphome only supports three speeds. However stepless dimming is one of the best advantages of this setup. 

[^1]: https://gathering.tweakers.net/forum/list_messages/1806429
