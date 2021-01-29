## Quick Notes on Grids

For each grid, there are 3 files:
* `.png`: the bitmap image of the grid.
* `.svg`: the vector source image of the grid. You can opem this with Inkscape and make changes as needed.
Finally use the LaserPecker Gcode extension to generate a Gcode file. 
* `.txt`: ready made Gcode file with hard-coded power/speed setting that should work on most materials.

Grid 1

<img src="resources/grid_1.png" width="200px">

Grid 2

<img src="resources/grid_2.png" width="200px">

Grid 3

<img src="resources/grid_3.png" width="200px">

## [See here for instructions on how to send Gcode files to your LP app](https://github.com/yy502/inkscape-laserpecker#sending-gcode-files-to-app)

Don't worry if you don't follow it, or just want some very quick grid as long as it's helpful. Do the following with grid 1 or 2:
* Save the `.png` grid image to your phone
* Open it in LP app as a normal image
* **Switch to Gcode mode**. Due to edge detection algorithm, each line in the image becomes double lines. i.e. **-** become `=`.
Just proceed and engrave the converted double line grid. Although this will take twice the time than using the ready-made Gcode file,
it is still `A LOT` faster than engraving this grid in Bin mode, and most importantly the outcome still serves its purpose.

**Note: due to the complexity of grid 3, I do not recommend using this method with it.**
