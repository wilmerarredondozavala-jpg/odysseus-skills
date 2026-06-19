---
name: excalidraw
description: "Hand-drawn Excalidraw JSON diagrams (arch, flow, seq)."
---

# Excalidraw Diagrams

## When to use
When you need to create architecture diagrams, flowcharts, sequence diagrams, or concept maps.

## How

### File Structure
```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "hermes-agent",
  "elements": [...],
  "appState": {"viewBackgroundColor": "#ffffff"}
}
```

### Element Types
```json
// Rectangle
{"type": "rectangle", "id": "r1", "x": 100, "y": 100, "width": 200, "height": 100, "roundness": {"type": 3}}

// Ellipse
{"type": "ellipse", "id": "e1", "x": 100, "y": 100, "width": 150, "height": 150}

// Diamond
{"type": "diamond", "id": "d1", "x": 100, "y": 100, "width": 150, "height": 150}

// Arrow
{"type": "arrow", "id": "a1", "x": 300, "y": 150, "width": 200, "height": 0, "points": [[0,0],[200,0]], "endArrowhead": "arrow"}

// Text
{"type": "text", "id": "t1", "x": 150, "y": 138, "text": "Hello", "fontSize": 20, "fontFamily": 1}
```

### Labeled Shapes (Container Binding)
```json
// Shape with bound text
{"type": "rectangle", "id": "r1", "x": 100, "y": 100, "width": 200, "height": 80,
  "roundness": {"type": 3}, "backgroundColor": "#a5d8ff",
  "boundElements": [{"id": "t_r1", "type": "text"}]}

// Text bound to shape
{"type": "text", "id": "t_r1", "x": 105, "y": 110, "width": 190, "height": 25,
  "text": "Hello", "fontSize": 20, "fontFamily": 1,
  "containerId": "r1", "originalText": "Hello", "autoResize": true}
```

### Arrow Bindings
```json
{
  "type": "arrow", "id": "a1",
  "startBinding": {"elementId": "r1", "fixedPoint": [1, 0.5]},
  "endBinding": {"elementId": "r2", "fixedPoint": [0, 0.5]}
}
```
fixedPoint: top=[0.5,0], bottom=[0.5,1], left=[0,0.5], right=[1,0.5]

### Color Palette
| Use | Color |
|-----|-------|
| Primary/Input | `#a5d8ff` (light blue) |
| Success/Output | `#b2f2bb` (light green) |
| Warning/External | `#ffd8a8` (light orange) |
| Processing | `#d0bfff` (light purple) |
| Error/Critical | `#ffc9c9` (light red) |
| Notes/Decisions | `#fff3bf` (light yellow) |
| Storage/Data | `#c3fae8` (light teal) |

### Sizing
- Minimum font: 16 (body), 20 (titles), 14 (annotations only)
- Minimum shape: 120x60
- Gap between elements: 20-30px minimum

### Tips
- NO emoji in text (doesn't render)
- Array order = z-order (first = back, last = front)
- Place bound text immediately after its container shape
- Upload to excalidraw.com for shareable link
