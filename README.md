# ◈ Galaxy S22 Ultra

### An interactive 3D exploration of the Galaxy S22 Ultra.

A cinematic, scroll-driven WebGL experience that transforms the **Samsung Galaxy S22 Ultra** into an interactive 3D object.

Explore the phone from every angle, move from its front display to the camera system, reveal the built-in S Pen, and gradually dismantle the device to expose its internal architecture.

> **Turn it. Explore it. Take it apart.**

---

## ✦ The Experience

This project reimagines a traditional smartphone product page as an interactive 3D exhibition.

Rather than presenting specifications in cards and tables, information is revealed progressively as the device moves through a carefully choreographed sequence.

The experience combines:

* ◇ Real-time 3D rendering
* ◇ Scroll-driven animation
* ◇ Interactive device rotation
* ◇ Exploded-view hardware visualization
* ◇ S Pen disassembly
* ◇ Procedurally constructed internal components
* ◇ Cinematic lighting
* ◇ Responsive typography
* ◇ Touch and mouse interaction
* ◇ Keyboard controls
* ◇ Reduced-motion support

---

## ◇ Explore the Device

The experience follows a continuous visual journey:

```text
                  GALAXY S22 ULTRA
                         │
                         ▼
                  Front Display
                         │
                         ▼
                    Device Turn
                         │
                         ▼
                  Camera System
                         │
                         ▼
                    S Pen Reveal
                         │
                         ▼
                  Device Separation
                         │
                         ▼
                  Internal Hardware
                         │
                         ▼
                    S Pen Breakdown
                         │
                         ▼
                  Processor + Memory
                         │
                         ▼
                       Battery
                         │
                         ▼
                    Connectivity
                         │
                         ▼
                    Final Reveal
```

The phone gradually separates into layers, revealing the conceptual architecture hidden beneath its exterior.

---

## ◇ Specifications

The experience highlights the original Galaxy S22 Ultra's key specifications.

### Display

**6.8"**

Dynamic AMOLED 2X

**3088 × 1440**

QHD+ resolution

**120 Hz**

Adaptive refresh rate

**1,750 nits**

Peak brightness

**HDR10+**

High dynamic range

---

### Camera

**108 MP**

Main camera

**12 MP**

Ultra-wide

**10 MP**

3× optical telephoto

**10 MP**

10× optical telephoto

**100×**

Maximum Space Zoom

**8K / 24 fps**

Maximum video recording

---

### S Pen

The S22 Ultra's defining feature is its integrated S Pen.

The experience explores:

* Built-in S Pen storage
* Low-latency input
* Bluetooth connectivity
* Air Actions
* Screen-Off Memo
* Samsung Notes
* Smart Select
* Translation
* Screenshot Writing
* Remote camera shutter

The pen itself can also be broken down into individual conceptual components.

---

### Performance

**Snapdragon 8 Gen 1**

or

**Exynos 2200**

Both processors are based on a 4 nm process.

Memory configurations include:

```text
8 GB RAM
12 GB RAM
```

Storage options extend from:

```text
128 GB
256 GB
512 GB
1 TB
```

---

### Battery

**5,000 mAh**

with support for:

**45 W**

wired charging

**15 W**

wireless charging

**Wireless PowerShare**

for charging compatible devices from the back of the phone.

---

### Connectivity

The device experience highlights:

* 5G
* Wi-Fi 6E
* Bluetooth 5.2
* Ultra Wideband
* USB-C 3.2
* Samsung DeX

---

## ◇ 3D Technology

The experience is powered by **Three.js** and WebGL.

### Core Stack

| Technology       | Role                      |
| ---------------- | ------------------------- |
| **Three.js**     | 3D scene and rendering    |
| **WebGL**        | GPU-accelerated graphics  |
| **GLTF / GLB**   | 3D model loading          |
| **JavaScript**   | Animation and interaction |
| **HTML5**        | Document structure        |
| **CSS3**         | Layout and visual system  |
| **Google Fonts** | Typography                |

---

## ◇ Rendering

The scene uses a physically-inspired rendering setup with:

* `WebGLRenderer`
* `GLTFLoader`
* `RoomEnvironment`
* ACES Filmic Tone Mapping
* HDR-style environment lighting
* Directional key lighting
* Rim lighting
* Fill lighting
* Physically-based materials

The renderer is also capped at a device pixel ratio of `2` to prevent unnecessarily expensive rendering on high-density displays.

---

## ◇ Interactive 3D Model

The primary device model is:

```text
assets/
└── samsung_galaxy_s22_ultra.glb
```

The model is loaded dynamically through Three.js.

The project also includes a JavaScript representation of the model for environments where the embedded asset is preferred:

```text
assets/
└── s22_ultra_b64.js
```

This allows the main experience to remain functional even when the external GLB asset is not used.

---

## ◇ Exploded View

One of the central visual elements is the device teardown.

The project defines individual displacement vectors for components:

```javascript
const OFF = {
    Display_ActiveArea: [0, 0, .95],
    Bezel: [0, 0, .7],
    Rearcase: [0, 0, 0],
    Back_Cover_Glass: [0, 0, -.58],
    Cam_Body: [0, 0, -.95],
    Cam_lens: [0, 0, -1.08],
    Usb_1: [0, -.7, 0],
    Usb_2: [0, -1, 0],
    Pen_Button: [0, 0, .5],
    Pen_Top: [0, -.55, 0],
    Pen_Cap: [0, -1.05, 0]
};
```

