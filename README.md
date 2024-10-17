# manual of how connect the weather to a led strip

## table of contents 
1. **Introduction**
2. **Materials Needed**
3. **Step 1: Setting Up**
4. **Step 2: Understanding the API**
5. **Step 3: Arduino Code**
6. **Step 4: Testing**
7. **step 5: Errors**
8. **Conclusion**
9. **my product**

---

## 1. Introduction


This manual will guide you through connecting your Arduino to the OpenWeatherMap API to control an LED strip based on the current weather temperature. The LED strip will change colors according to different temperature ranges. I made this manual for my project for IOT, i made a closet surrounded with a led strip that can change colours based on the weather.
<img width="461" alt="stylesync" src="https://github.com/user-attachments/assets/afbe5493-9278-4ddf-896d-71a3c2e84c00">

## 2. Materials Needed
- **Arduino Board** (e.g., Arduino Uno or ESP8266)
- **LED Strip** (compatible with Arduino, like the NeoPixel strip)
- **computer** (to connect the arduino to and implement the code)
- **Wi-Fi Connection** (to connect to the internet)
- **OpenWeatherMap API Key** (free to sign up on their website)
- **Arduino IDE** (for coding and uploading to your Arduino)

## 3. Step 1: Setting it Up 

1. **Install the Arduino IDE**:
   - Download the Arduino IDE from the [official website](https://www.arduino.cc/en/software) and install it on your computer.
   <img width="891" alt="Screenshot 2024-10-17 at 14 53 48" src="https://github.com/user-attachments/assets/c67a7d6d-11fd-416c-b552-4f1036d4b131">
2. **Install the Required Libraries**:
   - Open the Arduino IDE and go to `tools` > `Manage Libraries...`.
   - In the Library Manager, search for `Adafruit NeoPixel` and install it.
     <img width="764" alt="Screenshot 2024-10-17 at 14 59 51" src="https://github.com/user-attachments/assets/ca5c8f12-5485-45be-a012-e39850fb7398">
   - Make sure to also install `ArduinoJson` library for parsing JSON dat. Its possible that it says that ArduinoJson doesnt work, so         make sure you download ArduinoJson 6.XXXX not 7.XXXX , otherwise it says this ->
   <img width="789" alt="Screenshot 2024-10-17 at 14 58 55" src="https://github.com/user-attachments/assets/edae6143-9ed1-4446-81bf-0ee89222dbf1">
 3. **Connect Your Arduino**:
   - Use a USB/USBC cable to connect your Arduino board to your computer.
   - Select the correct board and port from `Tools` > `Board` > `Boardmanager`. type in the     searchbar: "esp8266" -> select "esp8266" by "ESP8266 Community". click install.
   - now you have to connect the port. you do this by choosing `Tools` > `Board` > `esp8266 Boards` > `choose NodeMCU 1.0` you have now connected your arduino!

## 4. Step 2: Understanding the API

1. **What is an API?**  
   An API (Application Programming Interface) allows different software applications to communicate with each other. In this manual, we will use the OpenWeatherMap API to get weather information.

2. **Getting Your API Key**:
   - Go to the [OpenWeatherMap website](https://openweathermap.org/).
   - Sign up for a free account.
   - After logging in, navigate to the API keys section in your account dashboard and copy your API key.

     <img width="145" alt="Screenshot 2024-10-17 at 15 26 29" src="https://github.com/user-attachments/assets/44887029-018b-48ea-a746-2854599da724">

3. **Finding the City ID**:
   - Use the City Search feature on the OpenWeatherMap website to find your city. For Amsterdam, the city ID is `2759794`. The City ID can be found in your browser's address bar
     <img width="1024" alt="Screenshot 2024-10-17 at 15 35 54" src="https://github.com/user-attachments/assets/05fe5c97-cf60-465a-aaa8-e707e72c820b">
   - You can use this URL in your browser to confirm the city ID, first you have to log in:
   [OpenWeatherMap website](https://openweathermap.org/). If you click on this you can find your API key.
  <img width="307" alt="Screenshot 2024-10-17 at 15 29 21" src="https://github.com/user-attachments/assets/e5c8cf57-220d-4aa8-a345-ed57b3baf8df">

## 5. Step 3: Arduino Code 

1. 
<img width="549" alt="Screenshot 2024-10-17 at 15 43 11" src="https://github.com/user-attachments/assets/5c297be1-984e-44cc-b9f7-555f08b091e8">

- <ESP8266WiFi.h>: This library allows the ESP8266 to connect to a Wi-Fi network.
- <ArduinoJson.h>: Used to parse JSON responses from APIs like OpenWeatherMap.
- <Adafruit_NeoPixel.h>: This library is used to control the NeoPixel LED strip.

2.
<img width="453" alt="Screenshot 2024-10-17 at 15 52 26" src="https://github.com/user-attachments/assets/c274ab63-262f-451a-8f8b-2ef20ed37f3b">

- PIN: Defines the pin (D1) on the ESP8266 that the LED strip is connected to.
- NUMPIXELS: Defines the number of LEDs on the strip.

3.
<img width="468" alt="Screenshot 2024-10-17 at 15 54 14" src="https://github.com/user-attachments/assets/4e2803f9-73e5-4589-a0f0-5dde29145d59">

- pixels: Creates a NeoPixel object, which controls the LED strip using the GRB color order (Green-Red-Blue) at a frequency of 800kHz.

4.
<img width="318" alt="Screenshot 2024-10-17 at 15 55 34" src="https://github.com/user-attachments/assets/ec2e892f-54ed-47d0-b6d5-4f5b0a0db68d">

- ssid: Stores the name of your Wi-Fi network.
- password: Stores the password for your Wi-Fi network.

5.
<img width="440" alt="Screenshot 2024-10-17 at 15 56 50" src="https://github.com/user-attachments/assets/f401fa3b-d3b4-4455-8fc7-e9cb08f21548">

- apiKey: Your API key from OpenWeatherMap, which you need to request weather data.
- cityID: The unique ID for Amsterdam on OpenWeatherMap.

6.
<img width="875" alt="Screenshot 2024-10-17 at 15 57 34" src="https://github.com/user-attachments/assets/b782e4ca-d1f7-4bd8-bab6-d32598a4af2e">

- weatherUrl: Constructs the full URL to make a request to OpenWeatherMap for the weather data in Amsterdam, using your API key and retrieving temperatures in Celsius.

7.
<img width="168" alt="Screenshot 2024-10-17 at 16 01 02" src="https://github.com/user-attachments/assets/f52c8345-af69-4a9c-ade8-4f52f4cd3966">

- client: A client object used to connect to the OpenWeatherMap server over Wi-Fi.

8.
<img width="379" alt="Screenshot 2024-10-17 at 16 03 27" src="https://github.com/user-attachments/assets/8e50a926-0ea4-4b3e-bab5-9e162945c616">

- Serial.begin(115200): Starts serial communication at 115200 baud to monitor output in the Serial Monitor.
- pixels.begin(): Initializes the LED strip.
- connectToWiFi(): Connects the ESP8266 to your Wi-Fi network.
- updateWeatherData(): Retrieves the weather data and updates the LED strip.

9.
<img width="420" alt="Screenshot 2024-10-17 at 16 04 26" src="https://github.com/user-attachments/assets/7f844493-0630-4fee-ad1d-0baf60a2ed5a">

- delay(600000): Delays the execution for 10 minutes (600,000 milliseconds) before fetching the weather data again.
- updateWeatherData(): Retrieves new weather data every 10 minutes and updates the LEDs accordingly.

10.
<img width="313" alt="Screenshot 2024-10-17 at 16 11 58" src="https://github.com/user-attachments/assets/0ec8b0f1-5996-4a13-8521-898eb8afecef">

- WiFi.begin(ssid, password): Starts the connection process to your Wi-Fi network using the provided credentials.
- while (WiFi.status() != WL_CONNECTED): Keeps the code looping until the ESP8266 successfully connects to the Wi-Fi network.
- Serial.println(): Outputs messages to the Serial Monitor to show the connection status.

11.
<img width="523" alt="Screenshot 2024-10-17 at 16 12 30" src="https://github.com/user-attachments/assets/0a7c3934-f94a-4b45-b84c-c12683d5ee77">

- client.connect("api.openweathermap.org", 80): Attempts to establish a connection to the OpenWeatherMap API server over HTTP.
- client.print(): Sends an HTTP GET request to fetch weather data.
- client.readStringUntil('\n'): Reads the response line by line until it finds a JSON response.
- parseWeatherData(line): Parses the JSON data and extracts temperature information.

12.
<img width="506" alt="Screenshot 2024-10-17 at 16 14 05" src="https://github.com/user-attachments/assets/2f3a0637-5b2c-4354-9e03-7449d06be954">

- deserializeJson(): Decodes the JSON string into a structured format.
- doc["main"]["temp"]: Extracts the temperature from the JSON response.

13.
<img width="433" alt="Screenshot 2024-10-17 at 16 19 33" src="https://github.com/user-attachments/assets/12012f0b-db1e-4d1f-ac23-92f1acaa4922">

- This block adjusts the LED colors according to the temperature: Red (above 30°C), Green (25-30°C), Blue (20-25°C), Orange (15-20°C), Purple (10-15°C), and White (below 10°C).

14.
<img width="582" alt="Screenshot 2024-10-17 at 16 20 00" src="https://github.com/user-attachments/assets/c5298cd3-5d3c-4c2f-bab2-f455079fa571">

- setPixelColor(): Sets the color of each pixel using RGB values.
- pixels.show(): Updates the LED strip with the new colors.


## 6. Step 4: Testing

### Put the code in the Arduino:
click on the upload button to check if there are any errors. If there are any errors try the tabs underneath.

### Check LED Strip:
Ensure your LED strip is correctly connected to the specified pin (D1 in this case) and powered appropriately. If the LEDs do not light up, double-check your connections.

### Wi-Fi Connection Issues:
If you see "Connection to OpenWeatherMap failed," verify your Wi-Fi credentials. Make sure the SSID and password are correct.

### No Weather Data:
If the temperature does not change the LED colors, ensure the API key is valid and check the city ID.

## 7 step 5: errors

### ArduinoJson
you will have a lot of errors tyring out this code, because i did too the first error you might encouter is the ArduinoJson error:

<img width="1439" alt="Screenshot 2024-10-07 at 12 19 01" src="https://github.com/user-attachments/assets/db8ee0cd-120d-484e-a19b-b9a34fe50b6e">
this error is fixed with installing the ArduinoJson library, found on line '37'

### the 3v/5v issue 
on the arduino that i am using there is a clear 3 volt output. but for this code that is not enough volt. you need an 5v output. i struggeld a long time with this and didnt know what to do because it kept saying that i didnt have enough space. like this:
<img width="761" alt="Screenshot 2024-10-17 at 16 36 40" src="https://github.com/user-attachments/assets/f6863c3b-ec5c-42c8-95fb-470abbf32592">

this means that the 3v should be switched to 5v because the power is not enough. 
- When You Should Use 5V
LED strips (NeoPixels): Most require 5V power, so you should use the 5V pin.
Devices with higher power demands: Motors, high-power sensors, and other components that consume more current.
General Arduino operation: Many Arduino-compatible components are designed to run at 5V.

- where is the 5v on the arduino? i didnt now this at first because i only saw 3v, then i looked it up on the internet and found that 5v is called VIN on the arduino board.
![IMG_2469](https://github.com/user-attachments/assets/a05fede0-546b-4422-9c4c-31dea9f3c8f1)

## 8 Conclusion
In this manual, you've learned how to connect an LED strip to an Arduino (or ESP8266) and make it change colors based on the weather using data from the OpenWeatherMap API. Step by step, we went over how to set up the hardware, install the right libraries, get an API key, and write code to get weather information. The LED strip lights up in different colors to show the current temperature.
This project was pretty hard for me because im technologically not the strongest 🥲 but i've managed to understand the code and explain it to you 😄.

## 9 my product
https://github.com/user-attachments/assets/75b87ac4-7ca3-4f10-99dc-e189c2c2297b




