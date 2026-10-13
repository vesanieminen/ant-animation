# Desert Ants — 3D

A real-time 3D animation of an ant caravan walking across desert dunes, built
with [Three.js](https://threejs.org/). No build step — a single HTML file plus
vendored Three.js modules.

## What's in the scene

- **Ant caravan** — 10 procedurally assembled ants (head, thorax, abdomen,
  eyes, mandibles, six jointed legs, swaying antennae) walking single-file
  along a winding circular route over the dunes, using a tripod gait
  (alternating leg phase groups, hip swing + knee bend + body bob).
  One ant is a leaf-cutter carrying a green leaf.
- **Desert** — layered sine-noise dune terrain with fine ripples,
  vertex-colored crest shading, procedural sand-grain texture, scattered
  rocks and saguaro cacti kept clear of the trail.
- **Atmosphere** — physically-based sky with a low warm sun, drifting
  wind-blown sand particles, warm distance fog, ACES tone mapping.
- **Camera** — slowly orbits and tracks the caravan; drag to orbit, scroll
  to zoom. The sun's shadow camera follows the lead ant for crisp close-up
  shadows.
- **HUD** — WebGL/GPU readout, brightness slider, and a self-diagnosing
  error overlay (explains WebGL or `file://` loading failures instead of
  showing a black screen).

## Run

```bash
python3 -m http.server 8321
# then open http://localhost:8321
```

Or one line (server + browser):

```bash
(pgrep -f "http.server 8321" >/dev/null || python3 -m http.server 8321 &) && sleep 1 && chromium http://localhost:8321
```

The page must be served over `http://` — browsers block ES modules over
`file://`.

### VMs / no-GPU machines

On virtual machines (virtio GPU) Chromium blocks software WebGL by default
and the page reports `Error creating WebGL context`. Launch with:

```bash
chromium --enable-unsafe-swiftshader --ignore-gpu-blocklist http://localhost:8321
```

or enable `#enable-unsafe-swiftshader` and `#ignore-gpu-blocklist` in
`chrome://flags` once.

## Layout

```
index.html      the whole scene (terrain, ants, props, camera, HUD)
vendor/         Three.js r160 + OrbitControls + Sky, vendored so no CDN is needed
```

## Stop the server

```bash
pkill -f "http.server 8321"
```
