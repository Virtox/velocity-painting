# This version is still work in progress

Changes:
The original script was not working for my printers and the detail I had in mind.
On one printer, during the faster moves, the extruder tried to keep up and started to miss steps, on another the extruder kept up and the result was poor/invisible. Increasing speeds reduced the quality too much.
So, I think an improvement for the velocity painting is to keep constant input pressure on the nozzle instead of relying on the fact the extruder can't keep up or just misses steps.
- Modified the extrusion amount to counteract the speed increase.
For example if the modulated speed doubles, the extrusion speed halves, resulting in the extruder motor running at the same speed during the whole print. New extrusion value stored in $newE etc.

- Changed spherical projection routine to Latitude Longitude form.
- Don't process lines when retracting

- Added a skip to z, so it will not process layers until this z.

- Added Getopt::Long for cleaner parameter parsing.

- Added a G92 parse to reset newE

- Print the parameters and gcode at the top of the Gcode file.

Still need to debug a little and clean up some more, but happy with the new results so far!
I have only use spherical projection so far, hope I did not break anything else.

# Velocity Painting

I'd love this to evolve into something cool. All I ask is that you use the term _Velocity Painting_, tag things with _#VelocityPainting_, and ack that I, Mark Wheadon, started this bizarre journey with the idea, the name, and some functional though fragile code ;-) See the licence at the bottom of this document.

If you improve this code then it would be great if you could submit a pull request back to the repository -- so others can benefit from the work.

## What's here

So, this is a rough and ready perl script that when given an image file and a GCODE file, processes the GCODE to change print speeds according to the intensity of the image pixels -- thus mapping the image onto the model. If a GCODE vector crosses a pattern boundary then the vector is split to allow a change in velocity to occur at that boundary.

An FAQ is [available here](https://github.com/MarkWheadon/velocity-painting/wiki/FAQ).

## In use

Slice your model with all speeds set to (say) 3000mm/min, then use the _3000_ as the first argument to the script. Don't forget to switch off
anything in the slicer that changes print speed according to layer time and anything that under-speeds infill, outer perimeters, bridges etc.
Note: At time of writing I have only run this code on the output from Simplify3D -- it hasn't been tried on output from Slic3r, Cura, etc.

Run the script with no arguments to get some usage instructions.

## Dependencies

The script relies on the _Imager_ perl module and _Math::Trig_.

## Important

Run the resulting GCODE though a GCODE previewer before sending it to a printer. *Especially* once you start to change the script.  Messing up the co-ordinates will send the print head places it should never go and that could easily damage your printer. I drag the GCODE onto Simplify3D to preview it -- Simplify3D even colour codes the print velocity, which is exactly what you need!

## Licence

Velocity Painting by [Mark Wheadon](https://github.com/MarkWheadon) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).  Based on a work at https://github.com/MarkWheadon/velocity-painting.

Mark Wheadon [Email _mark.wheadon_ at _the usual gmail domain_]
