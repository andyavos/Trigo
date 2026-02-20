# Trigo

A simple app for finding nearby triangulation stations within a chosen radius on Google Maps, using your current location.

The data currently used for this from Lonewalker's database: https://lonewalker.net/trigtable.php - I've not tested the correctness of this database, and it should be treated as such (see the disclaimer on that page).

## Setup

1. **Google Maps API key**  
   Get an API key from [Google Cloud Console](https://console.cloud.google.com/) (enable “Maps JavaScript API”).  
   Open `index.html` and replace `YOUR_GOOGLE_MAPS_API_KEY` with your key:

   ```js
   const GOOGLE_MAPS_API_KEY = 'your-actual-key-here';
   ```

2. **Serve the folder over HTTP**  
   Browsers block loading local files (e.g. `trigdatabase.csv`) from `file://`. Run a local server from the project directory. Any of these will work:

   ```bash
   # Python 3
   python -m http.server 8080

   # Node (npx)
   npx serve -p 8080

   # PHP
   php -S localhost:8080

   # Ruby
   ruby -run -ehttpd . -p8080
   ```

   Or use the **Live Server** extension in VS Code/Cursor (right‑click `index.html` → Open with Live Server).

   Then open **http://localhost:8080** on your phone (same Wi‑Fi) or computer.

3. **Location permission**  
   When you tap **My location**, the browser will ask for location access. Allow it so the map can centre on you and show nearby trig points.

## Usage

- Choose **Within** (5, 10, 25, or 50 km).
- Tap **My location** to centre the map on you and show trig points in that radius.
- Tap a green marker to see name, type, condition, height, and distance.
- Blue circle is your position.

## Data

Uses `trigdatabase.csv` (columns: `lat`, `long`, `tp_num`, `tp_name`, `full_name`, `type`, `condition`, `height_m`). The CSV is loaded once; filtering by radius is done in the browser with the Haversine formula.
