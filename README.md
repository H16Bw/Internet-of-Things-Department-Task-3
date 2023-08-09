# Internet-of-Things-Department-Task-3
3rd task of Internet of Things Department - Summer training program at Smart Methods

## Environmental Data Collection and Transmission with DHT22 Sensor and ESP8266/ESP32

## Wokwi Link : https://wokwi.com/projects/372550980634094593

![image](https://github.com/H16Bw/Internet-of-Things-Department-Task-3/assets/139852537/6a10f492-1ca7-4d9a-8799-f5b8af0c3b6e)


This code is an Arduino sketch designed for an ESP8266 or ESP32 microcontroller board to collect temperature and humidity data using a DHT22 sensor and send this data to a remote server using HTTP POST requests. This data can then be processed or displayed on the server side.

## Code step by step:

### 1. **Libraries and Definitions:**
   The necessary libraries are included at the beginning of the code. These libraries provide the functions required for Wi-Fi communication (**WiFi.h**), HTTP requests (**HTTPClient.h**), and interfacing with the DHT22 sensor (**`DHT.h`**).
   
   - **`DHTPIN`** and **`DHTTYPE`** define the pin connected to the DHT22 sensor and the sensor type, respectively.
   - An instance of the **DHT** class named **`DHT22`** is created, specifying the pin and sensor type.

### 2. **Wi-Fi Credentials and Server URL:**
   - You need to replace **"`your_wifi_ssid`"** and **"`your_wifi_password`"** with your actual Wi-Fi network credentials.
   - **URL** should be replaced with the actual URL where you want to send the data. This URL should point to a PHP script that will handle the incoming data.

### 3. **Setup Function:**
   - The **`setup()`** function initializes the serial communication for debugging and starts the Wi-Fi connection by calling **`WiFi.begin(ssid, password)`**.
   - The code waits until the Wi-Fi connection is established using a **`while`** loop and displays dots (**`.`**) to indicate the connection process.
   - Once connected, the DHT22 sensor is initialized using **`dht22.begin()`**.

### 4. **Loop Function:**
   - The **`loop()`** function is where the main functionality occurs. It runs repeatedly after the setup.
   - Temperature and humidity readings are taken using **`dht22.readTemperature()`** and **`dht22.readHumidity()`**.
   - The code checks if the readings are valid (not NaN, indicating failure to read from the sensor).
   - If the readings are valid, the code constructs a **`postData`** string with the temperature and humidity values.
   - An instance of **`HTTPClient`** named **`http`** is created, and it is set up to make an HTTP POST request to the specified URL.
   - The temperature and humidity data are sent in the POST request as part of the **`postData`**.
   - The HTTP response code is stored in **`httpCode`**.
   - If the HTTP response is successful (**`HTTP_CODE_OK`**), the payload (response content) is extracted using **`http.getString()`**.
   - If there's an error, it's printed to the serial monitor.
   - The HTTP connection is closed using **`http.end()`**.
   - The current status of the code execution is displayed on the serial monitor.
   - A delay of 5000 milliseconds (5 seconds) is added before the loop restarts to avoid sending data too frequently.

Overall, this code allows the ESP8266 or ESP32 board to collect temperature and humidity data, connect to Wi-Fi, and send the data to a remote server using HTTP POST requests. It's designed for applications where environmental data needs to be monitored and transmitted for further processing or analysis.
