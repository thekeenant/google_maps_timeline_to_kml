# Google Timeline to KML Converter (Single File Edition)

https://thekeenant.github.io/google_maps_timeline_to_kml/

## Project Overview

This repository contains a single `index.html` file. This file is a self-contained, client-side web application that converts Google Maps Timeline data (from a JSON export) into KML (Keyhole Markup Language) files. These KML files can then be used with various mapping applications like Google Earth, Google My Maps, or other GIS software to visualize your location history as paths.

The tool allows users to:

1.  Upload their Google Timeline JSON export (specifically looking for `semanticSegments`).
2.  Optionally filter the timeline data by a specific date range (start and end dates).
3.  Generate and automatically download a KML file representing the paths within the selected timeline data.

## The "Vibe Coded in One Shot" Story

This tool was essentially "vibe coded" – brought from concept to a working version in a single, focused development session. The core JavaScript logic for the JSON-to-KML conversion was provided, and the challenge was to rapidly build a user-friendly HTML interface around it.

The process looked something like this:

1.  **Core Logic Integration:** Start with the existing JavaScript function that handles the conversion.
2.  **Interface Sketch (Mental or Quick):** Envision the simplest possible user interaction: file upload, date pickers, a "convert" button, and a way to get the output file.
3.  **HTML Scaffolding:** Quickly lay out the basic HTML structure in `index.html` for these elements.
4.  **JavaScript Wiring:**
    - Write JavaScript to handle file input using `FileReader`.
    - Parse the uploaded JSON.
    - Read values from the date pickers and prepare them for the conversion function.
    - Adapt the conversion function for robust date handling (using JavaScript `Date` objects) and to gracefully handle potential inconsistencies in the input JSON.
    - Implement the KML file download mechanism using a `Blob` and an anchor tag.
    - Add basic status messages for user feedback (success, errors, processing).
5.  **Styling (Minimalist):** Add a touch of CSS directly in the `<style>` tags within `index.html` to make it presentable and usable without needing external files.
6.  **Rapid Test & Refine:** Perform quick local tests, identify immediate bugs or usability issues, and fix them on the fly. The focus was on achieving a functional result quickly.

"Vibe coding" in this context means relying on experience and intuition to build out the functionality in a fluid, continuous manner, driven by the overall feel and desired outcome rather than a rigid, pre-defined plan. It's about getting into a flow and letting the solution take shape organically. The constraint of a single `index.html` file further encouraged this focused, integrated approach.

## Primary Use Case: Geotagging Fuji X-T4 Photos (and other non-GPS cameras)

This tool was created with a specific practical application in mind: **adding GPS location data to photographs taken with cameras that lack built-in GPS functionality, such as the Fujifilm X-T4.**

Here's the workflow for this use case:

1.  **Enable Location History:** Ensure Google Location History is active on your smartphone while you are out taking photos.
2.  **Export Timeline Data:**
    - Go to Google Takeout ([takeout.google.com](https://takeout.google.com)).
    - Deselect all products, then select only "Location History."
    - Choose "JSON" as the format for the Location History export.
    - Download the Takeout archive. Locate your Location History JSON file(s) within the archive (e.g., under `Semantic Location History/YYYY/YYYY_MONTHNAME.json` or a more general `Records.json` or `Location History.json`). The key is that the JSON should contain an array named `semanticSegments`, where each segment representing movement has a `timelinePath` property.
3.  **Convert to KML:**
    - Open the `index.html` file from this repository in your web browser.
    - Upload the relevant JSON file.
    - Select the date(s) corresponding to your photoshoot to narrow down the KML to the relevant period.
    - Click "Convert to KML." A KML file will be downloaded.
4.  **Geotag Your Photos:**
    - Use specialized software to correlate the timestamps of your photos with the GPS track in the generated KML file. This software will write the corresponding latitude and longitude data into each photo's EXIF metadata.
    - Popular options include:
      - **Adobe Lightroom Classic:** The Map module can load GPS tracklogs (you might need to convert KML to GPX first using an online tool or GPSBabel, as GPX is often better supported for this).
      - **GeoSetter (Windows, free)**
      - **GPicSync (Open Source, cross-platform)**
      - Various other EXIF editors that support tracklog import.

By generating a KML file of your movements on a given day, you create a digital breadcrumb trail that photo-geotagging software can use to accurately place your photos on a map.

## Broader Applications

While designed for photo geotagging, this tool is useful for anyone wanting to extract and visualize their Google Timeline paths:

- **Trip Visualization:** Review past travels, hikes, or daily commutes in Google Earth or other KML-compatible software.
- **Custom Map Creation:** Import the KML into Google My Maps to build personalized, shareable maps of your journeys.
- **Data Backup/Archive:** Keep a local, visual record of your significant movements.
- **Route Sharing:** Easily share specific paths or segments of your location history with others in a standard KML format.
- **Personal Analytics/Journaling:** Complement journals or memory-keeping projects with geographic context.

## How to Use

1.  **Download/Access:** Get the `index.html` file.
2.  **Open in Browser:** Open `index.html` directly in any modern web browser (Chrome, Firefox, Safari, Edge, etc.). Since it's a single file with all CSS and JavaScript embedded, no internet connection or web server is needed after you have the file.
3.  **Upload JSON:** Click the "Choose File" / "Upload Google Timeline JSON File" button and select your Google Timeline JSON file.
4.  **Select Dates (Optional):** Use the date pickers to filter the data to a specific range. If no dates are selected, the tool will attempt to process all `semanticSegments` with `timelinePath` data found in the file.
5.  **Convert:** Click the "Convert to KML" button.
6.  **Download:** The KML file will be automatically generated and downloaded by your browser. Status messages will appear on the page to indicate progress or any issues.

## Technical Details

- **Client-Side Operation:** All processing (file reading, JSON parsing, KML generation) occurs locally in your web browser using JavaScript. Your Google Timeline data is **not** uploaded to any external server, ensuring privacy.
- **Input Format:** The tool specifically looks for a JSON structure containing an array named `semanticSegments`. Each object in this array that represents a path should have a `timelinePath` property, which itself is an array of points. Each point object should have a `point` property containing a string like `"latitude, longitude"` (degree symbols and N/S/E/W characters are handled).
- **Output Format:** Standard KML (Keyhole Markup Language) XML format, suitable for LineString geometries.
- **Dependencies:** None, beyond a modern web browser that supports HTML5 and basic JavaScript APIs (`FileReader`, `Date`, `Blob`, etc.).

---

Feel free to fork, modify, or suggest improvements!
_(As of May 2025, this tool was created and documented.)_
