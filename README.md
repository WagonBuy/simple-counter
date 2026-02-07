# simple-counter

A small, mobile-friendly counter web page implemented in a single HTML file.  
Designed to be easy to understand, easy to modify, and easy to deploy.

Live demo:  
https://wagonbuy.github.io/simple-counter/counter.html

---

## Overview

This repository contains a lightweight static web application built with plain HTML, CSS, and JavaScript.

The application does not rely on any external libraries, frameworks, or build tools.  
All functionality is contained in one file: `counter.html`.

---

## Functionality

The page provides three independent counters (A, B, and C).

For each counter, the following operations are available:

- Increment the value by 1  
- Set the value to a specific integer  
- Reset the value to 0 (with confirmation)

Global operations include:

- Reset all counters at once (with confirmation)  
- Export all counter values as JSON  
- Import counter values from JSON

---

## Data Storage

Counter values are stored locally in the browser using `localStorage`.

As a result:

- Values persist across page reloads  
- Data is stored per browser and per device  
- Values are not synchronized across devices  
- Clearing browser data will remove stored values  

Counter names are editable but not persisted and will reset on page reload.

---

## Mobile and Tablet Behavior

The layout is optimized for touch-based devices:

- Single-column layout on phones  
- Three-column layout on screens wider than 700px (for example, iPad in portrait mode)

Additional adjustments are made to improve usability on iOS Safari, including reducing unintended zooming during rapid button taps.

The page can be added to the iOS Home Screen and used as a standalone web app.

---

## Export and Import

Exported data is represented as a simple JSON object containing counter values only.

This allows manual transfer of data between browsers or devices.

---

## Project Structure

The repository structure is minimal:

- `counter.html` — the complete application  
- `README.md` — project documentation  
- `LICENSE` — MIT License text  

---

## License

This project is licensed under the MIT License.  
See the `LICENSE` file for details.
