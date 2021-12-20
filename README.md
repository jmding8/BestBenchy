# BestBenchy
## The quest for a perfect benchy

An investigation of which slicer, hardware, and firmware changes do (and jsut as importnatly, do not) contribute to a higher quality Benchy.

# Conclusions
None yet, we're just getting started!

# Log

* 0007_cyl_mk3sProfile_2.4b4
    * Intent: reproduce "ghosting" in a cylinder
    * Result: Was not able to reproduce, seam insertions actually look really good
* 0006_3dbArchs_prusaMk3sProfile_2.4beta4_constPerimSpeed
    * Intent: from 0004, re-slice with the same perimeter and external perimeter speed. Currently, 45mm/s perimeter with 25mm/s external perimeter.
    * Why: pressure drop due to speed change may take time to re-stabilize, leading to "ghosting" behavior.
    * Result: "ghosting" still present.
* 0005_3dbArches_prusaMk3sProfile_2.4beta4_flowContinued: flow during travel move
    * Intent: from 0004, manual edit the gcode so that extrusion continues during the travel move from inner to outer perimeter, see if this improves the "ghosting" behavior
    * Cancelled, going to try 0006 first
* 0004_prusaMk3sProfile_2.4beta4_arches: Reslice in 2.4-beta4
    * Intent: 2.4-beta4 places the seam for the inner perimeters much closer to the seam for the outer perimeters, this may result in better flow re-stabilization post-seam. Let's see if this improves the "ghosting" behavior.
    * Result: No better
* 0003_prusaMk3sProfile_2.3_arches: Remove gap fill and top layers
    * Intent: take 0002, and remove gap infill and top layers, to see if it helps reduce the "ghosting" artifacts
    * Result: "ghosting" artifacts still present
    * "Ghosting" seems likely to be due to flow re-stabilization after seam insertion
* 0002_prusaMk3sProfile_2.3_arches: Reproduce "ghosting" artifacts
    * Intent: isolate top of arches, ensure that the "ghosting" artifacts are reproducable
    * Result: artifacts reproduced
* 0001_prusaMiniProfile_2.3: Initial starting point
    * Printer, Kingroon KP3s
        * Purchased in November 2020
        * Direct drive, with a common Mk8 style extruder and PTFE lined hotend
        * Cantilevered, moving y-bed, linear rails on XY, and mostly (thick) sheetmetal construction, a surprisingly rigid machine
        * Chosen for being the lowest cost printer available with Trinamic stepper drivers (TMC2225), which may have better microstepping precision than A4988 drivers
        * Modifications:
            * 40mm hotend cooling fan (stock 30mm fan is extremely loud)
            * 5015 based layer cooling fan (stock 30mm fan is extremely loud)
            * Marlin 2.0 (primarily to enable babystepping, very helpful for live adjusting initial layer height)
            * Octoprint (for wifi file transfer)
    * Slicer
        * Slicer: PrusaSlicer 2.3
        * Printer Settings: Original Prusa MINI & MINI+
            * Note, this profile sets maximum values for speed, acceleration, and jerk via GCode
        * Filament Settings: Prusament PLA
        * Print Settings: 0.20mm QUALITY @MINI
    * Filament
        * PolyMaker, Teal, PolyLite PLA
        * Teal helps improve the visibility of surface defects
        * PolyMaker is an established brand with a reputation to uphold, and will hopefully make a consitent product
        * No mention of filament dimensional accuracy from the manufacturer
    * Results
        * Pretty poor overall
        * Hull not very smooth
        * Stringing everywhere
        * Unexpected gaps in extrusion
        * "Ghosting" artifacts in the arch area
