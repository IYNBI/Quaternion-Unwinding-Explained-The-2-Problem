# Quaternions: Visualising q = −q

> A step-by-step Jupyter notebook proving and animating the double-cover property of unit quaternions — built entirely from scratch with NumPy and Matplotlib.

---

## What this is

This notebook walks through one of the most unintuitive facts in 3D mathematics: **two different quaternions, `q` and `−q`, always represent the exact same rotation in 3D space.** No external quaternion library is used — every formula is implemented by hand so every step is fully transparent.

By the end you will have:
- A working `Quaternion` class with Hamilton multiplication, conjugation, and negation
- A proof that `q` and `−q` produce identical rotation matrices and identical rotated vectors
- An animation of the full 720° double-cover journey through S³

---

## Preview

| Double-cover animation | 3D vector rotation proof |
|---|---|
| w-component sweeps cos(θ/2) across 720° | q and −q land the arrow on the same point |

---

## Notebook structure

| Cell | Topic |
|------|-------|
| 1 | Imports — NumPy, Matplotlib, IPython |
| 2 | `Quaternion` class — `__mul__`, `conjugate`, `__neg__`, `norm` |
| 3 | `rotation_quaternion(axis, angle_deg)` — half-angle formula |
| 4 | `rotate_vector(q, v)` — sandwich product `q · v_pure · q*` |
| 5 | Sweep test — 37 random axes, every 10°, all identical |
| 6 | Rotation matrix proof — `quaternion_to_matrix()` compared for q and −q |
| 7 | Static 3D plots — 4 sample angles, q vs −q side by side |
| 8 | `FuncAnimation` — 720° animated journey with live w-component track |
| 9 | Summary + final numerical proof |

---

## Quick start

```bash
# 1. Clone
git clone https://github.com/your-username/quaternions-double-cover.git
cd quaternions-double-cover

# 2. Install dependencies (only two)
pip install numpy matplotlib

# 3. Launch
jupyter notebook quaternions_explained.ipynb
```

Run all cells with **Kernel → Restart & Run All**.

---

## Requirements

| Package | Version |
|---------|---------|
| Python | ≥ 3.8 |
| NumPy | ≥ 1.21 |
| Matplotlib | ≥ 3.5 |
| Jupyter | any recent |

No `scipy`, no `pyquaternion`, no `transforms3d` — pure NumPy throughout.

---

## The maths in 30 seconds

A unit quaternion encoding a rotation by **θ** around unit axis **n** is:

```
q = cos(θ/2)  +  sin(θ/2) · (nₓi + nᵧj + n_zk)
```

To rotate a 3D vector **v**, embed it as a pure quaternion and use the sandwich product:

```
v' = q · [0, v] · q*
```

Now negate every component:

```
−q = −cos(θ/2)  −  sin(θ/2) · (nₓi + nᵧj + n_zk)
```

The sandwich product `(−q) · [0, v] · (−q)*` expands to:

```
(−1) · q · [0, v] · q* · (−1)  =  q · [0, v] · q*  =  v'
```

The two minus signs cancel. **q and −q are antipodal points on S³ but they map to the same element of SO(3).** This 2-to-1 mapping is the double cover.

---

## Key concepts covered

- **Quaternion algebra** — Hamilton product, conjugate, norm, unit quaternion
- **Rotation encoding** — why the half-angle θ/2 appears
- **Sandwich product** — the standard method for applying a quaternion rotation
- **Double cover** — why S³ covers SO(3) twice, and what it means physically
- **Rotation matrix** — converting a quaternion to a 3×3 matrix and verifying identity
- **720° periodicity** — a continuous path in quaternion space that returns to start after two full 3D rotations

---

## File structure

```
quaternions-double-cover/
├── quaternions_explained.ipynb   # main notebook
└── README.md
```

---

## Further reading

- **3Blue1Brown** — [Quaternions and 3D rotation](https://www.youtube.com/watch?v=zjMuIxRvygQ) (YouTube, highly recommended)
- **Wikipedia** — [Quaternions and spatial rotation](https://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation)
- **Kuipers, J.B.** — *Quaternions and Rotation Sequences*, Princeton University Press
- **Hanson, A.J.** — *Visualizing Quaternions*, Morgan Kaufmann

---

## Licence

MIT — do whatever you like with it.
