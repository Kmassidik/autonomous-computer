# Assembled model — 2× desk box

An assembled STEP of the 2× housing, built from the parts in
[`../step_models`](../step_models). The upstream repo publishes the 2× and 4×
housings as individual parts only.

| File | Parts | Envelope | Aluminium | Size |
|:--|--:|:--|--:|--:|
| `2x-box-ASSEMBLY.step` | 8 | 307.6 × 315.0 × 404.0 mm (12.1 × 12.4 × 15.9 in) | 4.96 kg | 11.7 MB |

The README for this build states **12.5 × 12.5 × 16 in**. Agreement is within
0.4 in, the difference being panel thickness and where the outer covers sit.

**This housing has no placement faults.** Unlike the 4× cube — where
`Part 2 - Back` is stored rotated 90° and 272 mm high, see
[`../../4x-5090/assembly/README.md`](../../4x-5090/assembly/README.md) — every
part here is already in its correct assembly position. Merging them is a
compound and nothing else.

## Two files are not what their names suggest

Worth knowing before anyone tries to cut or print them.

### `Part 2 - Back.step` is not a panel

It contains **127 solids** and measures 398 × 315 × 168 mm. Breaking it down by
solid:

| Count | Size (mm) | Reading |
|--:|:--|:--|
| 1 | 163 × 86 × 150, 2,005 cm³ | power supply |
| 2 | 130.4 × 130.4 × 25.2 | 130 mm fans |
| 2 | 111.1 × 110.6 × 21.4 | 110 mm fans |
| 16 | 27.8 × 27.8 × 9.9 | small components |
| 40 | 8.6 × 3.2 × 0.2 | — |
| 38 | 4.4 × 0.5 × 0.1 | — |

These are the **internal components**, not sheet metal. It is excluded from the
assembly above, which is housing only.

The consequence: **the 2× housing has no back panel in the published CAD.** The
4× set has one (`Part 9 - Side`, the 2 mm mesh); this set does not.

### `Support.step` is 22 separate blocks

Not one part — **22 solids** in two sizes:

| Count | Size (mm) | Same as, in the 4× set |
|--:|:--|:--|
| 14 | 17.5 × 17.5 × 14.5 | `L mount` |
| 8 | 19.5 × 19.5 × 19.5 | `Corner mount` |

So it is the standoff and corner-mount hardware bundled into a single file,
matching the 4× parts exactly. Quote it as 22 small milled blocks in two sizes,
not as one component.

## Sheet parts and cut path

[`../drawings`](../drawings) carries dimensioned outlines and DXF for the four
laser-cut parts, generated from these STEP files with FreeCAD 1.1.4.

| Part | Size (mm) | Thickness | Cut path |
|:--|:--|--:|--:|
| Part 10 - Side cover | 314.0 × 393.0 | 4.0 | 32.95 m |
| Part 1 - Side | 238.0 × 339.0 | 6.0 | 21.42 m |
| Part 3 - Top | 250.0 × 250.0 | 6.0 | 15.77 m |
| Part 5 - Middle | 271.9 × 395.5 | 6.0 | 3.25 m |
| | | **total** | **73.39 m** |

About half the laser work of the 4× cube, which runs to 143.6 m.

The remaining housing parts are milling work: `Part 4 - Bottom` (307.6 × 307.6 ×
15 mm), `GPU mount 1` (15 mm), `GPU mount 2` (30.5 mm), and the 22 blocks in
`Support`.

As with the 4× build, the panels are **sheet, not milled from solid** — 4 mm and
6 mm. A quote priced as milling from solid is pricing the wrong process.

## Reproducing this

Generated headless from the published STEP files:

```bash
PYTHONDONTWRITEBYTECODE=1 \
  /Applications/FreeCAD.app/Contents/Resources/bin/freecadcmd script.py
```

`PYTHONDONTWRITEBYTECODE=1` matters: without it Python writes `.pyc` inside
`FreeCAD.app`, invalidating its code signature so macOS then refuses to launch
the GUI.
