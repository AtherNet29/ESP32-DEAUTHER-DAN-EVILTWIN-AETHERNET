<div align="center">
  <img src="https://img.shields.io/badge/Version-1.2_TRIAL-00ff00?style=for-the-badge&logo=esp32" />
  <img src="https://img.shields.io/badge/Chip-ESP32_(ESP32Dev)-blue?style=for-the-badge&logo=espressif" />
  <img src="https://img.shields.io/badge/Status-ACTIVE-success?style=for-the-badge" />
  <br><br>
  <img src="https://img.shields.io/badge/🛡️_Educational_Purpose_Only-IMPORTANT-red" />
</div>

<h1 align="center">⚡ AETHERNET TRIAL (ESP32 / JAMBLUE V 1.2)</h1>
<p align="center">
  <b>Advanced WiFi (2.4GHz) & Bluetooth Security Audit Tool</b><br>
  <i>Dual-module design integrating WiFi deauthentication, Evil Twin, Rogue AP, Beacon Spam, and dual NRF24L01+ Bluetooth jamming.</i>
</p>

<hr>

<h2>🎯 Feature Details</h2>

<h3>📡 WiFi Attacks (2.4GHz Support)</h3>
<ul>
  <li><b>Smart Deauth Attack:</b> Selectively disconnects targeted networks using native ESP32 raw 802.11 frames. Forces clients to automatically connect to our fake network for credential harvesting.</li>
  <li><b>Evil Twin & Captive Portal:</b> Clones target SSID with full BSSID spoofing. Forces clients to a fake login page with automatic password verification against the original network. Supports custom HTML templates uploaded via web UI.</li>
  <li><b>Rogue AP:</b> Creates a standalone fake Access Point with built-in Google login page to capture credentials directly. Fully captive-portal capable with DNS hijacking.</li>
  <li><b>Beacon Spam:</b> Floods the area with up to 50 customizable fake SSIDs to test client scanning mechanisms. Uses channel hopping (1, 6, 11) for maximum coverage.</li>
  <li><b>Monitor Mode:</b> Passive sniffer that hops across all 13 channels, detects deauthentication attacks in real-time, and reports attack status on OLED.</li>
</ul>

<h3>📻 Bluetooth / 2.4GHz Jamming</h3>
<ul>
  <li><b>JamBlue (Dual NRF24L01+):</b> Uses 2x NRF24L01+ modules running in parallel — one on HSPI, one on VSPI — to perform Continuous Wave Sweeping across the full 2.4GHz spectrum (channels 0–41 and 42–83). Highly effective at disrupting Bluetooth audio, IoT devices, and wireless peripherals. <b>Note: Activating this locks the ESP32 in RF mode and disables WiFi. Requires menu deactivation or reboot to stop.</b></li>
</ul>

<h3>🖥️ Interface & Control</h3>
<ul>
  <li><b>Dark Cyber Dashboard:</b> Futuristic web interface at <code>192.168.1.1</code>, fully mobile-responsive, equipped with 7 color themes (White / Cyber Blue / Matrix Green / Gold / Pink Neon / Purple / Orange), live clock sync, and real-time attack status.</li>
  <li><b>Custom OLED UI:</b> Cover-flow style menu navigation with animated 32x32 bitmap icons, custom 3x5 pixel font rendering, scrolling text, real-time attack stats, progress bars, brightness control, and idle clock display.</li>
  <li><b>Template Manager:</b> Upload, preview (live iframe), and set active HTML phishing templates for Evil Twin and Rogue AP directly from the web interface (stored in SPIFFS Flash).</li>
  <li><b>File Manager:</b> Full SPIFFS browser with upload, delete, rename, and assign functions. View free/total storage in real-time.</li>
  <li><b>Firmware OTA Update:</b> Upload new <code>.bin</code> firmware directly through the web interface.</li>
  <li><b>Activity Logging:</b> All credential captures and client MAC connections are logged to <code>/password_log.txt</code> with timestamps, viewable from the web Log tab.</li>
