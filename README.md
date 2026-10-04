# Roblox UI Engine Updates: New UI Capabilities

Roblox's UI engine provides native tools to customize interfaces directly inside Roblox Studio without needing external image assets or sliced texture hacks. Below is a detailed breakdown of the key UI engine classes: [UIShadow](https://create.roblox.com/docs/reference/engine/classes/UIShadow) and [UICorner](https://create.roblox.com/docs/reference/engine/classes/UICorner).

---

## 1. [UICorner](https://create.roblox.com/docs/reference/engine/classes/UICorner)

The `UICorner` class is a UI modifier that applies procedural corner deformation to its parent `GuiObject` (such as `Frame`, `TextButton`, `ImageLabel`, or `TextBox`). It clips input and visual rendering to rounded corner bounds.

### Internal Calculation Rules
* **Uniform Aspect Radius:** The radius of the X axis is always calculated to match the radius of the Y axis.
* **Scale Resolution:** When using `Scale` values in `UDim`, the percentage rounding always calculates based on the minimum dimension (width or height) of the parent object.

### Property Reference

| Property | Data Type | Description & Usage |
| :--- | :--- | :--- |
| **`CornerRadius`** | `UDim` | Defines the default curvature radius for all four corners. Serves as the global base value. |
| **`TopLeftRadius`** | `UDim` | Overrides and sets specific corner curvature for the top-left corner. |
| **`TopRightRadius`** | `UDim` | Overrides and sets specific corner curvature for the top-right corner. |
| **`BottomLeftRadius`** | `UDim` | Overrides and sets specific corner curvature for the bottom-left corner. |
| **`BottomRightRadius`** | `UDim` | Overrides and sets specific corner curvature for the bottom-right corner. |

---

## 2. [UIShadow](https://create.roblox.com/docs/reference/engine/classes/UIShadow)

The `UIShadow` class introduces native vector drop shadows for parent `GuiObject` containers, rendering dynamic elevation and ambient depth without requiring pre-rendered soft-blur texture assets.

### Core Features
* **Native Vector Rendering:** Scalable, performant shadow rendering across all screen resolutions without memory overhead from static textures.
* **Dynamic Lighting Controls:** Complete control over shadow offset, blur diffusion, expansion spread, color tinting, and transparency.

### Property Reference

| Property | Data Type | Description & Usage |
| :--- | :--- | :--- |
| **`BlurRadius`** | `UDim` | Controls the softness and blur diffusion of shadow edges. |
| **`Color`** | `Color3` | Specifies the RGB color tint of the cast shadow. |
| **`Enabled`** | `boolean` | Toggles rendering of the drop shadow effect on or off. |
| **`Offset`** | `UDim2` | Defines positional shift of the shadow relative to the parent origin across X and Y axes. |
| **`Spread`** | `UDim2` | Expands or contracts shadow boundaries beyond the parent bounding box. |
| **`Transparency`** | `number` | Sets shadow opacity, ranging from `0` (completely opaque) to `1` (completely transparent). |
| **`ZIndex`** | `number` | Determines rendering hierarchy and draw order relative to sibling UI elements. |

---

## Combined Workflow Example

Combining `UICorner` (with individual corner controls) and `UIShadow` allows for advanced modern UI components like tabbed cards, asymmetrical header panels, and pill buttons:

```
[ GuiObject: Frame ]
├── UICorner (TopLeftRadius = 12px, TopRightRadius = 12px, BottomLeftRadius = 4px, BottomRightRadius = 4px)
└── UIShadow (BlurRadius = 8px, Offset = (0, 4), Transparency = 0.5)
