# RFID Access Monitoring on ESP32

## **REQUIRED COMPONENTS:**

RFID READER
ESP32 2x
CABLES
RFID CARD/CHIP,CREDIT CARD or phone with NFC
 

## **Explanation of the project**

 This Project was Developed to Monitor School Attendance but can be also used in other Institutions/Workplaces.
### What is RFID?

RFID is Hexadecimal Sequence that identifies your Device, **its commonly used in things like credit cards,NFC chips** it can be Used to identify your device, you can find your RFID using Various Phone apps.

## **Explanation of the Code**

### Global space
 
in the global space we include libraries **SPI.h and MFRC522.h** which are libraries for Serial peripheral interface and RFID reader,
then we define where we connected SDA and RST(Reset) Pins, *for our cause its pin 5 and 0*, in the next step we create rfid instance through the library.

### Void Setup

In void setup we initialize Serial line Communication with speed of **115200 baud**,
the we initiate Communication through SPI and We Initiate Communication with the reader

### Void Loop

In the void loop we create if that will check if there are any RFID tags nearby and return the value, if there arent any it will begin the loop again, otherwise it will try to read the tag and check if it was read correctly,if it was succesfull we wll see the Tag type written in serial monitor.

in the next IF we check if the Tag is the type we support, **this is very good thing because we can filter out unwanted tags that could be used to bypass the reader**
if it isnt the supported one it will print a line in serial monitor.

### Getting RFID 

In this part of code (*vypisHex*) we will Read the Tag Id´s and Write them in serial monitor so we can then manually assign them to Exact person

### Assigning RFIDs 

if we want to assign RFIDs to people we have to create a IF, the IF will check who is the Assigned owner(*If there is any*) and Print a line in serial Monitor,
To make sure this IF works we have to make it check the IDs, 
we will achieve this by putting #FF0000 rfid.uid.uidByte #011BC4 [0] == #011BC4 0x52 as condition, 

**Where the red part of the text is the RFID we saved from reading, the Blue one is the Pair We are checking (0 = first pair) and the green one is the Combination we want in that pair, and we need to have for of these to check the entire RFID of the tag.**

### Detection of Unknown tag

If the IF decides the tag is unknown it will Tell us in Serial Monitor and end the communication

## **TroubleShooting**

** RFID Reader Might read some cards but wont show their real RFID this can be fixed by adding the card type to the list of Supported types of tags**


# RFID Database Data Subscriber (Second Code File)

## **Explantion of Function**

THis file is used to obtain data from Your Firebase Database (if you have set one up) and Present them to you via Serial Monitor

## **Code Explanation**

### Global Space 

For this Part of Code we will have to Include 3 Libraries which are **Arduino.h,Wifi.h,Firebase_ESP_Client.h, and addons TokenHelper.h and RTDBHelper.h**
Then we will Define Wifi SSID(Name) and Password for the wifi, Then we define Firebase Database API key and Database Url.
Then we create firebase data object, and  global Variables (Unsigned long,int,String,float and Bool).

### Void setup

In setup we will begin Communication and wifi connection, 
**THere will be dots on serial monitor until the wifi connects** after that there will be line in serial Monitor *Connected with IP:*

**In the next step we will assign Databse ap and config key, Via Config.api_key and Config.database_url**

Then we will IF that will attempt a signup to databse if it fails it will print a Error message. otherwise we are logged into the database.

Config.token_status_callback is a callback function for long running token generation.
**Firebase.reconnectWifi(true); is function to keep the connection between database and end node Working**

### Void loop
In this Function we create IF that will check if the database is working,if the end-node managed to signup and Time when it last obtained data.
then we create another string where we assign the Part of database we want to search for the data
If they are found they will be printed on Serial Monitor, **Otherwise there will be error message**











