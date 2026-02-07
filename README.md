# simple-counter

A beginner-friendly, mobile-first counter page built with **one single HTML file** (plain HTML + CSS + JavaScript).  
It works great on **iPhone** and **iPad**, supports **3 counters**, and stores values locally using **localStorage**.

**Live demo:** https://wagonbuy.github.io/simple-counter/counter.html

---

## What this project is

This repo contains a single-file web app that:

- Shows **3 counters** (A / B / C)
- Lets you **increment** a counter with `+1`
- Lets you **set** a counter to an exact integer
- Lets you **reset** a counter (with confirmation)
- Lets you **reset all** counters (with confirmation)
- Can **export/import** values as JSON (useful for moving between devices)
- Is optimized for iOS Safari (prevents annoying zoom when tapping quickly)

No frameworks. No build tools. No server.

---

## Quick start

### Option A: Run locally (no internet needed)

1. Download `counter.html`
2. Open it in a browser (Safari/Chrome)

### Option B: Host it on GitHub Pages (recommended)

This repo already uses GitHub Pages, so you can access it at:

- https://wagonbuy.github.io/simple-counter/counter.html

---

## Add to iPhone / iPad Home Screen (PWA-style)

On iOS Safari:

1. Open the page
2. Tap **Share**
3. Tap **Add to Home Screen**
4. Launch it from the Home Screen

This makes it feel like a simple “app” (still just a web page).

---

## How data is stored (very important)

### Values (persisted)
Counter values are saved to your device using:

- `localStorage`

That means:

- Values stay after refresh
- Values are device/browser-specific
- iPhone and iPad **do not sync automatically**
- Clearing Safari data removes the stored values

### Names (temporary)
Counter names are editable, but **NOT persisted**.  
They reset to defaults after refresh because the code stores names only in memory:

- `tempNames`

---

## File overview (counter.html)

This project intentionally keeps everything in one file:

- HTML: structure
- CSS: styling + responsive layout
- JavaScript: logic + storage + rendering

---

## UI behavior summary

Inside each counter card:

- **+1**: increment the counter by 1
- **Set**: prompt for an integer, then set the counter
- **Reset**: confirm, then reset to 0

Global actions:

- **Reset All**: confirm, then reset all counters
- **Export**: copies JSON to clipboard (values only)
- **Import**: paste JSON to restore values

---

## Mobile / iPad layout

### iPhone
- Single column layout (safe and readable)

### iPad (portrait-friendly)
- When screen width is **>= 700px**, the grid becomes **3 columns**

This is done with a CSS media query:

```css
@media (min-width: 700px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}


⸻

iOS Safari “double tap zoom” fix

Rapid tapping on iOS can trigger an automatic zoom.

This project reduces that with two layers:

1) Viewport settings

<meta
  name="viewport"
  content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no"
/>

	•	Prevents double-tap zoom
	•	Also disables pinch-zoom (intentional for this app)

2) touch-action optimizations

html, body { touch-action: manipulation; }
button { touch-action: manipulation; }

This tells the browser these are tap actions, not zoom gestures.

⸻

Code walkthrough (beginner-friendly)

1) Constants / configuration

These define the basic app “settings”:
	•	STORAGE_KEY: where values are stored in localStorage
	•	IDS: internal IDs for each counter
	•	DEFAULT_NAMES: visible default names
	•	DEFAULT_VALUES: initial values

Example:

const STORAGE_KEY = "simple_counter_values_v1";
const IDS = ["A", "B", "C"];


⸻

2) Loading and saving values

Load values

function loadValues() {
  const raw = localStorage.getItem(STORAGE_KEY);
  if (!raw) return { ...DEFAULT_VALUES };
  return { ...DEFAULT_VALUES, ...JSON.parse(raw) };
}

	•	If storage is empty: returns defaults
	•	If storage exists: merges saved values into defaults
	•	If JSON is broken: safely falls back to defaults

Save values

function saveValues(values) {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(values));
}


⸻

3) Rendering the UI

This app does not hardcode cards in HTML.

Instead, it generates all UI in JavaScript inside:

function render() { ... }

Steps:
	1.	Clear the container (grid.innerHTML = "")
	2.	Loop through counter IDs (IDS.forEach(...))
	3.	Create DOM elements (div, input, button)
	4.	Attach click handlers
	5.	Append everything into the page

Why do it this way?
	•	Simple to keep UI always consistent with data
	•	No manual HTML duplication
	•	Great for learning DOM basics

⸻

4) Button logic

+1 button

values[id] = (toInt(values[id]) ?? 0) + 1;
saveValues(values);
render();

Pattern you’ll see everywhere:
	1.	Update values
	2.	saveValues(...)
	3.	render() again

This keeps UI and storage always in sync.

Set button

Uses prompt() to ask the user for an integer.
	•	Rejects invalid input
	•	Only accepts integers

Reset button

Uses confirm() to avoid accidental resets:

if (!confirm(`Reset "${tempNames[id]}" to 0?`)) return;
values[id] = 0;
saveValues(values);
render();


⸻

Export / Import (JSON)

Export
	•	Converts values to JSON
	•	Copies to clipboard (or shows prompt if clipboard is blocked)

Example export output:

{"A":12,"B":0,"C":99}

Import
	•	Pastes JSON
	•	Parses it
	•	Merges into defaults
	•	Saves and renders

Useful for:
	•	moving values from iPhone → iPad
	•	backup before clearing browser data

⸻

Common beginner questions

“Can other people modify my counters?”

No.

Your values are stored on your own device in your browser’s localStorage.
Other visitors get their own local storage.

“Can other people modify the code on my GitHub Pages?”

No, unless you give them write access to your repo.

They can fork it and host their own copy, but they cannot change your repo.

“Why don’t counter names persist?”

Because names are stored in tempNames (memory only).
This is intentional to keep the app simple and avoid storing personal labels.

If you want persistent names, you can store them in localStorage too.

⸻

Customization ideas (easy beginner exercises)
	1.	Make Counter A/B/C persistent
→ Save tempNames into localStorage
	2.	Add more counters
→ Add more IDs into IDS and update defaults
	3.	Add a “-1” button
→ Same pattern as +1 but subtract
	4.	Add a dark mode
→ Use @media (prefers-color-scheme: dark)
	5.	Rename counter.html to index.html
→ Then your URL can be shorter:
https://wagonbuy.github.io/simple-counter/

⸻

License

This project is licensed under the MIT License.
