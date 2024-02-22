ESPHome replacement control board for Honeywell True HEPA Air Purifier.

![demo](docs/demo.m4v)

Designed to be compatible with HPA200. I expect it to also be compatible with
the HPA300 and HPA100. The specific design you see in this repo now has not
been tested, but is a product of correcting errors in the version I'm currently
using in my unit.

![control panel photo](./controls.jpg)

This is a replacement for EH-A-4200-C V1.00, designed 2012-10-12.

![board photo](./cropped.jpg)

## BOM

### Desoldered from original

- 7x touchpad springs
- 1x cable assembly

### Hand-soldered

- 1x [D1 mini ESP32](https://github.com/r0oland/ESP32_mini_KiCad_Library) (I used https://www.aliexpress.us/item/2251832671740023.html, "CH9102X drive")
- 1x 6.3V+, 100uF+, P=3.5mm through-hole capacitor (probably optional)
- 4x 10-pin 2.54mm headers. 2x of these generally come with your D1 mini ESP32 kit, and you can likely repurpose the long female headers from the kit as the other 2x.
- 7805-compatible buck regulator module (I used https://www.aliexpress.us/item/3256801422436146.html)

### SMD

- 5x 16V+, 1uF+, 0805 ceramic capacitor
- 10x SKC6812 LEDs
- 1x M7 SMA diode

## Installation

### Tools

1. T20 security bit, 2in long
2. Philips #2 screwdriver
3. Spudger or flathead screwdriver
4. Soldering iron
5. Soldering wick
6. Solder

### Procedure

#### Disassembly

1. Unplug the unit from the wall. If you do not do this, there is a high risk of electric shock.
1. Remove the filter grill from the front of the device by pressing it inwards
1. 6 screw holes will be revealed on the sides of the unit. 2 of the screws were T20 security screws, and the other 4 were #2 philips. Unscrew these screws.
1. The top of the unit still has four clips holding the front on. Use a spudger to release the top clips on the front side.
1. Remove the front panel of the unit.
1. 4 smaller philips screws will be revealed holding the top on. Unscrew these.
1. Use a spudger to release the top clips on the back side.
1. The top panel should easily come off.
1. Unscrew the screws holding the controls tray.
1. Unscrew the screws holding the control PCB.
1. Release the clips holding the control PCB in.
1. Unplug the control cable assembly from the power supply board.
1. Use the soldering iron and solder wick to remove the touchpad springs and the cable assembly.

#### Modifications

**Figure 1:**
![](docs/fig_1.jpg)

1. Flash the D1 mini ESP32 with ESPHome via the USB port. See the config at [hepa-filter.yaml](./hepa-filter.yaml) as a starting point.
1. Solder the touchpad springs on the top side of the replacement control board. This is the side of the control board with the LEDs.
1. Solder the cable assembly on the top side of the replacement control board.
1. Solder the D1 mini ESP32 on the reverse of the replacement control board, using the silk-screen outline as a guide.
1. De-solder Q1 from the power-supply board. Replace it with a 7805-compatible buck regulator. The output pin is the one closest to the connector. (see Fig 1, a)
1. Re-install the power supply board. Note that the screw is flat-tipped and shorter than the others (Fig 1, b)
1. Insert the board into the control panel, then use ESP32 Touch Pad's `setup_mode` to calibrate touch thresholds

#### Re-assembly

**Figure 2:**
![](docs/fig_3.jpg)

**Figure 3:**
![](docs/fig_3.jpg)

Reverse steps to re-assemble. Some notes:

1. Make sure the motor wires are coming out of the hole indicated in Fig 2, a
1. First screw the electronics box to the lid (Fig 2, b)
1. Then screw the lid onto the rest of the unit (Fig 2, c)
1. When snapping the front of the device on, make sure the plastic next to the handle (Fig 3, a) is correctly snapped in on both sides


## Software

See the config at [hepa-filter.yaml](./hepa-filter.yaml) as a starting point.

## Credits

- Thank you to [Keith Burzinski](https://github.com/kbx81) for reviewing my design through endless revisions!
