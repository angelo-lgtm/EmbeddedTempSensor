# Testing Instructions

Follow these steps carefully to test the entire embedded system flow from end-to-end.

## Phase 1: Hardware & Local Testing

1. **Wire the Hardware:**
   - Connect the DHT11 and the LCD display to your Arduino Uno as described in `connections.md`.

2. **Upload Arduino Code:**
   - Open `arduino_temp_lcd/arduino_temp_lcd.ino` in the Arduino IDE.
   - Go to **Tools -> Board** and select `Arduino Uno`.
   - Go to **Tools -> Port** and select your COM port.
   - Click the **Upload** button.
   - **Verification**: You should see your name scrolling on the top row of the LCD, and the temperature displaying on the second row.

3. **Verify Local Serial Data:**
   - In the Arduino IDE, open the **Serial Monitor** (magnifying glass icon in top right).
   - Set the baud rate in the bottom right corner to **9600**.
   - **Verification**: You should see data printing out like `TEMP:24.50` every two seconds. Close the Serial Monitor when done (important so the Python script can use the port!).

## Phase 2: PC to Cloud MQTT Testing

1. **Install Python Libraries:**
   - Open your PC terminal (Command Prompt or PowerShell).
   - Run: `pip install pyserial paho-mqtt`

2. **Run the PC Client Script:**
   - Make sure your Arduino is plugged in via USB and the Arduino IDE Serial Monitor is **closed**.
   - Run the script:
     ```bash
     python pc_client.py
     ```
   - **Verification**: The terminal should say `Successfully connected to Arduino` and `Connected to MQTT Broker`. You will see it printing live temperature updates like `[14:32:15] Received Temperature: 24.50 °C`.

## Phase 3: Dashboard Verification

1. **Open the Web Dashboard:**
   - Simply double-click the `dashboard.html` file to open it in your browser (Chrome, Edge, Firefox, etc.).
   - Ensure you have an active internet connection.

2. **Verify Real-time Updates:**
   - The dashboard should initially say `Connecting...` and then `Connected`.
   - The live dot will pulse gold.
   - Watch the temperature value on the dashboard update in real-time to match the values shown in your PC terminal!

## Troubleshooting Upload Errors

If you see the error **"Programmer is not responding"** or **"Failed uploading"** in the Arduino IDE:

1. **The "Manual Reset" Trick (Very Important):**
   - Click the **Upload** button in the IDE.
   - Watch the status bar at the bottom. The moment it changes from "Compiling Sketch..." to **"Uploading..."**, immediately press and release the **RESET button** on your Arduino Uno.
   - This manually triggers the bootloader and often solves connection timing issues.

2. **Check the COM Port:**
   - Unplug the Arduino and plug it back in.
   - In the IDE, go to **Tools -> Port** and ensure the port is still selected (sometimes it changes from COM18 to another number).
   - If no port appears, your USB cable might be faulty or "charge-only". Try a different cable.

3. **Check Wiring on Pins 0 and 1:**
   - Ensure **nothing** is connected to Digital Pin 0 (RX) and Digital Pin 1 (TX) while uploading. These pins are used for the upload itself.

4. **Install CH340 Drivers:**
   - If your Arduino is a clone (it doesn't say "Made in Italy" on the back), you may need the **CH340 driver**. Search for "CH340G driver Windows" online and install it.

---

## Final Exam Deliverables checklist:
- [ ] Take a photo of the Arduino and LCD working.
- [ ] Take a screenshot of the `python pc_client.py` terminal running successfully.
- [ ] Take a screenshot of the beautiful black and gold `dashboard.html` showing data.
- [ ] Push the folder to GitHub and submit!
