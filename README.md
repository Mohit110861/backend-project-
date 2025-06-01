# Real-Time Location Sharing App

A simple real-time location sharing web application built with **Node.js**, **Express**, **Socket.IO**, and **Leaflet.js**. It allows multiple users to share their live geolocation on a shared map.

---

## Features

- Real-time user location updates using WebSockets (Socket.IO).
- Displays multiple user locations simultaneously on an interactive map.
- Removes markers when users disconnect.
- Uses OpenStreetMap with Leaflet.js for map rendering.
- Responsive frontend served by Express with EJS templating.

---

## Project Structure


---

## How It Works

### Server (`app.js`)

- **Express** sets up the web server and serves static files from `public/`.
- Uses **EJS** as the template engine to render the main page (`index.ejs`).
- Creates an HTTP server and attaches **Socket.IO** to enable real-time bidirectional communication.
- Listens for Socket.IO connections:
  - When a client sends their location (`send-location`), it broadcasts it to all connected clients (`receive-location`), including the sender's unique socket ID.
  - When a client disconnects, it notifies others to remove the corresponding marker (`user-disconnected`).

### Client (`public/js/script.js`)

- Checks if the browser supports geolocation.
- Uses `navigator.geolocation.watchPosition` to continuously track user location.
- Emits location data (`latitude`, `longitude`) to the server via Socket.IO.
- Initializes a Leaflet map centered initially at coordinates `[0,0]`.
- Listens for incoming location updates from the server:
  - Updates existing markers if the user already has one on the map.
  - Adds a new marker for new users.
- Removes markers when a user disconnects.

### Frontend (`views/index.ejs`)

- Loads the Leaflet CSS and JS from CDN.
- Loads Socket.IO client library.
- Loads custom CSS and client JS.
- Contains a div with id `map` which is the Leaflet map container.

---

## Installation and Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/real-time-location-app.git
   cd real-time-location-app
   git clone https://github.com/yourusername/real-time-location-app.git
cd real-time-location-app
npm install
node app.js
http://localhost:3000
