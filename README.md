# AI-VR-AGENT

**Type a description. Get a blueprint, a 3D model, or both. Edit it by hand, view it in VR, export it to a file your other tools can use.**

DRAFT/VR is a single self-contained web app — no build step, no backend, no install. Open the HTML file in a browser and it works.

---

## What it does

- **Generate** — describe a part, mechanism, or object in plain English. Choose Blueprint, 3D Model, or Both, and it drafts a result using Claude.
- **Edit by hand** — flip on EDIT mode and click any element (blueprint) or shape (3D model) to open an inspector: position, size, radius/height, rotation, color, label. Add or delete elements freely.
- **View in VR** — a real WebXR session on a standalone headset (Quest, PICO, etc.), or **Cardboard mode** on any phone: full 3-axis head tracking via the phone's own gyroscope, no headset intelligence required, works with a basic ₹300–800 phone-holder viewer.
- **Export**:
  - Blueprint → **PNG** / **JPG**
  - 3D model → **STL**, **OBJ**, **3MF** (opens directly in Bambu Studio / OrcaSlicer), and **STEP** (true B-rep solid, planar-faceted primitives — opens in FreeCAD, SolidWorks, Fusion 360)
- **History** — past generations persist across sessions (per-browser, via the app's own storage).

## Try it

Open `index.html` directly in a browser for everything except motion sensors. VR / Cardboard mode specifically needs the page served over **HTTPS** (browsers block motion-sensor access on plain `http://` or a local file) — that's what this repo + GitHub Pages is for.

**Live:** `https://viren-robot.github.io/AI-VR-AGENT/`

## Tech

- Single HTML file — no framework, no build step, no dependencies to install.
- [Three.js](https://threejs.org/) (r128, via CDN) for 3D rendering and WebXR.
- [JSZip](https://stuk.github.io/jszip/) (via CDN) for 3MF packaging.
- **Payments** via PhonePe Checkout — ₹2,100 lifetime access, verified server-side via webhook signature.
- STEP export is a hand-written, self-tested B-rep exporter (box/cylinder/cone/sphere primitives as closed polyhedral solids — see `Export → STEP` in-app for details on what that means for accuracy).

## Known limitations

- STEP export is **faceted** (24-sided polygons standing in for true curved surfaces), not analytic B-rep. It's a valid, correctly-oriented solid that opens cleanly everywhere, but a perfect circle it is not.
- Cardboard mode gives rotational head tracking only (look around), not positional tracking (walk around) — same ceiling as any phone-in-a-headset setup.
- No native Android/iOS app — this is a browser page. It can be wrapped as one (Trusted Web Activity / Capacitor) as a separate step if you want it installable.

## License

MIT — see [LICENSE](LICENSE). Change this if you'd rather keep it private/unlicensed.