</ul>

<h3>🔐 Security Features</h3>
<ul>
  <li><b>Trial Limitation: Firmware is limited to 10 minutes of usage. After expiration, all features are permanently disabled, WiFi is turned off, and the OLED displays a "TRIAL EXPIRED" lock screen. The lock persists across reboots via EEPROM marker.</li>
  <li><b>Factory Reset Trigger:</b> Broadcasting SSID <code>SETELAN_AWAL</code> near the device within 30 seconds of boot will trigger a full configuration reset.</li>
</ul>

<hr>

<h2>🛠️ Hardware & Pinout Specifications</h2>
<p><b>⚠️ STRICT WARNING:</b> This firmware is hard-coded specifically for the <b>ESP32 Dev Module</b> pinout below. Ensure strict adherence to this wiring diagram.</p>

<h3>1. OLED Display (SSD1306 128x64 - I2C)</h3>
<table border="1" style="border-collapse: collapse; width: 100%; text-align: left; padding: 8px;">
  <tr style="background-color: #f2f2f2;">
    <th>OLED Pin</th>
    <th style="text-align: center;">ESP32 Pin</th>
    <th>Notes</th>
  </tr>
  <tr><td>SDA</td><td style="text-align: center;"><b>GPIO 4</b></td><td>I2C Data Line</td></tr>
  <tr><td>SCL</td><td style="text-align: center;"><b>GPIO 5</b></td><td>I2C Clock Line</td></tr>
  <tr><td>VCC</td><td style="text-align: center;"><b>3.3V</b></td><td>DO NOT use 5V</td></tr>
  <tr><td>GND</td><td style="text-align: center;"><b>GND</b></td><td>Common Ground</td></tr>
</table>
<p><i>* I2C Address must be set to <b>0x3C</b>.</i></p>

<h3>2. NRF24L01+ #1 - BT Jammer (HSPI)</h3>
<table border="1" style="border-collapse: collapse; width: 100%; text-align: left; padding: 8px;">
  <tr style="background-color: #f2f2f2;">
    <th>NRF24L01 Pin</th>
    <th style="text-align: center;">ESP32 Pin</th>
    <th>Notes</th>
  </tr>
  <tr><td>CE</td><td style="text-align: center;"><b>GPIO 16</b></td><td>Chip Enable</td></tr>
  <tr><td>CSN</td><td style="text-align: center;"><b>GPIO 15</b></td><td>Chip Select</td></tr>
  <tr><td>SCK</td><td style="text-align: center;"><b>GPIO 14</b></td><td>HSPI CLK</td></tr>
  <tr><td>MOSI</td><td style="text-align: center;"><b>GPIO 13</b></td><td>HSPI MOSI</td></tr>
  <tr><td>MISO</td><td style="text-align: center;"><b>GPIO 12</b></td><td>HSPI MISO</td></tr>
  <tr><td>VCC</td><td style="text-align: center;"><b>3.3V</b></td><td>DO NOT use 5V</td></tr>
  <tr><td>GND</td><td style="text-align: center;"><b>GND</b></td><td>Common Ground</td></tr>
</table>

<h3>3. NRF24L01+ #2 - BT Jammer (VSPI)</h3>
<table border="1" style="border-collapse: collapse; width: 100%; text-align: left; padding: 8px;">
  <tr style="background-color: #f2f2f2;">
    <th>NRF24L01 Pin</th>
    <th style="text-align: center;">ESP32 Pin</th>
    <th>Notes</th>
  </tr>
  <tr><td>CE</td><td style="text-align: center;"><b>GPIO 22</b></td><td>Chip Enable</td></tr>
  <tr><td>CSN</td><td style="text-align: center;"><b>GPIO 21</b></td><td>Chip Select</td></tr>
  <tr><td>SCK</td><td style="text-align: center;"><b>GPIO 18</b></td><td>VSPI CLK</td></tr>
  <tr><td>MOSI</td><td style="text-align: center;"><b>GPIO 23</b></td><td>VSPI MOSI</td></tr>
  <tr><td>MISO</td><td style="text-align: center;"><b>GPIO 19</b></td><td>VSPI MISO</td></tr>
  <tr><td>VCC</td><td style="text-align: center;"><b>3.3V</b></td><td>DO NOT use 5V</td></tr>
  <tr><td>GND</td><td style="text-align: center;"><b>GND</b></td><td>Common Ground</td></tr>
