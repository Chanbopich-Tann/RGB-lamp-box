# 🏮 Smart RGB Lamp Box

An open-source, multi-functional ambient lighting system developed as an Integrated Semester Project at the **University of North Carolina at Charlotte (UNCC)**. The system merges digital fabrication (3D printing and laser cutting) with an embedded Arduino microcontroller to deliver dynamic lighting states and musical audio playback.

---

## 📸 Assembled Outcome

| Complete Assembly (Side View) | Top View (Custom Raster) | Bottom View (Mode Select Controls) |
| :---: | :---: | :---: |
| ![Assembled Lamp Side](docs/assembled_side.jpg) | ![Assembled Lamp Top](docs/assembled_top.jpg) | ![Assembled Lamp Bottom](docs/assembled_bottom.jpg) |

The lamp features an outer 3D-printed house frame/hanger designed to be ceiling-mounted via string or chain, which houses an inner laser-cut wooden cube that diffuses light through custom tree vector cutouts.

---

## 🛠️ Interactive Capabilities & Operating Modes

The system features four dedicated input switches corresponding to distinct operational states:

1. **Normal Mode (Switch 1):** Activates a continuous, single-colored internal LED array.
2. **Auto Mode (Switch 2):** Engages an analog photoresistor (LDR light sensor) to dynamically auto-adjust LED brightness based on ambient room light levels.
3. **RGB Mode (Switch 3):** Cycles through 7 distinct color states (Red, Green, Blue, Purple, Teal, Orange, White, and OFF) using software-debounced button presses[cite: 3].
4. **Music Mode (Switch 4):** Triggers an integrated piezo buzzer to play programmed melody sequences ("Jingle Bells")[cite: 3].

---

## 📐 Digital Fabrication Specifications

### 1. 3D Printed Frame / Hanger (Prusa i3 MK3)
Designed in **Fusion 360** and sliced with **PrusaSlicer**[cite: 3]:
* **Lamp Box Header (Roof):** Features a ceiling mounting aperture and an internal view port displaying personalized raster branding ("Tann's Lamp")[cite: 3].
* **Lamp Box Frame (Body):** Features five large circular view openings revealing the internal laser-cut tree patterns[cite: 3].
* **Lamp Box Bottom (Base):** Serves as the bottom closure while maintaining access to the mode selection switches[cite: 3].

### 2. Laser-Cut Enclosure (Mini Laser Cutter)
Designed in **Inkscape** and prepared in **Adobe Illustrator**[cite: 3]:
* **6-Sided Wooden Cube Box:** Uses a finger-jointed/notched box construction to hold the internal Arduino circuit and dual breadboards[cite: 3].
* **Tree Vector Cutouts:** Four side panels feature intricate tree patterns to diffuse internal light[cite: 3].
* **Custom Rastering & Switch Ports:** Includes top custom raster branding and bottom square cutouts housing the four tactical switch interfaces[cite: 3].

---

## ⚡ Circuit Diagram & Component List

![Tinkercad Schematic](docs/tinkercad_schematic.png)

### Hardware Components
* **Microcontroller:** Arduino Uno[cite: 3]
* **Inputs:** 4 Snap Switches/Push Buttons, Photoresistor (LDR Light Sensor)[cite: 3]
* **Outputs:** Single-colored LEDs, RGB LED, Piezo Speaker[cite: 3]
* **Power & Accessories:** Dual Breadboards, 5V Battery / Barrel Jack Cable, Current-Limiting Resistors, Jumper Wires[cite: 3]

---

## 💻 Firmware Implementation

The control logic (`/src/main.ino`) processes sensor feedback, tone synthesis, and software button debouncing[cite: 3]:

```cpp
// Auto Mode: Ambient light sensing & inverse PWM mapping
if (led2On) {
    val = analogRead(LIGHT);
    val = map(val, MIN_LIGHT, MAX_LIGHT, 255, 0);
    val = constrain(val, 0, 255);
    analogWrite(LED2, val);
}

// Software Button Debouncing Routine
boolean debounceButton(int buttonPin, boolean last) {
    boolean current = digitalRead(buttonPin);
    if (last != current) {
        delay(5);
        current = digitalRead(buttonPin);
    }
    return current;
}
