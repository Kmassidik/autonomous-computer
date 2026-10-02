# Assembled model — 4× cube

An assembled STEP of the 4× housing, built from the fifteen parts in
[`../step_models`](../step_models). The upstream repo publishes the 4× and 2×
housings as individual parts only; the single assembled model exists just for
the archived 8× build.

| File | Parts | Envelope | Size |
|:--|--:|:--|--:|
| `4x-cube-ASSEMBLY.step` | 15 | 517.4 × 509.9 × 616.5 mm (20.4 × 20.1 × 24.3 in) | 14.4 MB |

The README for this build states **19.8 × 19.8 × 24.2 in**. Height matches; the
extra width is panel thickness sitting proud of the frame.

## Why this was easy to build

Each part file already carries its **assembly coordinates** rather than sitting
at its own origin — `Part 1 - Bottom` at Z −466.6, `Part 4 - Middle` at Z −282.6,
`Part 3 - Top` at Z +143.9. Merging them is a compound, not a fitting job.

## Two parts needed correcting

Assembling the published parts as-is gives an envelope **888.3 mm tall** instead
of 616.5 mm. Two parts fall outside the frame:

| Part | Offset from frame | |
|:--|--:|:--|
| `Part 2 - Back` | **+271.8 mm** above | also stored rotated 90° |
| `L mount` | +100.8 mm above | small bracket |

The six structural parts — Bottom, Middle, Top, Side, Corner 1, Corner 2 —
assemble correctly on their own into **506.2 × 505.9 × 616.5 mm**, i.e.
19.9 × 19.9 × 24.3 in, matching the published dimensions to within 0.1 in.

### `Part 2 - Back` — rotation (verified)

As published, the panel measures **4.0 × 606.5 × 498.0 mm**: thin along X, with
its long 606.5 mm axis lying along Y. A wall of this frame needs the 606.5 mm
axis vertical — the frame is 616.5 mm tall and `Part 9 - Side` spans exactly
606.5 mm in Z.

Rotating **120° about the (1,1,1) axis** gives **498.0 × 4.0 × 606.5 mm** — thin
in Y, as a Y-face wall should be. Three independent checks then line up:

| Check | Result |
|:--|:--|
| Resulting X span vs `Part 1 - Bottom` | 15.2 … 513.2 — **exact match** |
| Resulting Z span vs `Part 9 - Side` | −462.6 … 143.9 — **exact match** |
| Bounding-box overlap with the other 13 parts | **none** |

Three exact coincidences at once is not chance, so the rotation is taken as
established.

### What is *not* established

**Which Y face it belongs to.** Y-min and Y-max are both flush and both clear;
the CAD does not record which. `Y-min` was chosen here. If that is wrong it is a
mirror, and it **changes nothing for fabrication** — the part is identical either
way.

This also fits the assembly guide, which fits three panels in steps 21–23 while
only one `Part 9 - Side` is published: the frame appears to use 3× mesh side and
1× back, so which face is "back" is a build decision that the part files do not
capture.

**`L mount`.** It is demonstrably floating, but its correct seat cannot be
derived from the geometry without guessing. It was translated down so its top
sits at the frame's top plane — enough to keep it inside the envelope, but it
should not be treated as a correct placement.

A corrected copy of the panel alone is at
[`../step_models/Part 2 - Back - CORRECTED.step`](../step_models/Part%202%20-%20Back%20-%20CORRECTED.step).
The original is untouched.

## Drawings

[`../drawings`](../drawings) carries dimensioned flat outlines and DXF files for
the sheet parts, generated from these STEP files with FreeCAD 1.1.4.

Measured from the CAD, the sheet parts total **143.6 m of cut path**, of which
`Part 9 - Side` alone is **77.96 m** — 54% of the laser work in one panel.

One note for anyone quoting this housing: the build README describes the
enclosure as *milled from solid aluminium*. The panels are not. `Part 9 - Side`
is **2 mm**, `Part 2 - Back` is **4 mm**, Top and Middle are **6 mm** — sheet
parts for laser cutting. A quote priced as milling from solid is pricing the
wrong process.

| Part | Size (mm) | Thickness | Cut path |
|:--|:--|--:|--:|
| Part 9 - Side | 498.0 × 606.5 | 2.0 | 77.96 m |
| Part 3 - Top | 496.0 × 496.0 | 6.0 | 23.87 m |
| Part 2 - Back | 606.5 × 498.0 | 4.0 | 23.69 m |
| 9 Fan mount | 464.0 × 464.0 | 10.0 | 5.84 m |
| Part 4 - Middle | 498.0 × 498.0 | 6.0 | 5.41 m |
| Part 8 - GPU Holder 2 | 294.0 × 294.0 | 5.0 | 2.74 m |
| 3 Fan mount | 478.0 × 124.0 | 10.0 | 2.46 m |
| Part 6 - Corner 2 | 52.0 × 421.5 | 5.0 | 1.01 m |
| Part 5 - Corner 1 | 52.0 × 171.0 | 5.0 | 0.53 m |
| Part 10 - Button | 17.4 × 17.5 | 7.0 | 0.06 m |

The remaining five parts — Bottom (15 mm), GPU Holder 1, GPU mount, Corner mount
and L mount — are milling work.

## Reproducing this

Nothing here is hand-modelled. The assembly, the measurements and the drawings
were all produced headless from the published STEP files:

```bash
PYTHONDONTWRITEBYTECODE=1 \
  /Applications/FreeCAD.app/Contents/Resources/bin/freecadcmd script.py
```

The `PYTHONDONTWRITEBYTECODE=1` matters: without it Python writes `.pyc` files
inside `FreeCAD.app`, which invalidates its code signature and makes macOS
refuse to launch the GUI afterwards.
