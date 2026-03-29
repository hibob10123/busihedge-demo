# Design System Specification: Precision Editorial

## 1. Overview & Creative North Star
**The Creative North Star: "The Financial Ledger"**

This design system eschews the bubbly, rounded trends of consumer tech in favor of a high-end, editorial aesthetic rooted in Swiss design principles. It is built on the concept of **Architectural Precision**. We treat the interface not as a collection of widgets, but as a sophisticated financial document. 

The system moves beyond "standard" UI by leveraging a rigid adherence to a 0.35rem baseline grid, extreme whitespace, and intentional sharp-edged geometry. By forbidding shadows and gradients, we place the entire burden of hierarchy on typography and tonal shifts, resulting in a product that feels authoritative, transparent, and permanent.

---

## 2. Colors & Tonal Architecture
The palette is a study in "High-Contrast Neutrals." We use a clinical white and off-white base to allow the data—the most important element—to command attention.

### Core Palette
- **Background (`surface`):** `#f9f9f9` – A crisp, cool-toned neutral that prevents screen fatigue.
- **Primary Text (`on_surface`):** `#1a1c1c` – Near-black for maximum legibility.
- **Accent (`primary_container`):** `#0066ff` – Used sparingly for "The Path of Success."
- **Success (`secondary`):** `#16a34a` – For payouts and growth.
- **Risk (`tertiary_container`):** `#dc2626` – High-visibility for risk and alerts.

### The "No-Line" & Surface Rule
To maintain a premium feel, avoid using 1px borders to separate large sections. Instead, use **Surface Nesting**:
- **Level 0 (Global):** `surface` (`#f9f9f9`)
- **Level 1 (Cards/Panels):** `surface_container_lowest` (`#ffffff`) 
- **Level 2 (In-card Wells):** `surface_container` (`#eeeeee`)

**The Signature Texture:** While the system is flat, we achieve "soul" through the interplay of `surface` and `surface_container_low`. Use a 1px `outline_variant` (`#c2c6d8`) at **10% opacity** only when a card sits on a background of the same color. Otherwise, let the change in hex value define the edge.

---

## 3. Typography: The Semantic Engine
Typography is the primary tool for navigation. We use **Inter** for structural narrative and **JetBrains Mono** for technical data.

### Technical Data (JetBrains Mono)
All currency, percentages, and timestamps must use JetBrains Mono. This typeface signals "raw data" and "accuracy."
- **Data-Lg:** 1rem / Medium (500) / Tracking -2%
- **Data-Sm:** 0.75rem / Regular (400)

### Editorial Hierarchy (Inter)
- **Display-Md:** 2.75rem / Semi-Bold (600) / Leading 1.1. Used for portfolio totals.
- **Headline-Sm:** 1.5rem / Medium (500) / Tracking -1%. For section headers.
- **Title-Sm:** 1rem / Semi-Bold (600). For card titles.
- **Body-Md:** 0.875rem / Regular (400). For standard interface text.
- **Label-Sm:** 0.6875rem / Semi-Bold (600) / Uppercase. For table headers and metadata.

---

## 4. Elevation & Depth: Tonal Layering
This system prohibits traditional box-shadows. Depth is achieved through a **"Stacked Paper"** philosophy.

- **The Layering Principle:** To highlight a specific data point, do not lift it; instead, "sink" the surrounding environment by using `surface_container_high`.
- **Zero-Radius Mandate:** All containers use a `0px` to `2px` max radius. This sharpness communicates institutional stability.
- **The Ghost Border:** For form fields and interactive zones, use a bottom-border only (`outline_variant`) at `1px`. This mimics the look of a physical ledger or a high-end stationery set.

---

## 5. Components

### Buttons: The Action Bricks
- **Primary:** `primary` background, `on_primary` text. Rectangular (0px radius), 1.4rem padding (horizontal).
- **Secondary:** `surface_container_lowest` background, `outline` 1px border.
- **States:** Hover states should not change color, but rather shift the tonal weight (e.g., `primary` moves to `on_primary_fixed_variant`).

### Data Tables (The Core Component)
- **Header:** `label-sm` (Uppercase), `#999` text, bottom-border 1px `outline_variant` at 20% opacity.
- **Row:** No vertical lines. Use `spacing-4` (1.4rem) vertical padding. 
- **Hover:** Use `surface_container_low` to highlight the active row.

### Order Panel Card
- **Structure:** `surface_container_lowest` background. 
- **Input:** Bottom-border only. No background fill. `label-md` floating above the line.
- **Totalizer:** A dedicated `surface_container` section at the bottom of the card with `JetBrains Mono` for the final calculation.

### Filter Pills
- **Style:** Outlined (`outline-variant`), `0px` radius.
- **Active State:** Fill with `primary` and change text to `on_primary`. Avoid rounded "pill" shapes; maintain the "brick" aesthetic.

---

## 6. Do’s and Don’ts

### Do:
- **Use Intentional Asymmetry:** Align primary content to the left and metadata to the extreme right to create an editorial "spread" feel.
- **Embrace Whitespace:** If a layout feels crowded, increase padding using `spacing-8` (2.75rem) or `spacing-10` (3.5rem).
- **Monospace for Numbers:** Always use JetBrains Mono for figures. It ensures tabular alignment where numbers don't "jump" as they change.

### Don't:
- **No Gradients:** Never use a gradient to solve a contrast issue. Adjust the surface token instead.
- **No Rounded Corners:** Avoid any radius over `2px`. If the component looks "friendly," it’s likely off-brand. 
- **No Divider Lines:** In lists, use whitespace (`spacing-3`) to separate items. Only use a line (`outline_variant` at low opacity) if the data density is so high that legibility fails.
- **No Shadows:** We define space through color, not light simulation.