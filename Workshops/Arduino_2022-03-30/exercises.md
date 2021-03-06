# Arduino Exercises

## Arduino Background

[Some background](arduino_background.md)

## Exercise 1: Install Arduino IDE

<details>
	<summary>Hints</summary>

* The official Arduino website is https://www.arduino.cc/

  - Download the IDE from https://www.arduino.cc/en/software
    - Arduino IDE 1.8.19: The standard Processing like IDE (most tutorials refer to this)
    - Arduino IDE 2.0 RC: The modern VSCode-like IDE (uses the same libraries and board-definitions)
    - There is also a web-based editor: https://create.arduino.cc/editor
  - Install according to operating system
  - Consider giving them a donation
</details>

## Exercise 2: Install ESP32 board definition

<details>
	<summary>Hints</summary>

* The ESP32 support is hosted here: https://docs.espressif.com/projects/arduino-esp32/en/latest/index.html. [Installation instructions](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html)
* Here's a step-by-step guide with screenshots: https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/
 - Start the Arduino IDE
 - Open preferences: `Ctrl-,` ( or File -> Preferences / Fil -> Egenskaber)
 - Copy-paste the stable release link into the box: `Additional Boards Manager URLs` (https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json)
 - Go to Tools -> Board (display current board) -> Boards Manager.
 - Search for esp32
 - Click install (version 2.0.0 currently)
 - Wait for the board definition to install
 - Now select the board: ESP32 Dev module (or Node32s?)
 - Restart the Arduino IDE
* On Ubuntu you need to add yourself to `dialout` group and install `pyserial`.
  Reboot after this!
```
 sudo usermod -a -G dialout $USER 
 sudo apt install  python3-serial
```
  Check that it worked with `id`. It should include `dialout` in the list.
</details>

## Exercise 3: Write a simple program

<details>
	<summary>Hints</summary>
- Test an example: File -> Examples -> 01.Basics -> BareMinimum
  Edit:

```
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
}

void loop() {
  // put your main code here, to run repeatedly:
  Serial.println("Hello");
  delay(1000);                       // wait for a second
  Serial.println("World");
  delay(1000);                       // wait for a second 
}
```

* Select the correct COM port. In my test on windows it was COM5.
* Open the Monitor `Ctrl-Shift-M` (Tools -> Serial Monitor)
* Set to 115200 baud
* ESP32 specific examples: https://github.com/espressif/arduino-esp32/tree/master/libraries
  Eg https://github.com/espressif/arduino-esp32/blob/master/libraries/ESP32/examples/ChipID/GetChipID/GetChipID.ino
  My chip is "ESP32-D0WDQ6 Rev 1"
* Note: You need to hold down the "Boot" button on the ESP32 while uploading.
</details>


## Exercise 4: LED on breadboard

<details>
	<summary>Hints</summary>

* Example here: https://microcontrollerslab.com/gpio-pins-esp32-led-blinking-example/
* Datasheet here: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf

* Compute the resister to use to allow max 10 mA to flow through the LED, when the board supplies 3.6V (https://microcontrollerslab.com/esp32-pinout-use-gpio-pins/ says 20mA, https://microcontrollerslab.com/gpio-pins-esp32-led-blinking-example/ says 10 mA)
  See also https://community.blynk.cc/t/esp32-gpio-pins-info-restrictions-and-features/43166

* Connect resistor and LED between GDN and pin D22

- Avoid: GPIO34-39 (only digital input)
  - Check pinout here:  https://microcontrollerslab.com/esp32-pinout-use-gpio-pins/

* To blink the on-board LED: Use `int LED_BUILTIN = 2;`

</details>

## Exercise 5: Add DHT11 temperature sensor
<details>
	<summary>Hints</summary>

- Tutorial: https://randomnerdtutorials.com/esp32-dht11-dht22-temperature-humidity-sensor-arduino-ide/
	
</details>

## Exercise 5.a: Add BME280 temperature sensor

<details>
	<summary>Hints</summary>

- See https://randomnerdtutorials.com/esp32-bme280-arduino-ide-pressure-temperature-humidity/
- Add board definition
- Connect via i2c interface (gpio21, gpio22 according to https://microcontrollerslab.com/esp32-pinout-use-gpio-pins/)

</details>

## Exeercise 6: Display temperature with LED

<details>
	<summary>Hints</summary>
- write program to turn on LED when temperature is above threshold
</details>

## Extra Exercise Stream temperature over MQTT to Grafana dashboard on Raspberry pi

