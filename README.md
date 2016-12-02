# Rancilio Silvia Temperature PID

About the Rancilio Silvia (general construction and details):
 * http://www.pidsilvia.com/whypid.htm

Usefull links and similar projects:
 * http://ispresso.net
 * http://josh.to/crema/
 * https://mecoffee.nl
 * https://gonium.net/blog/2010/12/12/das-leben-ist-zu-kurz-fur-schlechten-kaffee

## Get all the parts together

1. Adafruit HUZZAH ESP8266 breakout
2. Temperature Sensor DS18B20
3. Serial Converter USB BTE13-007 CP2102
4. SSD1306 128x64 OLED Display

## Final controller design
![Alt text](img/WebCoffee_controller.png?raw=true "Microcontroller design")

## Meassuring the temperature
As a first step I wanted to find out, how good or bad the built-in thermostat in the Rancilio Silvia does its job. So I just put a temperature sensor on the boiler and wrote some code to read the temperature from the DS18B20 temp. sensor on the ESP8266. The temperature is publish it as a REST service (JSON) on a simple HTTP web server on the ESP8266. For the client I wrote a shell script that regularly polls the web server and writes the temperature to a log file.

Here is the resulting graph:
![Alt text](img/ranc_silvia_temp_curve.png?raw=true "Rancilio Silvia Temperature Curve")

After around 2230 seconds, I pushed the button to pump water through the group head, as if I was going to make some espresso. The temperature drops almost for 10 degrees Celsius during the espresso making process. Right after finishing the espresso making, I switched on the steam button. The DS18B20 is only able to measure temperature up to 127 degrees Celcius, but I guess the temperature got a bit higher than that. After reaching the steam temperature, I simulated the milk steaming process. Right after that, I switched off the steam button and released steam through the group head until water came out and the boiler thermostat kicked in again ("boiler cool down").

![Alt text](img/ranc_silvia_temp_curve_2.png?raw=true "Rancilio Silvia Temperature Curve - Coffee and Steaming")
