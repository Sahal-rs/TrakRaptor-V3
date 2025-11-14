Project Goal
To develop a fully functional, real-time, full-stack web application for the command and control of the RoboRescue Rover, including dual-camera video feeds, precision arm movement, and variable speed control. The application must be visually appealing, highly responsive, and adhere to a strict dark theme aesthetic.

I. Technical Requirements & Design Mandate
1. Design & Aesthetics (Mandatory)
Theme: Fully Dark Theme (high contrast, low-light optimized, using deep grays, blacks, and electric/neon accent colors).

Typography: Use a "Classic" or Monospaced Font (e.g., Fira Code, Inconsolata, or similar) for a high-tech, terminal-like feel.

Responsiveness: The layout must be fully responsive, prioritizing mobile/tablet use (for portable control) while maintaining usability on a desktop.

Layout: A single-page dashboard divided into three main sections: Video Feed, Controls, and Telemetry/Status.

2. Communication Protocol
The application must use WebSockets (or similar low-latency protocol) for real-time, bi-directional communication between the Backend API and the Rover (via the ESP32-S3) for low-latency video streaming and immediate control response.

II. Frontend Application (The Dashboard)
The frontend must be built as a single-page control dashboard featuring the following interactive components:

A. Video & Display
Dual Camera View: Display two simultaneous, distinct video feeds:

Primary RGB Feed: Live stream from the ESP32-S3 Camera Module.

Secondary Thermal Feed: Live stream from the Thermal Imaging Sensor. This feed should display a customizable false-color overlay (e.g., heat map) for easy interpretation of temperature data.

Message Console: A small, scrolling console to display system messages (e.g., connection status, errors, commands sent).

B. Control Interface
Rover Connection:

Button: A prominent "Connect Rover" button.

Functionality: Initiates the Wi-Fi connection handshake with the ESP32-S3 module via the backend, establishing the WebSocket link. Changes to "Disconnect" when active.

Robotic Arm Control (Joystick):

A visually intuitive, on-screen 2D/3D Joystick interface.

Axis Control: Must allow control over three axes (X, Y, Z) of the robotic arm.

Drill Toggle: A dedicated, illuminated button to Toggle Drill Power (ON/OFF).

Speed Control (Throttle Lever):

A large, dedicated Vertical Slider (Throttle Lever) to control the rover's speed.

Range: 0% (Stop) to 100% (Full Speed). Must update the numerical percentage value in real-time.

C. Telemetry & Status
Status Indicators: A dedicated panel to display critical real-time data:

Connection Status: (Connected/Disconnected, Latency Ping).

Rover Battery Level (Visual Gauge and Percentage).

Wi-Fi Signal Strength (RSSI).

Arm Position (Current X, Y, Z coordinates).

III. Backend API & Hardware Interface
The backend serves as the crucial intermediary, handling authentication, data relay, and translation of user commands into hardware signals.

A. API Endpoints (REST & WebSocket)
Authentication/Connection:

POST /api/connect: Initiates connection to the ESP32-S3.

POST /api/disconnect: Closes the connection.

Control Commands (REST or WebSocket Command Channel):

POST /api/control/throttle: Receives speed value (0-100) and forwards motor commands to the ESP32.

POST /api/control/arm: Receives joystick input (X, Y, Z) and drill state, forwarding servo/actuator instructions.

Telemetry Feed (WebSocket Data Channel):

Receives constant status updates from the ESP32-S3 (battery, signal, etc.) and pushes them to the connected frontend clients.

B. Data Handling Logic
Video Processing: Efficiently receive and relay camera streams (e.g., MJPEG, H.264) to minimize latency.

Thermal Data Translation: The backend must receive raw thermal sensor data, perform necessary calibration/translation, and encode it for the frontend to render the false-color map.

IV. Suggested Technology Stack
Frontend: React, Vue, or Angular (using Tailwind CSS for rapid dark-theme development).

Backend: Node.js (with Express) or Python (with Flask/Django) for handling REST API, and a robust WebSocket library (e.g., socket.io).

Communication: WebSockets, MQTT (optional for telemetry).
