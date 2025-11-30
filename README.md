# 🔒 MFRC522 RFID Access Control System (Arduino)

A basic Arduino sketch implementing an access control system using the MFRC522 RFID reader module. It reads the Unique Identifier (UID) of an RFID tag, compares it against an authorized list, and controls a relay to simulate a lock mechanism.

## 🛠️ Components and Connections

This sketch is designed to work with the following components connected to an Arduino board (e.g., Uno):

* **RFID Reader:** MFRC522 Module 
    * **SS/SDA Pin:** Connected to Digital Pin 10 
    * **RST Pin:** Connected to Digital Pin 9 
    * **SPI Bus:** The system uses the SPI communication protocol
* **Relay/Lock:** Connected to Digital Pin 3 (`int a=3;`)
* **Access Granted LED (Green/Success):** Connected to Digital Pin 6.
* **Access Denied LED (Red/Error):** Connected to Digital Pin 7.

## 📚 Prerequisites

1.  **Arduino IDE:** Installed on your machine.
2.  **Libraries:**
    * **SPI Library:** Standard library, usually included
    * **MFRC522 Library:** Required to communicate with the RFID module. You can install this via the Arduino Library Manager.

## 🚀 How to Use

1.  **Installation:** Ensure the necessary libraries (`SPI.h` and `MFRC522.h`) are installed in your Arduino IDE.
2.  **Hardware:** Connect the components as described above.
3.  **Authorization:** You must modify the authorized UID in the code before uploading.

    * Upload the sketch to your Arduino board.
    * Open the **Serial Monitor** at **9600 baud**.
    * Approximate your authorized card to the reader.
    * Note the UID displayed on the Serial Monitor (e.g., `UID tag : EE 93 6F 1D`).
    * In the `loop()` function, change the hardcoded UID to your card's UID:

        ```c++
        // Locate this line and update the UID in quotes
        if (content.substring(1) == "EE 93 6F 1D") //change here the UID... 
        ```

4.  **Upload:** Re-upload the modified sketch to the Arduino.

## ⚙️ Functionality

The main loop continuously checks for a new RFID card.

* **Card Detection:** If a card is present, the sketch reads the card's UID.
* **Authentication:** The read UID is converted to a string (`content`) and compared to the authorized string.
* **Authorized Access:**
    * The Serial Monitor displays `"Authorized access"`.
    * The relay is set to the **LOW** state (`digitalWrite(a,LOW);`), and the LED on pin 6 flashes multiple times.
* **Access Denied:**
    * The Serial Monitor displays `" Access denied"`.
    * The relay is kept in the default **HIGH** state (`digitalWrite(a,HIGH);`), and the LED on pin 7 flashes multiple times.

## 💡 Notes

* Pin `a` is initialized to `3` and is set to `HIGH` (locked/default state) during setup.
* [cite_start]The `content.substring(1)` is used because the read UID string starts with an unintentional space from the formatting loop.
