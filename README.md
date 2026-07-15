# ⚛️ Particle Accelerator — 2D Relativistic Simulator

A real-time, browser-based 2D relativistic particle accelerator simulator that models proton dynamics inside a circular accelerator ring. Built with vanilla HTML5 Canvas and JavaScript — zero dependencies, runs entirely in the browser.

**[→ Live Demo on Vercel](https://particle-accelerator.vercel.app)**

![Screenshot](screenshot.png)

---

## Features

- **Real-time 60fps animation** — smooth Canvas rendering with `requestAnimationFrame`
- **Full relativistic physics** — Lorentz factor γ = 1/√(1 − v²/c²), relativistic momentum p = γmv
- **Lorentz force** — magnetic field bending via F = q(v × B) cross product
- **RF cavity acceleration** — electric field kicks that increase particle energy each revolution
- **Euler-Cromer integration** — symplectic numerical method that conserves energy over long simulations
- **Adjustable speed** — simulation speed from 1× to 100×
- **Classical vs Relativistic toggle** — compare Newtonian mechanics against Einstein's special relativity
- **Live telemetry** — velocity (% of c), kinetic energy (MeV), Lorentz factor γ, revolution count
- **Color-coded trajectory** — blue → red gradient showing acceleration over time
- **Deployed on Vercel** — zero-config static hosting, instant global CDN

## Physics

| Concept | Equation | Description |
|---------|----------|-------------|
| Lorentz Force | `F = q(v × B)` | Magnetic force bends proton into circular orbit |
| RF Cavity | `ΔKE = qV` | Electric field adds energy per revolution |
| Lorentz Factor | `γ = 1/√(1 − v²/c²)` | Relativistic mass increase near speed of light |
| Relativistic Momentum | `p = γmv` | Momentum diverges as v → c |
| Kinetic Energy | `KE = (γ − 1)mc²` | Energy grows without bound relativistically |
| Euler-Cromer | Update p → v → x | Symplectic integrator, conserves shadow Hamiltonian |

## Tech Stack

- **HTML5 Canvas** — hardware-accelerated 2D rendering
- **Vanilla JavaScript** — no frameworks, no build step
- **CSS Grid** — responsive dark-theme layout
- **Vercel** — zero-config static deployment

## Getting Started

```bash
# Clone the repo
git clone https://github.com/BMO-can-code/particle-accelerator.git
cd particle-accelerator

# Open in browser
open index.html

# Or deploy to Vercel
npx vercel --prod
```

## Project Structure

```
particle-accelerator/
├── index.html          # Complete app: physics engine + UI + rendering
├── vercel.json         # Vercel deployment config
└── README.md           # This file
```

## How It Works

1. **Physics Engine** — Pre-computes 200,000 Euler-Cromer integration steps with configurable magnetic field (0.1–5 T), RF cavity voltage (10–500 kV), and optional special relativity
2. **Animation Loop** — `requestAnimationFrame` renders pre-computed data at 60fps, with adjustable playback speed (1×–100×)
3. **Visualization** — Dual-panel display: 2D trajectory with color-coded velocity + kinetic energy vs time chart
4. **Telemetry** — Real-time metrics: velocity as % of c, kinetic energy in MeV, Lorentz factor γ, position, simulation time

## License

MIT
