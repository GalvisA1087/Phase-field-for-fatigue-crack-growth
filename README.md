# Phase-field-for-fatigue-crack-growth

**Phase-field modelling of low- and high-cycle fatigue crack growth in brittle materials using FreeFEM++**

This repository contains a fully documented implementation of an adaptive **phase-field framework for fatigue crack growth in brittle materials**, covering both the **low-cycle (LCF)** and **high-cycle (HCF)** fatigue regimes, using [FreeFEM++](https://freefem.org). The code is written for serial execution and combines:

- a **cycle-based quasi-monolithic solver** with optional same-load corrections of the history-dependent fields,
- **metric-based mesh adaptation** after every computed loading cycle, without pre-refined regions along the expected crack paths,
- an **explicit cycle-jump scheme**, activated through a single parameter, for simulations involving large numbers of cycles,
- an optional **boundary-mask treatment** to suppress spurious damage at loaded or constrained boundaries.

It accompanies the paper:

> _An adaptive phase-field framework for low- and high-cycle fatigue crack growth in brittle materials_  
> Andres F. Galvis, Smita Sahu, Daniel M. Prada, Julian A. Ávila  
> *Submitted to International Journal of Fatigue (DOI to be added upon publication)*

and builds on the quasi-static and dynamic implementation available at [Phase-field-for-brittle-fracture](https://github.com/GalvisA1087/Phase-field-for-brittle-fracture).

---

## 📁 Repository Structure

Each example folder contains the five problem-specific scripts required to reproduce the corresponding numerical benchmark described in the paper.

```
Phase-field-for-fatigue-crack-growth/
├── CODE/                        # Main simulation scripts (modular .edp files)
├── Examples/                    # Example problems from the paper (Section 4.x)
│   ├── 4.1/                     # Single-edge notched tension test
│   ├── 4.2/                     # Single-edge notched shear test (R = 0 and R = -1)
│   ├── 4.3/                     # Asymmetric double notched plate
│   ├── 4.4/                     # Plate with a hole and multiple cracks
│   └── 4.5/                     # Cycle-jump acceleration in the LCF and HCF regimes
├── LICENSE                      # GNU GPL v3.0 license
└── README.md                    # Project documentation (this file)
```

Each subfolder of `Examples/` contains the files:

```
Mesh.edp  BoundaryConditions.edp  Variational.edp  Mask.edp  Parameters.edp
```

---

## ⚙️ Requirements

To run the code, you need:

- [**FreeFEM++**](https://freefem.org) (version 4.9 or newer recommended)  
  Compatible with **Linux**, **macOS**, and **Windows**

> 📌 Only the `iovtk`, `lapack` and `MUMPS_seq` plugins are used, all of which are included in the standard FreeFEM++ distribution.  
> No external libraries or parallel tools are required. The code runs in **serial** mode.

---

## 🚀 How to Run an Example

By default, `CODE/` is configured for the **plate with a hole and multiple cracks** (Section 4.4) with `Ncorr = 1`, so it can be run directly.

1. Choose the example you want to run from the `Examples/` directory (e.g. `Examples/4.2/`)
2. Copy the five `.edp` files from that folder into the `CODE/` directory, replacing the existing files
3. Create the output folder defined by `vtuFiles` in `Parameters.edp` (by default `Results_sPFf/` inside `CODE/`)
4. Open a terminal and navigate to the `CODE/` folder
5. Run the main script:

```bash
FreeFem++ sPFf.edp
```

To activate the cycle-jump scheme, set `DN > 0` in `Parameters.edp`. To use the boundary mask, set `Usingmask = 1` and define the protected boundary labels in `Mask.edp`.

---

## 📊 Outputs

After every computed cycle, the phase-field, displacement, strain and stress fields, together with the von Mises equivalent stress, are converted back to dimensional form and exported in **VTU** format to the output folder, so they can be visualised in [ParaView](https://www.paraview.org). The phase field is also plotted during the simulation in the FreeFEM++ graphics window.

---

## 📖 Citation

If you use this code, please cite:

```bibtex
@article{Galvis2026,
  author  = {Galvis, Andres F.},
  title   = {Phase-field modelling of quasi-static and dynamic brittle fracture: A FreeFEM++ implementation},
  journal = {Engineering Fracture Mechanics},
  volume  = {333},
  pages   = {111846},
  year    = {2026},
  doi     = {10.1016/j.engfracmech.2026.111846}
}
```

---

## 📄 License

This project is licensed under the **GNU General Public License v3.0**. See the [LICENSE](LICENSE) file for details.
