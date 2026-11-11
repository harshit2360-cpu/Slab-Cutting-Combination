# Slab Combination & Costing Calculator

**Darla Exports — internal costing tool**

A single-file web calculator for working out how a granite block will be cut into slabs of different thicknesses, and what that combination costs, sells for, weighs and earns.

---

## Getting started

1. Open `Slab_Cutting_Combination.html` in any modern browser (Chrome, Edge, Firefox, Safari). Nothing needs to be installed.
2. The page opens with a worked example already filled in. Change any value and every result updates straight away.
3. Use **Print / Save as PDF** to keep a copy. Use **Reset to example** to go back to the default values.

> **Note:** Nothing you enter is saved. Closing or refreshing the page brings back the example values. Print or save a PDF of any combination you want to keep.

An internet connection is only needed for the fonts. Without one, the page still works and uses your system fonts.

---

## How to use it

### 1. Block & Order Details

| Field | What to enter |
|---|---|
| **Length (cm)** | Block length. This is one side of the slab face. |
| **Height (cm)** | Block height. This is the other side of the slab face. |
| **Width (cm)** | Block width. This is the side the saw cuts across, so it is shared out between the slab thicknesses. |
| **FX Rate (₹ per unit)** | Exchange rate used to convert sales value into rupees (for example, 94 ₹ per $). |
| **Block Cost / FOB (₹)** | Cost of the block itself. It is added to the factory cutting cost to get total cost. |
| **Saw loss per slab (cm)** | Material lost to the saw blade on each cut (kerf). |
| **Currency symbol** | Symbol shown for sales rates and sales value (default `$`). This changes the label only. The conversion comes from the FX rate. |
| **Granite shade** | Sets the density used for weight: Light (2700 kg/m³), Medium / Dark Grey (2900), Black (3100), or **Custom**. |
| **Custom density (kg/m³)** | Only appears when the shade is set to Custom. |
| **Container target (tons)** | Weight limit for the container. Leave it at 0 for no limit. |

The readout under the inputs shows the block volume (m³) and the face area of one slab (m²).

### 2. Thickness Combination

Each row is one slab thickness. For each row, choose a **Use** mode:

- **Not used**: the thickness is ignored.
- **Slab count**: cut a fixed number of slabs of this thickness. Enter the number in **Slab Count**.
- **Remaining width**: fill whatever width is left after the fixed-count rows with this thickness. **Only one row can use this mode.** If more than one is set, only the first is used and a warning appears.

For every row in use, enter:

- **Factory Rate (₹/sft)**: the factory's cutting/processing price per square foot.
- **Sales Rate ($/m²)**: your selling price per square metre, in the currency set above.

Use **+ Add thickness** to add a custom thickness (for example, 2.5 cm), and **×** to remove a row. The rows for 2–12 cm are set up by default.

### 3. Calculated Output

One line per thickness in use, showing width used, slab count, area (m² and sft), weight, purchase cost and sales value, with a totals row underneath.

### 4. Profit Summary

Total slabs, total area, approximate cargo weight (with % of container target), purchase cost, block cost, total cost, sales value (in both currencies), **profit** and **margin**. Profit and margin turn green when positive and red when negative. The cargo weight turns red if it goes over the container target.

---

## Formulas

| Quantity | Calculation |
|---|---|
| Slab face area (m²) | Length × Height ÷ 10,000 |
| Width used (fixed-count row) | Slab count × (thickness + saw loss) |
| Remaining width | Block width − total width used by fixed-count rows |
| Slabs (remaining-width row) | floor(remaining width ÷ (thickness + saw loss)), then capped by weight (see below) |
| Total m² | Slabs × slab face area |
| Total sft | Total m² × 10.764 |
| Weight (kg) | Total m² × (thickness ÷ 100) × density |
| Purchase cost (₹) | Factory rate × total sft |
| Sales value | Sales rate × total m² |
| Total cost (₹) | Purchase cost + block cost (FOB) |
| Sales in ₹ | Sales value × FX rate |
| Profit (₹) | Sales in ₹ − total cost |
| Margin | Profit ÷ sales in ₹ × 100 |

### Container weight cap

If a container target is set, the calculator first adds up the weight of all fixed-count slabs. Whatever weight is left in the target is the budget for the remaining-width thickness. That row gets **the smaller of** the slabs that fit the width and the slabs that fit the weight budget. When the weight limit is the deciding factor, a note says so, and some of the block width is left uncut.

---

## Worked example (default values)

Block 315 × 180 × 170 cm, saw loss 1 cm, light granite (2700 kg/m³), FX 94, block cost ₹78,000, container target 27.5 t.

| Thickness | Use | Slabs | m² | Weight (kg) | Purchase (₹) | Sales ($) |
|---|---|---|---|---|---|---|
| 3 cm | Remaining width | 37 | 209.79 | 16,992.99 | 9,52,838.87 | 13,006.98 |
| 5 cm | 2 slabs | 2 | 11.34 | 1,530.90 | 80,513.26 | 1,088.64 |
| 7 cm | 1 slab | 1 | 5.67 | 1,071.63 | 53,280.83 | 720.09 |
| **Total** | | **40** | **226.80** | **19,595.52** | **10,86,632.95** | **14,815.71** |

- Width: fixed rows use 2 × 6 + 1 × 8 = 20 cm. That leaves 150 cm, which gives 37 slabs of 3 cm (150 ÷ 4, rounded down).
- Cargo weight: 19.60 t, which is 71.3% of the 27.5 t target, so the weight cap does not apply.
- Total cost: ₹10,86,632.95 + ₹78,000 = **₹11,64,632.95**
- Sales in ₹: $14,815.71 × 94 = **₹13,92,676.74**
- **Profit: ₹2,28,043.79 · Margin: 16.4%**

---

## Warnings you may see

| Message | Meaning |
|---|---|
| *Combination uses X cm more than the block width* (red) | The fixed slab counts need more width than the block has. Reduce the counts. |
| *X cm of block width is not assigned to any thickness* | No row is set to Remaining width, so part of the block is not being used. |
| *Remaining-width slabs capped to stay within the container target* | The weight limit, not the block width, decided the slab count. |
| *Only one thickness can use "Remaining width"* | More than one row is set to Remaining width. Only the first one counts. |

---

## Things to keep in mind

- **Weights are approximate.** They are based on the chosen density and the slab volume only. Saw loss, packing and crates are not included.
- **The weight cap only applies to the Remaining-width row.** Fixed-count rows are always cut as entered, even if they go over the container target. The weight figure turns red when that happens.
- **Saw loss is counted once per slab**, including the last one.
- The **currency symbol is only a label**. Make sure the FX rate matches the currency your sales rates are in.
- Conversion used: **1 m² = 10.764 sft**.
- Printing hides the buttons, hints and formula notes so the PDF shows only the inputs and results.
