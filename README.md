# Crossly Pattern Data Model

This document describes the JSON data model used by **Crossly**, an open-source tool for designing and sharing cross-stitch embroidery patterns.

## Overview

A **Crossly pattern** represents a needlework design on a logical grid of fabric. The model captures:
- Fabric (Canvas) dimensions and appearance (`fabric`)
- Threads available for stitching (`threads`)
- A list of needle paths through the grid (`pattern`)

The model separates data and rendering, focusing on logical stitch paths — leaving interpretation (like visual rendering or semantic meaning) to the engine or UI.

---

## Schema Components

### `name` (string)
The name of the pattern. Human-readable, used for display.

---

### `fabric` (object)
Describes the canvas/grid on which stitching occurs.

| Property     | Description |
|--------------|-------------|
| `name`       | Display name of fabric type (e.g. "Aida 14 count"). |
| `columns`    | Number of columns in the logical grid. |
| `rows`       | Number of rows in the logical grid. |
| `color`      | Background color of the fabric. |
| `dots`       | Appearance and spacing of alignment dots on the logical grid. |
| `threads`    | Color and width of the optional overlay lines for grid guidance (not the stitch threads). |

---

### `threads` (array of objects)
Defines the threads available for stitching the pattern.

Each thread includes:
- `name`: Label or code (e.g. `"DMC 321"`)
- `color`: Hex or named color string
- `width`: Visual thickness in drawing units

Threads are **referenced by index** in the `pattern` section.

---

### `pattern` (array of objects)
Describes the **needle paths** (not just stitches!) that form the design.

Each path contains:
- `threadIndex`: Index of the thread used from the `threads` array
- `needlePath`: Sequence of dot positions `(indexesX[i], indexesY[i])` visited in order

```json
"needlePath": {
  "indexesX": [4, 5, 4],
  "indexesY": [4, 5, 6]
}
