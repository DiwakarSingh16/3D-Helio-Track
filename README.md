# HelioTrack · 3D Solar Tracker Lab

An interactive digital twin for a single-axis solar tracker. Inspect the assembly in real time, watch a simulated sun move across the sky, and read sensor data through speedometer-style gauges and telemetry charts.

![HelioTrack dashboard with the 3D tracker, live-style sensor gauges, and telemetry charts](docs/screenshots/heliotrack-dashboard.png)

## 3D model preview

The model follows the daylight cycle as the sun moves. Drag to orbit the camera, adjust the panel tilt, or let auto tracking follow the sun vector.

![Animated 3D solar tracker following the sun through a daylight cycle](docs/screenshots/heliotrack-sun-tracking.gif)

## Features

- Interactive Three.js model of a single-axis solar panel tracker, with named assembly components.
- Daylight cycle with a moving sun and changing illumination; manual tilt and automatic tracking controls.
- Eight speedometer gauges for LDR 1, LDR 2, servo angle, panel temperature, gyroscope X/Y/Z, and acceleration magnitude.
- Telemetry history with field trends, LDR comparison, and gyroscope charts.
- Demo readings available on launch, so the dashboard and charts are ready to explore without hardware.
- Live ESP32 USB serial input with a browser COM port picker, plus ThingSpeak, ESP32 Wi-Fi JSON, and Bluetooth LE sources.
- Sensor history saved locally in the browser by channel or source.

## Run locally

No build step is required. On Windows, double-click `run.bat` in this folder. It starts the server from the correct project directory on port **4174** and opens the dashboard. Keep the terminal window open while using the app.

Alternatively, open a terminal in the **3D-Helio-Track** project folder (the folder containing `index.html`) and run:

```bash
python -m http.server 4174
```

Then open [http://localhost:4174](http://localhost:4174) in a modern browser. Three.js and the display fonts load from CDNs, so an internet connection is needed for the 3D scene and fonts.

## Connect your tracker

Choose **Connect data source** and select a source:

- **ESP32 USB serial:** Choose **ESP32 USB serial · COM port**, leave the baud rate at **115200** to match the sketch, click **Save & Connect**, then select the ESP32 port (for example, COM7) in Chrome or Edge. The dashboard reads the sketch's labeled serial output and updates the gauges and local history as each sensor block arrives. Close Arduino Serial Monitor before connecting because it holds the COM port.
- **ThingSpeak:** Enter your channel ID and, for a private channel, its read-only API key. Configure the ThingSpeak field names to match the eight readings listed above. The browser fetches the latest feed and channel history.
- **ESP32 Wi-Fi:** Enter an HTTP endpoint that returns JSON fields such as `field1` through `field8`, or the supported sensor names. The endpoint must allow CORS. A secure hosted page may be blocked from reading a local, non-HTTPS endpoint by the browser.
- **Bluetooth LE:** Enter the ESP32 service and characteristic UUIDs, then pair from Chrome or Edge on a supported device. The characteristic should provide JSON telemetry.
- **Simulator:** Use generated sample readings to explore the gauges, model tracking, and charts without connecting hardware.

ThingSpeak read keys are stored in this browser's local storage. Use a read-only key; never enter a write key. The app is a browser dashboard and does not upload your data to a separate HelioTrack server.

## Controls

- Drag in the 3D viewport to orbit; use **Reset view** to restore the camera.
- Toggle component labels with **Labels**.
- Move the **Daylight cycle** slider or play/pause the sun's movement.
- Adjust **Array tilt** directly or keep **Auto tracking** enabled.
- Choose a sensor and time range in **Telemetry analytics** to inspect stored history.

## Project files

```text
run.bat      Windows launcher for port 4174
index.html   Dashboard layout and connection dialog
styles.css   Responsive visual design
app.js       Three.js scene, sensor connections, gauges, and charts
docs/
  screenshots/
    heliotrack-dashboard.png
    heliotrack-sun-tracking.gif
```

## Technology

- HTML, CSS, and JavaScript modules
- [Three.js](https://threejs.org/) for the interactive WebGL model
- ThingSpeak REST API, browser Fetch, and Web Bluetooth API
- Canvas 2D for telemetry history charts

## License

No license file is included yet. Contact the repository owner before redistributing or reusing this project.

