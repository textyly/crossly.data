# Crossly Pattern Model

This document outlines the structure and purpose of the **Crossly Pattern** JSON schema, which represents an embroidery design. It is intended for use in digital cross-stitch and embroidery projects, enabling users to define and share patterns in a structured format.

## Motivation

The goal of the **Crossly Pattern** model is to provide a consistent and extensible structure for defining embroidery patterns that can be used in various applications. By standardizing the representation of a pattern, fabric properties, thread definitions, and stitching paths, we aim to facilitate better interoperability between design tools, sharing of patterns, and precise reproduction of designs across platforms.

Embroidery, while an ancient craft, is increasingly being integrated into digital design workflows. The Crossly Pattern model seeks to enable these workflows by allowing for the easy definition, visualization, and sharing of embroidery patterns. The model also provides the flexibility to adapt to various fabric types, thread colors, and custom stitching techniques.

## Schema Explanation

The schema defines a structured object that includes the following key sections:

### 1. `name`
- **Type**: `string`
- **Description**: The name of the embroidery pattern.
  
### 2. `fabric`
Defines the fabric properties where the pattern will be worked. It includes:
- **`name`**: The display name of the fabric type (e.g., 'Aida 14 count').
- **`columns`** and **`rows`**: Defines the dimensions of the fabric grid (width and height).
- **`color`**: Specifies the background color of the fabric.
- **`dots`**: Configures the visual markers on the fabric grid, aiding users in aligning stitches. It includes properties like the color, radius, and spacing of dots, along with hidden dot settings.
- **`threads`**: Defines the default thread appearance for overlay canvas lines (used in UI for reference, not stitching).

### 3. `threads`
An array that defines all the threads used throughout the design. Each thread is described by:
- **`name`**: The name or code of the thread (e.g., 'DMC 321').
- **`color`**: Hex code or named color of the thread.
- **`width`**: Thickness of the thread.

### 4. `pattern`
A list of stitched paths in the design, where each path uses one of the threads defined in the top-level `threads` array. Each pattern object contains:
- **`threadIndex`**: The index of the thread used for this stitching path (referencing the `threads` array).
- **`needlePath`**: A sequence of positions (coordinates) the needle follows on the fabric grid. The order represents the stitching direction, and it includes at least two coordinates to define the path.

## Key Benefits of the Model

- **Standardization**: By using a structured schema, this model ensures consistency in how patterns are defined and shared across applications.
- **Extensibility**: The model can easily accommodate new features, such as additional fabric properties or stitch types, without breaking existing workflows.
- **Clarity**: Clear naming conventions and descriptions help users understand the different components involved in a cross-stitch design.
- **Interoperability**: As a JSON-based format, this model can be integrated with various software applications, allowing users to work with their patterns in multiple contexts, from design tools to production environments.

## Example

Here is an example of how a Crossly Pattern might look in JSON format:

```json
{
    "name": "Simple Cross Stitch",
    "fabric": {
        "name": "Aida 14",
        "columns": 10,
        "rows": 10,
        "color": "#fff8dc",
        "dots": {
            "color": "#9fa19f",
            "radius": 1.4,
            "space": 24,
            "hidden": {
                "enabled": true
            }
        },
        "threads": {
            "color": "#d2d4d2",
            "width": 1.4
        }
    },
    "threads": [
        {
            "name": "DMC 321",
            "color": "#C00000",
            "width": 1
        },
        {
            "name": "DMC 310",
            "color": "#000000",
            "width": 1
        }
    ],
    "pattern": [
        {
            "threadIndex": 0,
            "needlePath": [
                {
                    "x": 2,
                    "y": 2
                },
                {
                    "x": 4,
                    "y": 4
                },
                {
                    "x": 4,
                    "y": 2
                },
                {
                    "x": 2,
                    "y": 4
                }
            ]
        },
        {
            "threadIndex": 1,
            "needlePath": [
                {
                    "x": 6,
                    "y": 2
                },
                {
                    "x": 4,
                    "y": 4
                },
                {
                    "x": 6,
                    "y": 4
                },
                {
                    "x": 4,
                    "y": 2
                }
            ]
        }
    ]
}