</table>
<p><b>⚠️ IMPORTANT:</b> Solder a <b>10uF Capacitor</b> directly between the VCC and GND pins on EACH NRF24L01 module to prevent voltage drops and crashes during transmission.</p>

<h3>4. Navigation Buttons (Input Pullup)</h3>
<table border="1" style="border-collapse: collapse; width: 100%; text-align: left; padding: 8px;">
  <tr style="background-color: #f2f2f2;">
    <th>Button</th>
    <th style="text-align: center;">ESP32 Pin</th>
    <th>Function</th>
  </tr>
  <tr><td>UP</td><td style="text-align: center;"><b>GPIO 17</b></td><td>Navigate up / Increase brightness</td></tr>
  <tr><td>DOWN</td><td style="text-align: center;"><b>GPIO 33</b></td><td>Navigate down / Decrease brightness</td></tr>
  <tr><td>OK / SELECT</td><td style="text-align: center;"><b>GPIO 27</b></td><td>Confirm / Activate feature (hold 3s to deselect in scan list)</td></tr>
  <tr><td>BACK</td><td style="text-align: center;"><b>GPIO 32</b></td><td>Back / Deactivate feature / Exit menu</td></tr>
</table>

<h3>5. Built-in LED</h3>
<table border="1" style="border-collapse: collapse; width: 100%; text-align: left; padding: 8px;">
  <tr style="background-color: #f2f2f2;">
    <th>Component</th>
    <th style="text-align: center;">ESP32 Pin</th>
    <th>Function</th>
  </tr>
  <tr><td>LED_BUILTIN</td><td style="text-align: center;"><b>GPIO 2</b></td><td>Monitor attack indicator (blinks when deauth detected)</td></tr>
</table>

<hr>

<h2>📦 How to Flash the Firmware</h2>

<h3>1. Using PlatformIO (Recommended)</h3>
<ul>
  <li>Install <b>PlatformIO Core</b> or PlatformIO IDE for VSCode.</li>
  <li>Create a project targeting board: <i>Espressif ESP32 Dev Module</i>.</li>
  <li>Install required libraries:
    <ul>
      <li><code>Adafruit GFX Library</code></li>
      <li><code>Adafruit SSD1306</code></li>
      <li><code>RF24</code></li>
      <li><code>ezButton</code> (optional, for button handling)</li>
    </ul>
  </li>
  <li>Place <code>main.cpp</code>, <code>Main.h</code>, and <code>Button.cpp</code> in the <code>src/</code> folder.</li>
  <li>Run: <code>platformio run -t upload</code></li>
  <li><b>AETHERNET SSID will appear shortly.</b> Connect to it and navigate to <code>192.168.1.1</code>.</li>
</ul>

<h3>2. Using Arduino IDE</h3>
<ul>
  <li>Install the <b>ESP32 Arduino Core</b> in Arduino IDE (Boards Manager).</li>
  <li>Select Board: <i>ESP32 Dev Module</i>.</li>
  <li>Install the required libraries via Library Manager.</li>
  <li>Open <code>main.cpp</code> and upload via USB.</li>
  <li>The module will automatically reboot and broadcast <b>AETHERNET</b>.</li>
</ul>

