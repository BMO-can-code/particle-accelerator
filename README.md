# Synchrotron — Particle Accelerator Simulator

Computational simulation of a synchrotron particle accelerator demonstrating the fundamental principles of beam acceleration: the synchrotron condition (fixed orbit radius with increasing magnetic field), RF cavity energy injection, relativistic kinematics, and optional synchrotron radiation.

**[→ Live Simulation](https://particle-accelerator.vercel.app)** | **[GitHub](https://github.com/BMO-can-code/particle-accelerator)**

---

## Physics Model

### 1. The Synchrotron Principle

A synchrotron maintains a **fixed orbit radius** by increasing the magnetic field as the particle gains energy. The bending radius is:

```
R = p / (q × B)
```

where `p` is the relativistic momentum, `q` is the particle charge, and `B` is the dipole magnetic field. As energy increases, `B` must increase proportionally to keep `R` constant — this is the defining principle of a synchrotron (as opposed to a cyclotron where `B` is fixed and `R` grows).

Rearranging for the required field:
```
B [T] = p [MeV/c] × 10⁶ / (c × q × R)
```

This is how the LHC operates: 1,232 dipole magnets ramp from 0.5 T at injection to 8.3 T at top energy (7 TeV), maintaining the 26.7 km ring radius.

### 2. RF Cavity Acceleration

Each revolution through the RF cavity adds energy:

```
ΔE = q × V_rf
```

where `V_rf` is the peak RF voltage. In the LHC, four RF cavities per beam provide 16 MV total, adding 6.4 MeV per turn at 400 MHz. Over ~10 million revolutions, this accelerates protons from 450 GeV to 6.5 TeV.

The RF frequency must match the revolution frequency times a harmonic number `h`:
```
f_rf = h × f_rev = h × c / (2πR × β)
```

This ensures the particle sees the same accelerating field each turn — the principle of **phase stability**.

### 3. Relativistic Kinematics

At relativistic speeds, classical mechanics fails. The simulation uses:

```
E² = (pc)² + (mc²)²     — energy-momentum relation
γ = E / (mc²)            — Lorentz factor
β = √(1 − 1/γ²)         — velocity as fraction of c
p = γmv = γβmc            — relativistic momentum
KE = (γ − 1)mc²          — kinetic energy
```

As `v → c`, `γ → ∞` and the energy grows without bound. The kinetic energy per RF turn becomes a smaller fraction of the total energy, explaining why acceleration becomes progressively harder at high energies.

### 4. Cyclotron Frequency (Relativistic)

The revolution frequency decreases as `γ` increases:

```
f_rev = cβ / (2πR)
```

In a cyclotron (fixed `B`), this means the particle falls out of sync with the RF — the fundamental limitation that necessitates the synchrotron design.

### 5. Synchrotron Radiation (Electrons)

Charged particles radiate electromagnetic energy when accelerated (curved in a magnetic field):

```
P = (c₂/2π) × E⁴ / (ρ² × m⁴)
```

where `c₂ = 8.85 × 10⁻⁵ GeV⁴ m⁻² s⁻¹`, `E` is total energy, `ρ` is bending radius, and `m` is particle mass.

**Critical mass dependence:** `P ∝ 1/m⁴`. Electrons (m = 0.511 MeV) radiate ~10¹³ times more than protons (m = 938 MeV) at the same energy. This is why:
- Electron synchrotrons need massive RF power to compensate radiation loss
- Proton synchrotrons (like LHC) have negligible radiation loss
- Synchrotron light sources deliberately use electron radiation for experiments

---

## Detector/Accelerator Parameters

| Parameter | Symbol | Value | Notes |
|-----------|--------|-------|-------|
| Ring radius | R | 10–500 m | User adjustable |
| Circumference | C | 2πR | ~314 m at R=50m |
| Initial B-field | B₀ | 0.01–8 T | LHC: 0.5 T injection, 8.3 T top |
| RF voltage | V_rf | 1–1000 kV | LHC: 16 MV total (4 cavities) |
| Synchrotron radiation | c₂ | 8.85e-5 | For electrons |

## Features

- **Four particle types** — proton, electron, positron, lead ion with correct masses and charges
- **Synchrotron condition** — B-field automatically adjusts to maintain constant orbit radius
- **Relativistic dynamics** — full energy-momentum relation, Lorentz factor, velocity
- **RF acceleration** — adjustable voltage, shows energy gain per turn
- **Synchrotron radiation** — correct E⁴/m⁴ scaling, dominant for electrons
- **Live plots** — KE vs turn, γ and β vs turn
- **Telemetry** — velocity, energy, gamma, momentum, B-field in real-time

---

## Significance to CERN Accelerator Physics

This simulator demonstrates the core principles of LHC operation:

1. **Synchrotron design** — The same R = p/(qB) constraint that determines LHC magnet strength. The 1,232 NbTi dipole magnets must track the beam energy from injection to collision.

2. **RF acceleration** — The LHC's 400 MHz superconducting cavities provide the same ΔE = qV_rf per turn. Phase stability keeps the 2808 bunches synchronized over millions of revolutions.

3. **Relativistic limitation** — The plot of γ vs turns shows why higher energies require exponentially more turns: each RF kick adds a fixed ΔE, but the total energy grows, so the fractional gain decreases.

4. **Synchrotron radiation** — The E⁴/m⁴ scaling explains why the LHC accelerates protons (m = 938 MeV) rather than electrons (m = 0.511 MeV) to achieve higher energies. Electron circular colliders (LEP, future FCC-ee) face enormous radiation losses.

These are the same principles tested in CERN accelerator physics interviews and used daily in LHC operation.

---

## References

- Lee, S.Y. *Accelerator Physics* (World Scientific, 2019)
- Edwards & Syphers, *An Introduction to the Physics of High Energy Accelerators* (Wiley, 1993)
- Wille, *The Physics of Particle Accelerators* (Oxford, 2000)
- CERN Accelerator School: [CAS](https://cas.web.cern.ch)
- LHC Design Report, CERN-2004-003

## License

MIT
