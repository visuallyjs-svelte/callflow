### Summary
This demo illustrates a call flow diagram builder using VisuallyJS in Svelte. It features a canvas with drag-and-drop capabilities from a palette and an inspector for editing node details.

### Components Used
- `SurfaceProvider`: Provides context for the VisuallyJS surface to its children.
- `SurfaceComponent`: The main canvas area where the diagram is rendered.
- `ControlsComponent`: Provides UI controls for zooming, undo/redo, etc.
- `MiniviewComponent`: A small overview map of the canvas.
- `PaletteComponent`: (Used in `CallFlowPalette.svelte`) Provides a draggable palette of nodes.
- `InspectorComponent`: (Used in `Inspector.svelte`) Provides a UI for inspecting and editing selected nodes.

### Component Options
#### `SurfaceComponent`
- `renderOptions`: Configuration for how elements are rendered on the surface.
- `viewOptions`: Configuration for the view, such as zoom levels and panning.
- `modelOptions`: Configuration for the underlying data model.
- `url`: The URL to load the initial dataset from.
- `className`: CSS class name for the canvas container.

#### `MiniviewComponent`
- Inherits default configuration for the overview map.

### Stylesheet Requirement
The `visuallyjs.css` stylesheet must be included in the application for the components to render correctly.

```css
@import "@visuallyjs/browser-ui/css/visuallyjs.css";
```
