# Particle Accelerator — Relativistic Beam Dynamics Simulator

Computational simulation of proton beam dynamics in a circular particle accelerator, implementing relativistic kinematics under Lorentz force and RF cavity acceleration. Models core principles of accelerator physics relevant to LHC beam operation.

**[→ Live Simulation](https://particle-accelerator.vercel.app)** | **[GitHub](https://github.com/BMO-can-code/particle-accelerator)**

---

## Physics Model

### Relativistic Kinematics

The proton's relativistic momentum is updated at each integration step:

```
p_new = p_old + F_total · dt
v     = p / (γ · m)
γ     = 1 / √(1 − v²/c²)
```

Unlike classical `F = ma`, force changes **momentum** directly. Velocity is recovered from momentum via the Lorentz factor γ, which naturally enforces the speed-of-light limit: as v → c, γ → ∞, requiring infinite energy for further acceleration.

### Lorentz Force — Magnetic Bending

A uniform magnetic field **B** perpendicular to the orbital plane provides centripetal bending via the cross product:

```
F = q(v × B)
F_x = q · v_y · B_z
F_y = −q · v_x · B_z
```

This force is always perpendicular to velocity — it bends the trajectory without changing speed. The cyclotron radius `R = γmv / (qB)` grows with γ, demonstrating why stronger magnets are required at higher beam energies (the fundamental design constraint of the LHC).

### RF Cavity Acceleration

A localized electric field region models the RF cavity. When the proton enters the cavity angular region:

```
F_rf = q · E_field (tangential)
ΔKE  = q · V_rf    (energy gain per revolution)
```

This is the same mechanism by which the LHC's 400 MHz cavities accelerate protons from injection (450 GeV) to collision energy (6.5 TeV) over ~10 million revolutions.

### Symplectic Integration — Euler-Cromer Method

The equations of motion are integrated using the **Euler-Cromer method**, a symplectic integrator:

1. Update momentum: `p_{n+1} = p_n + F(x_n, v_n) · Δt`
2. Recover velocity: `v_{n+1} = p_{n+1} / (γ_{n+1} · m)`
3. Update position: `x_{n+1} = x_n + v_{n+1} · Δt`

Unlike standard Euler (which updates v then x using the same timestep), Euler-Cromer uses the **updated velocity** for position. This semi-implicit scheme is symplectic — it conserves a shadow Hamiltonian, preventing the artificial energy drift that makes standard Euler unsuitable for long accelerator simulations.

## Numerical Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Time step Δt | 5 × 10⁻¹¹ s | Resolves cyclotron frequency at B = 1 T |
| Total steps | 200,000 | ~10 μs simulation time |
| Safety clamp | v < 0.9999c | Prevents numerical超光速 from rounding |
| Lorentz floor | ε = 10⁻¹² | Prevents division by zero at ultra-relativistic speeds |
| Iterative solver | 5 fixed-point iterations | Recovers v from p = γ(v)mv |

## Features

- Classical vs. Relativistic physics toggle — compare Newtonian and Einsteinian dynamics
- Adjustable magnetic field (0.1–5 T) and RF cavity voltage (10–500 kV)
- Real-time telemetry: velocity (% of c), kinetic energy (MeV), Lorentz factor γ
- Color-coded trajectory visualization (blue → red = accelerating)
- Kinetic energy vs. time plot showing energy accumulation per revolution
- 60fps Canvas rendering with 1×–100× playback speed

## Significance to Accelerator Physics

This simulator demonstrates the core computational challenges of beam dynamics modeling:

- **Relativistic momentum tracking** — the same formulation used in beam optics codes (MAD-X, COMSOL)
- **Energy conservation verification** — symplectic integration prevents unphysical energy gain/loss
- **RF synchronization** — cavity field timing relative to particle arrival (phase stability)
- **Magnetic rigidity** — the relationship between B-field strength and beam momentum that dictates magnet design

These principles directly underpin LHC operation, where 2808 bunches of protons circulate at 99.9999991% of c, requiring superconducting dipole magnets at 8.3 T and RF cavities at 400 MHz.

## References

- Lee, S.Y. *Accelerator Physics* (World Scientific, 2019)
- Edwards & Syphers, *An Introduction to the Physics of High Energy Accelerators* (Wiley, 1993)
- CERN Accelerator School: [CAS](https://cas.web.cern.ch)

## License

MIT