<h3>❓ What if the SSID does not appear?</h3>
<ol>
  <li>ESP32 might be stuck in bootloader mode. Press the <b>EN/RST button</b> once after upload completes.</li>
  <li>Check wiring, specifically NRF24L01 VCC/GND shorts, which prevent booting.</li>
  <li>Verify OLED wiring — a shorted SDA/SCL line can halt I2C initialization at boot (<code>display.begin()</code> loops forever on failure).</li>
  <li>Verify your ESP32's MAC address matches the whitelist (<code>68:09:47:4E:85:7C</code>). If not, the device will enter LED blink lock mode. Edit <code>allowedMAC</code> in <code>main.cpp</code> to match your chip's MAC.</li>
  <li>Flash the SPIFFS data partition if templates or config fail to load.</li>
</ol>

<h2>🌐 Web Interface Tabs</h2>
<table border="1" style="border-collapse: collapse; width: 100%; text-align: left; padding: 8px;">
  <tr style="background-color: #f2f2f2;">
    <th>Tab</th>
    <th>Function</th>
  </tr>
  <tr><td><b>DASHBOARD</b></td><td>Attack controls + network target table</td></tr>
  <tr><td><b>GANTI TEMA</b></td><td>Switch between 7 color themes</td></tr>
  <tr><td><b>LOG</b></td><td>View captured credentials and MAC connections</td></tr>
  <tr><td><b>TAMPILAN HTML</b></td><td>Upload and assign phishing templates</td></tr>
  <tr><td><b>FILE MANAGER</b></td><td>Browse, upload, rename, delete SPIFFS files</td></tr>
  <tr><td><b>SETTINGS</b></td><td>Configure SSID, password, hidden mode, screen timeout</td></tr>
  <tr><td><b>UPDATE</b></td><td>OTA firmware upload (.bin)</td></tr>
  <tr><td><b>INFO</b></td><td>Legal disclaimer and about info</td></tr>
  <tr><td><b>REBOOT</b></td><td>Restart ESP32</td></tr>
</table>

<div align="center">
  <h2> Get the Full / Premium Version</h2>
  <p>The file available in this repository is a Trial Version, strictly limited to 10 Minutes of usage time for initial demonstration. Once the trial expires, the device is permanently locked and displays a "TRIAL EXPIRED" message on both Web and OLED.</p>
  <br>
  <a href="https://t.me/+6283141852690">
  <img src="https://img.shields.io/badge/Contact-Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" />
  </a>
  <br><br>
  <i>Click the button above to chat directly with the developer on Telegram.</i>
</div>

<hr>

<h2>📸 Preview & Documentation</h2>
<p><b>Dashboard Preview (ESP32):</b></p>
<p align="center">
  <img src="https://via.placeholder.com/800x400/0d0e12/00f0ff?text=AETHERNET+PRO+Dashboard" width="800" alt="Dashboard Preview" />
</p>

<p><b>Module Wiring Diagram (ESP32):</b></p>
<p align="center">
  <img src="https://via.placeholder.com/800x500/0d0e12/00ff00?text=ESP32+Wiring+Diagram" width="800" alt="Wiring Diagram" />
</p>

<hr>

<div align="justify" style="background-color: #ffcccc; padding: 15px; border-left: 5px solid #ff0000;">
  <h3>⚖️ Legal Disclaimer</h3>
  <b>STRICT WARNING:</b> This tool is created purely for <i>Penetration Testing</i> and <i>Educational Purposes</i> within the scope of network security. It is strictly forbidden to use this tool to attack, steal data, or disrupt networks that are NOT your property. Any form of abuse that violates your country's laws is <b>NOT</b> the responsibility of the Developer. By using this firmware, you agree to these terms and conditions.
</div>

<div align="center">
  <br>
  <sub>Built with ❤️ by AETHERNET Developer Team — ESP32 Edition (JAMBLUE V2.2 PRO)</sub>
</div>
