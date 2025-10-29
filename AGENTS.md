#Spec.MD
A) Codex-Optimized Condensed Spec (paste this)
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