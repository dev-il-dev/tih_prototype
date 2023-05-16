# tih_prototype

We use a gas sensor circuit with ESP32 as the microcontroller. We connect the microcontroller to the hydrogen gas sensor ME4-H2 and water pressure sensor SEN0257 and take input through the GPIOs. Analog data is read through these pins and using the in-built WiFi module, the data values are transmitted as a payload to the backend database developed on Firebase. These values are reflected on the front-end user dashboard. 

Simultaneously, if the analog value coming from the gas sensor exceeds a certain threshold, that is user-specified, then the ESP32 initiates high signal to the output terminals that goes to a buzzer, a solenoid valve and the exhaust fan relay switch. The buzzer turns on and gives an alarming signal. The solenoid valve is fitted in the pipeline, and once the hydrogen sensor detects gas concentration above the threshold, the valve is closed and flow of gas is constricted. The exhaust fan is simultaneously turned on through the relay switch. Hence, in principle, from the comparison between the analog gas sensor value and the threshold value performed by the ESP32, it generates a high signal that goes parallel to all the three components. 

The algorithm can be written as:

Loop 
{
Input: 
analogGasSensorValue  	 from gas sensor ME4-H2
            analogPressureSensorValue 	from pressure sensor SEN0257
Send data through Wifi to backend database: 
 analogGasSensorValue  		
 analogPressureSensorValue 

If (analogGasSensorValue > Threshold)
Turn On:
	Buzzer
	Exhaust fan
	Solenoid valve
}

        

![image](https://github.com/dev-il-dev/tih_prototype/assets/90281515/78517c52-fb6e-456d-bad1-12548a780a21)






Fig. 11 - Block diagram of the proposed system model


If the gas sensor analog value is below the threshold value, then no action is taken at the microcontroller. It simply transfers the payload to the Firebase application, where the rest of the processing takes place. 


# Software

In today's interconnected world, the ability to transfer data in real-time has become increasingly essential. One powerful combination for achieving this is the ESP32 microcontroller and Firebase Realtime Database. ESP32 is a versatile microcontroller renowned for its Wi-Fi capabilities, while Firebase provides a scalable and real-time NoSQL database. 
The software infrastructure used by the project consists of two segments, The first one is that in the programming of the esp32 module, the other one is the web-app that is used to show the real time fluctuation of Hydrogen concentration to the user using a real time Firebase database.
The programming of the esp32 allows us to read the value of the hydrogen gas concentration around the gas sensor along with transmitting it to the Firebase Server using WiFi. 
The web based application is used to process and display the leak level in the system. It uses the sensor data from Firebase server and uses a threshold value to decide whether a leak is taking place or not. 

## Programming of ESP32 

Setting up the Arduino IDE and Libraries: This step ensures that you have the necessary tools to program the ESP32 microcontroller. It involves installing the Arduino IDE, configuring the IDE to work with the ESP32 board, and installing the required libraries for ESP32 and Firebase integration.
Steps:
Ensure that you have the latest version of the Arduino IDE installed on your system.
Open the Arduino IDE and navigate to "Preferences."
In the "Additional Board Manager URLs" field, paste the following URL:
https://dl.espressif.com/dl/package_esp32_index.json
Click "OK" to close the Preferences window.
Go to "Tools" -> "Board" -> "Board Manager."
Search for "esp32" and click on the "esp32 by Espressif Systems" result.
Click "Install" to install the ESP32 board package.

Connecting the ESP32 to Firebase Realtime Database: In this step, you establish the connection between the ESP32 and your Firebase Realtime Database. This involves connecting the ESP32 to your computer, selecting the appropriate board and port in the Arduino IDE, and installing the Firebase ESP32 library.

Connect your ESP32 to your computer via USB.
Open the Arduino IDE and select the appropriate board and port from the "Tools" menu.
Install the required libraries by going to "Sketch" -> "Include Library" -> "Manage Libraries."
Search for "Firebase ESP32" by "Mobizt."
Click "Install" to add the library to your Arduino IDE.
Go to the Firebase website (firebase.google.com) and create a new project.
In your Firebase project, click on "Add app" and choose the web option (</>).
Register your web app by providing a name for it.
Copy the provided Firebase SDK configuration code snippet.

Writing the ESP32 Code: This step focuses on writing the code that runs on the ESP32 to transfer data to the Firebase Realtime Database. The code initializes the necessary libraries, sets up the Wi-Fi connection using your Wi-Fi credentials, and establishes the connection to the Firebase Realtime Database using your Firebase project credentials. The code then fetches the sensor data and stores it in the firebase real time database (Appendix A1).


## Programming of Web-Interface

The system uses a web interface using HTML and CSS to display data from a hydrogen gas leak sensor. The data is received through an ESP32 microcontroller and stored in Firebase Realtime Database. It is displayed through a basic and clean UI developed on HTML and CSS. HTML (Hypertext Markup Language) and CSS (Cascading Style Sheets) are fundamental technologies used for creating and styling web pages. HTML provides the structure and content of a webpage, while CSS controls the visual presentation and layout. 

Creating the HTML-CSS Web Interface:

Create an HTML file and link a CSS file to it.
Design the structure of the web interface using HTML tags 
Use CSS to style the web interface elements. You can customize the layout, colors, fonts, and other visual aspects to suit your preferences.
Add a <script> tag in the HTML file to include JavaScript code.

Retrieving Data from Firebase and Updating the Web Interface- 
Write JavaScript code within the <script> tag to interact with the Firebase Realtime Database.
Initialize the Firebase JavaScript SDK using your Firebase project configuration code snippet.
Retrieve the sensor data from the Firebase Realtime Database using the appropriate Firebase API methods.
Manipulate the HTML elements dynamically using JavaScript to display the sensor data in the web interface.
Set up a listener to listen for real-time updates in the data and update the web interface accordingly.

Thus, the interface uses HTML, CSS, and JavaScript to display data from a hydrogen gas leak sensor. Leveraging the capabilities of ESP32 and Firebase Realtime Database, the system can now transmit sensor data in real-time and visualize it in a user-friendly manner. 





