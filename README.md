# Heatbed Soak Macro for Klipper 3D Printers

### What it does

It is well known that the print bed on 3D Printers can continue to flex and move even after the thermister reports that the print bed has reached its target temperature.
This issue becomes more prevalent the larger a print bed is.
This movement can cause any bed levelling mesh routine to measure a values that will subsequently change after it was measured, leading to poor first layer print quality.
This macro takes note of how long it takes for a print bed to reach a target temperature and will then wait for as long again plus two more minutes, to ensure that the print bed's temperature has fully equalised.
If the print-bed was already pre-warmed then this macro will still wait for at least 2 minutes to attempt to ensure temperature equalisation.
At all times the time spent waiting and the time remaining is reported back to the printer's UI console.

In general, use of this macro will result in vastly improved first layer quality on printers with print beds much larger than 200x200mm in size.

## How to install

To use this macro, import the [Heatbed_Soak.cfg](https://github.com/stew675/heatbed-soak-macro/blob/main/Heatbed_Soak.cfg) file from this repository into your printer's configuration directory

Now edit your `printer.cfg` and include the path to the `Heatbed_Soak.cfg` macro file

For example:

```
[include Heatbed_Soak.cfg]
```

The above assumes that the `Heatbed_Soak.cfg` file was placed in the same directory as your `printer.cfg` file.

## How to Use

Inside your slicer there will be a printer configuration panel which defines the Gcode that the printer will
run when starting a print.

You will want add the following `HEAT_SOAK` line, preferably just before the first line that has a `G28` command on it.

For example:

```
...
HEAT_SOAK TARGET=[first_layer_bed_temperature]
G28
...
```

If you see any `M140` or `M190` commands, these can be safely commented out by placing a `;` in front of those lines.

For example:

```
;M190 S[first_layer_bed_temperature]
```
