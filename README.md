# Lily58 Wireless ZMK Configuration

This repository contains a custom **ZMK firmware configuration** for a **Lily58 wireless split keyboard**
using **Nice!Nano v2** controllers.

It is designed to be simple, reproducible, and easy to flash using **prebuilt UF2 files**
generated automatically by **GitHub Actions**.

---

## Repository Purpose

This repository allows you to:

- Build firmware for a **wireless Lily58**
- Flash firmware **without installing ZMK locally**
- Reset Bluetooth pairings safely
- Flash left and right halves independently
- Avoid common pairing and flashing issues

---

## Repository Structure

```
.
├── config/
│   ├── lily58.conf        # General ZMK configuration (Bluetooth, display, power)
│   ├── lily58.keymap      # Keymap, layers, encoders
│   └── west.yml
│
├── .github/
│   └── workflows/
│       └── build.yml     # CI workflow that builds the firmware
│
├── build.yaml            # Build matrix for GitHub Actions
└── README.md             # Documentation
```

### File Overview

- **lily58.conf**  
  Global ZMK options (Bluetooth, display, power management).

- **lily58.keymap**  
  Keyboard layout, layers, encoder rotation and encoder button behavior.

- **build.yaml / build.yml**  
  Define how GitHub Actions builds firmware for left and right halves.

---

## Firmware Files

After a successful GitHub Actions build, you will download **three UF2 files**:

1. **settings_reset-nice_nano_v2-zmk.uf2**  
   Clears all Bluetooth pairings and stored settings.

2. **lily58_left-nice_nano_v2-zmk.uf2**  
   Firmware for the **left half**.

3. **lily58_right-nice_nano_v2-zmk.uf2**  
   Firmware for the **right half**.

---

## Flashing Instructions (Step by Step)

### Requirements

- USB cable
- Any OS (Windows, macOS, Linux)
- Nice!Nano v2 installed on both halves

---

### Step 1: Enter Bootloader Mode

For each half of the keyboard:

1. Press the **RESET button twice quickly**
2. A removable USB drive will appear

---

### Step 2: Flash the Settings Reset Firmware

This step is **required** and prevents pairing issues.

1. Drag and drop  
   `settings_reset-nice_nano_v2-zmk.uf2`
   into the bootloader drive
2. The drive will close automatically
3. The controller reboots

---

### Step 3: Flash the Keyboard Firmware

Repeat separately for each half.

#### Left Half

1. Press RESET **twice quickly**
2. Drag and drop  
   `lily58_left-nice_nano_v2-zmk.uf2`

#### Right Half

1. Press RESET **twice quickly**
2. Drag and drop  
   `lily58_right-nice_nano_v2-zmk.uf2`

Each time, the drive will close automatically.

---

## Recommended Flashing Order

1. settings_reset → left half  
2. settings_reset → right half  
3. lily58_left → left half  
4. lily58_right → right half  

---

## Bluetooth Pairing Issues

If the halves do not pair correctly:

1. Press and hold **RESET on both halves at the same time**
2. Hold for **~10 seconds**
3. Release both buttons

The halves should re-pair automatically.

---

## Encoder Notes

- Encoder **rotation** is defined in `sensor-bindings`
- Encoder **clicks** are treated as normal keys
- Encoder positions are fixed by the Lily58 matrix
- No additional steps are required during flashing

---

## Troubleshooting

- **No bootloader drive appears**  
  → Press RESET twice quickly

- **Halves do not connect**  
  → Perform the 10-second dual reset

- **Wrong layout**  
  → Ensure correct firmware was flashed to each half

---

## License

Based on **ZMK Firmware**  
Licensed under the **MIT License**
