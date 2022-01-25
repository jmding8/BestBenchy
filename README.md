# BestBenchy
## The quest for a perfect benchy

An investigation of which slicer, hardware, and firmware changes do (and jsut as importnatly, do not) contribute to a higher quality Benchy.

# Conclusions
None yet, we're just getting started!

# Log

* 0020
    * Slicing: [0.20mm QUALITY @MK3, Skirt Height: 1] [Prusament PLA] [Original Mk3s, Wipe: Off, Z-hop: Off] [PrusaSlicer 2.4]
    * Mutators: None
    * Intent: see if disabling Z-hop elimiantes the top surface issues that disabling wipe produces. Without z-hop, maybe the nozzle irons the blob down?
    * Result:
        * top surface blobs mostly gone
        * less stringing overall
        * still some strings where travel moves dont travel over any printed areas
* 0019
    * Slicing: [0.20mm QUALITY @MK3, Skirt Height: 1] [Prusament PLA] [Original Mk3s, Wipe: Off] [PrusaSlicer 2.4]
    * Mutators: None
    * Intent: see if disabling wipe produces as good results as wipe + inwardWipeMutator
    * Result:
        * side surfaces look good, "ghosting" artifact is gone
        * top surfaces have issues, little blobs are left at the end of lines
* 0018
    * Slicing: [0.20mm QUALITY @MK3, Skirt Height: 1] [Prusament PLA] [Original Mk3s] [PrusaSlicer 2.4]
    * Mutators: InwardWipeMutator
    * Intent: validate that InwardWipeMutator produces a significantly better Benchy than base slicer profile 
    * Result: validated. However, the thick strings happened again, not sure why.
* 0017
    * Slicing: [0.20mm QUALITY @MK3, Top: 0, Bottom: 3, Skirt Height: 1, Gap Fill: false] [Prusament PLA] [Original Mk3s] [PrusaSlicer 2.4]
    * Mutators: InwardWipeMutator
    * Intent: confirm that InwardWipeMutator with gap fill enabled produces weird thick strings
    * Result: Weird thick strings not present, maybe it was just a transient issue?
* 0016
    * Intent: InwardWipeMutator on 0014, see if weird thick strings are due to gap fill somehow
    * Result: Very good print, no "ghosting" artifact, and very clean surfaces
* 0015_0002_inwardWipeMutator
    * Intent: modify 0020, force wipes to occur tracing the inner perimeter by using InwardWipeMutator
    * Result:
        * "ghosting" artiact is gone
        * weird thick strings, probably a bug in the mutator code
        * interior corner at the arch looks sharper than 0013
        * more surface blobs though
* 0014_3dbArches_2.4_mk3sNoWipeNoGap
    * Intent: using PrusaSlicer 2.4 presets for Mk3s and eliminating 1) wipe move and 2) gap fill, see if that removes the "ghosting" artifact
    * Result:
        * "ghosting" artiact is gone
        * seems like general extrusion consistency is a bit worse than 0002 though
* 0012_retractionTest_mk3s_2.4b4_wipeIn
    * Intent: starting with 0009, wipe to the inner perimeter to hide the wipe-blob
    * Result: 
* 0011_retractionTest_mk3s_2.4b4_noZHop
    * Intent: from 0010, no Z-hop, see if that contributes to the blob
    * Result: slightly better
* 0010_retractionTest_mk3s_2.4b4_longRetract
    * Intent: double retraction distance, see if that helps
    * Result: slightly better
* 0009_retractionTest_mk3s_2.4b4
    * Intent: fast retraction test to verify that the "ghosting" issue (hereby renamed wipe-blob issue) is reproduced
    * Result: reproduced as expected
        * 0008_3dbArchs_mk3s_2.4b4_extrudeTransitions
    * Intent: starting with 0004, add extrusions during the travel moves between the internal and external perimeters to see if holding constant flow during that transition will eliminate the "ghosting" issue
    * Result: From watching the print it became clear that the "ghosting" is actually due to the wipe! There is a slight blob where the wipe ends, which forms this "ghosting" artifact.
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
