# BestBenchy
## The quest for a perfect benchy

An investigation of which slicer, hardware, and firmware changes do (and jsut as importnatly, do not) contribute to a higher quality Benchy.

# Conclusions
None yet, we're just getting started!

# Log

* 0001_prusaMiniProfile_2.4.0-beta4: Updating PrusaSlicer
    * Among other changes, it looks like PrusaSlicer 2.4.0-beta4 changes how inner perimeters transition to outer perimeters
    * Hopefully this will reduce the distance of the travel move between inner and outer perimeters, resulting in less significant extrusion flow interruption and reduced seams
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
        * ...
