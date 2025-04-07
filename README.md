# Crossly Data Model

This model defines the structure of a **Crossly pattern**, which encodes embroidery designs using **logical paths**, **threads**, and a **fabric canvas**. Instead of relying on graphics or SVG, this model focuses on *semantic description* of the stitch process, making it ideal for analysis, editing, and AI-driven tools.

## Top-Level Properties

- **`name`**: Name of the embroidery pattern.
- **`fabric`**: Defines the canvas, appearance, and fabric details used as a stitching base.
- **`threads`**: A palette of threads, each with a name, color, and width.
- **`stitches`**: A list of individual stitch instructions using paths of dots and threads.

---

## Fabric

The `fabric` object contains everything needed to render and align the pattern:

- **`name`**: User-friendly name (e.g. "Aida 14").
- **`columns` / `rows`**: Dimensions of the fabric canvas.
- **`color`**: Background color of the fabric.
- **`dots`**: Visual aid showing canvas points (used in UIs).
  - `color`, `radius`, `space`: Control appearance and spacing.
  - `hidden.enabled`: Optionally show hidden dots.
- **`threads`**: Lines shown between stitches to simulate fabric weave.

---

## Threads

Each thread defines how it will look and behave:

- **`name`**: Label or code (e.g. DMC thread code).
- **`color`**: Hex or named color (e.g. "#ff0000").
- **`width`**: Thickness used when drawing the stitch path.

---

## Stitches

Each `stitch` contains:

- **`thread.index`**: Index into the threads array [threads](#Threads) to define which thread is used.
- **`path.dotsX` and `path.dotsY`**: A sequence of X and Y coordinates, forming the thread path. Coordinates must be aligned by index (i.e. first X and Y form one point, second X and Y form the next, etc.)

This path-based approach makes it possible to represent any kind of stitch (cross stitch, half stitch, backstitch and so forth) by controlling the needle path.

---

## Why Not SVG?

This model abstracts away from SVG and graphical tools:

- Focuses on **real-world stitching concepts**, not just appearance.
- Captures **intent**, not just **look**.
- Enables **AI, logic, validation**, and even export to **embroidery machines** or **pattern generators**.
- Allows **custom stitch libraries** and **technique modeling** without needing a drawing engine.

---

## Summary

The Crossly data model is a **domain-first** representation of embroidery that makes pattern generation, sharing, editing, and automation both **human-readable** and **machine-usable**.

It’s not just about drawing — it’s about **stitching with intent**.
