# Drift — 3D Water / Island Study

A 3D interactive ocean diorama for GitHub Pages. No build step, single `index.html`.

### What’s inside

- **Marching Cubes island**: `THREE.MarchingCubes` at 48³ resolution (~30k polys max). Procedural metaballs form a lumpy island with peaks and a flat bottom that merges into the baseplate. Regeneratable with random seed.
- **Baseplate**: sand-box diorama base (140×6×140) with canvas-generated stud grid texture and instanced rim studs — like a Lego baseplate.
- **Open ocean**: 500×500 plane, 200×200 segments (40k verts), displaced in vertex shader with **4 Gerstner waves** (real wave physics: wavelength, steepness/Q, amplitude, direction, dispersion `c = sqrt(g/k)`). Wind, choppiness, and flow speed all exposed.
- **Water level**: moves the ocean plane up/down, revealing shoreline foam and submerging the baseplate.
- **Ripples & rain**: 8-slot ripple uniforms. Click water to add ripple, rain particles create ripples on impact. CPU Gerstner sampling for buoy bobbing.
- **Atmosphere**: time-of-day slider lerps sky, fog, water colors, sun intensity/position. FogExp2, ACES tonemapping, soft shadows.
- **Floating objects**: 14 buoys/debris that sample wave height on CPU and bob/tilt realistically.
- **Polish**: OrbitControls with damping, pause on tab hidden, FPS counter, keyboard shortcuts (R = rain, Space = regen island, C = clear), responsive panel, grain overlay.

### Controls

- Water level, Wave height, Wind/speed, Choppiness (Q), Flow speed, Island size, Time of day
- Buttons: Make it rain, Regen island, Clear ripples, Pause, Reset view
- Interaction: Drag to orbit, scroll to zoom, shift+drag to pan, click water for ripples

### Run locally

Open `index.html` directly (imports via unpkg importmap), or:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

### Deploy to GitHub Pages

Settings → **Pages → Deploy from a branch**, select `main` and root. No build needed. Three.js is loaded from CDN (`0.160.0`) via importmap.

### Tech

- Three.js + OrbitControls + MarchingCubes (examples/jsm)
- Custom ShaderMaterial for water (Gerstner + ripple + fresnel + foam + fog)
- Single file, dependency-free besides CDN

Interact, raise the sea, make it storm.
