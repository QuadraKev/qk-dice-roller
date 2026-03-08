# QK Dice Roller - iCUE Dashboard Widget

The QuadraKev Dice Roller (QK Dice Roller) is an interactive dice rolling widget for the **Corsair Xeneon Edge** touchscreen display, built for iCUE's LCD widget system. Tap to roll any standard polyhedral die, with spinning 3D wireframe dice and roll history tracking.

---

## How It Works

The widget runs entirely within iCUE with no external server or dependencies. Tap the dice area to roll. Results are displayed with a rolling animation, and previous rolls are tracked in a history panel.

Supports all standard RPG polyhedral dice: d4, d6, d8, d10, d12, d20, and d100. Roll up to 10 dice at once with individual results and totals displayed.

### In-Widget Controls

The dice type and count can be changed directly on the widget using +/- buttons arranged in standard dice notation format: `[-] 1 [+] d [-] 20 [+]`. The left control adjusts how many dice to roll (1-10), and the right control cycles through dice types (d4 through d100). No need to open iCUE settings to change dice configuration.

### 3D Wireframe Dice Backdrop

A spinning wireframe of the current die type is displayed behind the result number. For d4, d6, d8, d10, d12, and d20, live 3D wireframe projections of the actual polyhedra rotate in the background -- tetrahedron, cube, octahedron, pentagonal trapezohedron, dodecahedron, and icosahedron respectively. The d100 uses a static overlapping-circles shape.

Technical details:
- **Orthographic projection** with backface culling via Newell's method for normal calculation
- **3D tumbling** -- angular velocity is a 3D vector with random axis drift each frame, producing realistic tumbling motion rather than single-axis rotation
- **Roll animation** -- tapping to roll spins the backdrop dice at 60 rad/s with exponential deceleration back to the idle speed of 0.3 rad/s
- **Fixed-scale rendering** -- dice are projected at a fixed scale based on their circumradius, preventing visual "squishing" during rotation
- **d10 geometry** -- mathematically derived planar kite faces with 90-degree side angles, computed from the constraint d/H = (1-cos36)/(1+cos36)
- **Multi-dice grid** -- when rolling multiple dice, wireframes are arranged in a CSS grid layout (e.g., 3x3 for 9 dice)

All shapes use the accent color at low opacity. Original viewing angles inspired by Noun Project dice by Fritz Duggan (CC BY 3.0).

---

## Requirements

- Corsair iCUE (built and tested on 5.41.42)
- Corsair Xeneon Edge (or compatible dashboard LCD display with touchscreen)

---

## Setup

**1. Install the widget in iCUE:**

- Copy the project folder into your iCUE widgets directory
  - Typically `C:\Program Files\Corsair\Corsair iCUE5 Software\widgets`
  - `QKDiceRoller.html`, `QKDiceRoller_translation.json` should be added to `\widgets`
  - `images\qk-dice-roller.svg` should be added to the `widgets\images` folder
- Add the widget to your Xeneon Edge dashboard in iCUE

**2. Roll dice** by tapping anywhere on the widget.

---

## Settings

| Setting | Description |
|---------|-------------|
| **Dice Type** | Default polyhedral die (d4-d100). Also adjustable in-widget via +/- buttons. |
| **Number of Dice** | Default dice count (1-10). Also adjustable in-widget via +/- buttons. |
| **Show History** | Toggle the roll history panel |
| **Text Color** | Color for result numbers and text |
| **Accent Color** | Color for the dice wireframe, type label, and history headers |
| **Background Color** | Widget background color |
| **Transparency** | Background transparency |

---

## Layout

The widget adapts to all Xeneon Edge dashboard slot sizes:

- **S slot** (840x344) -- history panel is hidden to maximize dice area; controls and result are scaled up to match the physical size of larger slots
- **M slot** (840x696) -- dice result and controls centered, history scrolls horizontally below
- **L slot** (1688x696) -- dice result on the left, history panel on the right
- **XL slot** (2536x696) -- same as L with more horizontal space
- **Portrait layouts** (vertical orientation) -- dice result on top, history list below

When rolling multiple dice, individual results are shown below the total in brackets (e.g., [4, 8, 5]).

---

## Troubleshooting

**Widget doesn't respond to taps**
- Make sure you're using a touchscreen-equipped display (Xeneon Edge)
- The widget requires the `x-icue-interactive` flag which is included

**Results seem non-random**
- The widget uses JavaScript's built-in `Math.random()` which provides adequate randomness for casual use
- This is not intended for cryptographically secure random number generation
