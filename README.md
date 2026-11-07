# AeroLab | Mini Wind Tunnel

A simplified aerodynamic model for a 2D airfoil. Change wind speed, angle of attack, air density and wing area and watch lift, drag and CL / CD respond, with streamlines flowing around the wing in real time.

Everything lives in a single file, `index.html`. No build step, no dependencies, no folders.

## Put it on GitHub Pages

1. Open your `Mini-Wind-Tunnel-Simulator` repository on GitHub.
2. Choose **Add file > Upload files** and drag in `index.html`. It replaces your current `index.html` because the name is the same.
3. Commit. After about a minute, hard-refresh your page (Ctrl+Shift+R).

Your old files (for example a separate stylesheet or script) are no longer used. You can leave them or delete them.

## The model

Edit the `MODEL` block near the top of the `<script>` in `index.html` to match your own version:

```js
var MODEL = {
  clSlope: 2 * Math.PI,   // lift-curve slope, per radian
  stallDeg: 15,           // stall angle (degrees)
  postStallLoss: 0.055,   // fraction of stall-CL lost per degree beyond stall
  postStallFloor: 0.35,   // CL never drops below this share of its stall value
  cd0: 0.02,              // zero-lift drag coefficient
  k: 0.05                 // CD = cd0 + k * CL^2
};
```

- Lift and drag: `L = 1/2 * rho * V^2 * S * CL` and `D = 1/2 * rho * V^2 * S * CD`
- `CL = 2*pi*alpha` up to the stall angle, then a heuristic loss beyond it
- `CD = cd0 + k * CL^2` (a simple quadratic polar)

The streamlines are potential flow around a Joukowski airfoil, with the circulation set from the model's CL. They are illustrative, not CFD.

Other tweakable things: slider ranges and defaults (the `CTL` and `S` variables), presets (`PRESETS`), and the Source link in the header.

## Features

- Live streamlines, force vectors and angle-of-attack arc
- Lift, drag, CL, CD and CL / CD readouts
- Presets: Cruise, Takeoff, Near stall, Stalled
- Lift and L/D curves with a draggable marker (arrow keys work too)
- A live free-body diagram with the numbers worked out
- Responsive, keyboard accessible, respects reduced motion
