# CAN on ESP32 Example

This project demonstrates a very small CAN setup using the ESP32 TWAI
peripheral. Two applications are provided:

* **sender** – reads `0` or `1` from the serial monitor and sends a CAN
  message containing this value.
* **receiver** – listens for the message and toggles an LED accordingly.

The LED should be connected to GPIO25 through a current limiting resistor
(100–400 Ω). Connect the CAN transceivers to 3.3 V and GND and wire the
signals as defined in `menuconfig` (defaults are TX=GPIO32 and RX=GPIO33).

## Hardware setup

You will need two ESP32 boards and two CAN transceiver modules (for example
SN65HVD230). Connect each ESP32 to its transceiver and join the CANL/CANH
lines. The demo LED should be attached to GPIO25 through the resistor. If you
prefer other pins for TX, RX or the LED you can change them under
**CAN Example Configuration** in `menuconfig`.

## Building and flashing

1. Clone the repository:

   ```bash
   git clone https://github.com/Geibinger/CAN_ESP32_Example
   ```

2. Open the project with the provided VS Code devcontainer. When prompted,
   choose **Reopen in Container**. If no prompt appears, press `Ctrl+P` and run
   `> Dev Containers: Rebuild and Reopen in Container`. After the container is
   built, all ESP‑IDF tools are available.

3. Configure the build target using `menuconfig`.
   Under **CAN Example Configuration** select **sender** or **receiver**.
   Here you can also change the TX, RX and LED pins if required.

   ```bash
   idf.py menuconfig
   ```

4. Connect the ESP32 and build/flash the selected application:

   ```bash
   idf.py build flash
   ```

5. Repeat step 3 and 4 for the second ESP32 with the opposite target.

## Running the demo

Open a monitor for each board:

```bash
idf.py monitor -p <PORT>
```

Entering `0` or `1` in the sender's monitor transmits a CAN message. The
receiver prints the received value and switches the LED on (1) or off (0).