This allows the individual pieces to move away from the central device while maintaining their relative position.

---

## ◇ Procedural Internals

The original exterior model does not contain every internal component needed for the teardown sequence.

Instead, additional hardware is constructed programmatically using Three.js primitives.

The conceptual internals include:

* Logic board
* Processor
* Memory
* Battery
* Wireless charging coil
* Camera modules
* Speakers
* Haptic hardware
* Connectors
* Hinge-like structural elements
* Internal electronics

Custom canvas-generated textures are also used to create believable surfaces for components such as:

```text
Logic Board
Processor
Battery
Electronic Components
```

This creates the impression of a complete internal engineering visualization without requiring a fully modeled teardown asset.

---

## ◇ Interaction

### Scroll

The entire product story is controlled by vertical scrolling.

The page intentionally uses an extended scroll surface:

```css
#scroll {
    height: 1100vh;
}
```

Scroll progress is mapped to the 3D animation timeline.

---

### Mouse

Click and drag horizontally across the device to rotate it.

```text
← Drag ───────────────→
```

The rotation is continuous and designed to feel like physically turning the phone in your hand.

---

### Touch

On mobile:

```text
Swipe ← →
```

to rotate the device.

The canvas uses:

```css
touch-action: pan-y;
```

so vertical scrolling remains natural while horizontal gestures control the device.

---

### Keyboard

The device can also be rotated using:

```text
← Left Arrow
Right Arrow →
```

---

## ◇ Motion Design

The project uses smooth interpolation rather than abrupt transitions.

Animation stages use easing functions including:

**Smoothstep**

```javascript
x * x * (3 - 2 * x)
```

and

**Smootherstep**

```javascript
x * x * x * (x * (x * 6 - 15) + 10)
```

This gives the device movement:

* Smooth acceleration
* Smooth deceleration
* No sudden jumps
* Natural component separation
* Cinematic transitions

---

## ◇ Visual Language

The interface intentionally avoids traditional product-page UI.

There are:

* No conventional cards
* No large navigation menus
* No dense specification grids
* No dashboard-style components

Instead, the experience uses a minimal editorial composition.

### Typography

**Cormorant Garamond**

Used for:

* Product titles
* Large specifications
* Editorial headlines
* Hero messaging

**Jost**

Used for:

* Supporting information
* Technical descriptions
* Interaction hints
* UI text

---

## ◇ Atmosphere

The visual environment is built around a dark cinematic palette.

The background uses a subtle radial gradient:

```text
Deep indigo
     ↓
Muted violet
     ↓
Near-black
```

The device is illuminated using multiple directional sources to create controlled reflections across its glass and metal surfaces.

The result is closer to a **premium hardware film** than a conventional website.

---

## ◇ Responsive Experience

The layout adapts to:

* Desktop
* Laptop
* Tablet
* Mobile
* Portrait screens
* Landscape phones
* Narrow windows
* High-resolution displays

On smaller screens, the information panels move below the device so that the 3D model remains the visual focus.

---

## ◇ Accessibility

The experience respects the user's motion preference:

```css
prefers-reduced-motion
```

The WebGL canvas also exposes an accessible description:

```text
Interactive 3D Samsung Galaxy S22 Ultra with S Pen.
Drag to rotate.
```

This provides a basic accessible description of the primary interactive element.

---

## ◇ Project Structure

```text
galaxy-s22-ultra-site/
│
├── index.html
├── README.md
│
└── assets/
    │
    ├── samsung_galaxy_s22_ultra.glb
    │
    └── s22_ultra_b64.js
```

---

## ◇ Run Locally

The project can be opened directly in a modern browser because the 3D model can be embedded through the provided JavaScript asset.

For the recommended development workflow, run a local HTTP server.

### Python

```bash
python3 -m http.server 8000
```

### Windows

```powershell
py -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

---

## ◇ Browser Requirements

Recommended:

* Chrome
* Edge
* Firefox
* Safari

A browser with modern WebGL / WebGL2 support is recommended for the best experience.

A dedicated GPU or modern integrated graphics will provide smoother 3D rendering.

---

## ◇ Original Device

The project visualizes the:

**Samsung Galaxy S22 Ultra**

Released:

**February 25, 2022**

The experience references the original device's major hardware characteristics, including its integrated S Pen, camera system, AMOLED display, processor variants and battery.

---

## ◇ 3D Model Attribution

The 3D model used in this project is:

**"Samsung Galaxy S22 Ultra" by DatSketch**

Source:

https://sketchfab.com/DatSketch

License:

**CC BY-NC 4.0**

The model is used under its non-commercial Creative Commons license and requires attribution to the original creator.

---

## ◇ Disclaimer

This repository is an **independent interactive visualization project**.

It is not affiliated with, sponsored by, or endorsed by Samsung Electronics.

**Samsung**, **Galaxy**, **Galaxy S22 Ultra**, **S Pen**, **Samsung DeX**, and related trademarks belong to their respective owners.

Product specifications are presented for visualization and educational purposes.

---

## ◇ Why This Project?

Most product pages tell you what a device can do.

This project asks a different question:

> **What if you could experience how the device is built?**

The goal was to combine:

**Product design**

×
**3D graphics**

×
**Interaction design**

×
**Engineering visualization**

×
**Editorial storytelling**

into a single continuous experience.

---

<div align="center">

# GALAXY S22 ULTRA

### An interactive study of form, hardware & engineering.

**Three.js · WebGL · JavaScript**

◇

**Designed & developed by Ahanaf Mokammel Omi**

</div>
