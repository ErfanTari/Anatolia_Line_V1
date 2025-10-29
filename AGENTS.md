Project: Anatolia Live Production MVP — Offline + React (no backend)
Goal: Three production lines shown as big boxes (“First line”, “Second line”, “Third line”). Each box displays static parameters:
body, thickness_mm, size, engobe, product_code, protection_glaze, kiln_temperature_C, kiln_cycle, surface.
Login (demo): Name Production, Password Prototype. No sensors, no network. Everything offline via localStorage.
Deliverables
Offline single-file HTML: index.html (inline CSS + JS only; no external files).
React + Vite project with the same behavior and schema (no UI libraries).
Line Labels & IDs
UI labels: “First line”, “Second line”, “Third line”.
Internal IDs: LA, LB, LC. Mapping: First→LA, Second→LB, Third→LC.
Buttons per Line
Edit → opens side panel to edit the 9 parameters; changes persist on reload.
Finished production → opens modal:
Inputs: Quantity (sqm) required (>0), Notes optional
Read-only Run code (preview)
Save writes a history record to localStorage, increments a per-day counter, shows “Saved ✓ {run_code}”.
Run Code Format
YYMMDD_L{1|2|3}_CXX
YYMMDD = local date (zero-padded)
L1/L2/L3 = line number for First/Second/Third
CXX = two-digit counter per (date,line) starting at 01: C01, C02, … (if >99, continue C100, C101 …).
Example: 251029_L2_C03.
Persistence (localStorage)
Namespace keys with anatolia.v1.*
anatolia.v1.lines: { LA:{…}, LB:{…}, LC:{…} } (current editable state)
anatolia.v1.history: Run[] array (see schema)
anatolia.v1.counters: map YYYY-MM-DD|LA → next counter int (start 1)
Include schema_version: 1 in records. Initialize if absent.
History Record Schema
{
  "schema_version": 1,
  "run_code": "YYMMDD_L{1|2|3}_CXX",
  "line_id": "LA|LB|LC",
  "line_label": "First line|Second line|Third line",
  "production_date": "YYYY-MM-DD",
  "saved_at": "ISO-8601",
  "quantity_sqm": 1234.5,
  "notes": "optional",
  "snapshot": {
    "body": "", "thickness_mm": 18, "size": "160x320",
    "engobe": "", "product_code": "", "protection_glaze": "",
    "kiln_temperature_C": 1220, "kiln_cycle": "", "surface": ""
  },
  "counter_of_day": 3
}
Top Bar (Global)
Search by date: numeric inputs Day, Month, Year + Search button → filter History to that exact YYYY-MM-DD.
History button: opens modal/table of runs with columns (Run code, Date, Line, Quantity, Product code, Surface), filters (date or date range, line, free-text over product_code/notes), row → details drawer.
Export JSON filename anatolia-history-YYYYMMDD.json.
Import JSON optional: merge, skip duplicates by run_code.
Login (demo gate)
Full-screen when not authed. Accept only Production / Prototype. Client-side only.
Constraints
Offline build: single index.html with inline CSS+JS, no external refs.
React build: React+Vite only. No extra libraries.
No live animations (kiln temp is static like others).
Keep code readable and direct.
Acceptance Checklist
Login works.
Edit persists via localStorage.
Finished production saves a unique run_code, appears in History.
Search by date returns expected rows.
Export/Import JSON works; duplicates skipped.
Entire offline build runs by double-clicking index.html (no server).
Work Plan for the Agent
Propose a 2-step plan and wait for confirmation.
Implement offline single-file index.html first; stop.
Implement React + Vite project mirroring behavior; stop.
Provide a short README and manual test checklist.
No external libraries; do not add a backend.
