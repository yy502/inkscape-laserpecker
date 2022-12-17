[中文介绍点此处](README_CN.md)

# LaserPecker Extension for Inkscape
This is a Gcode generator extension for Inkscape, that will generate Gcode compatible with LaserPecker engravers. The LaserPecker App already has a built-in Gcode converter with capability of line-filling, which is pretty easy to use. Please consider using the built-in Gcode mode first. 


## LaserPecker
LaserPecker is a brand of affordable and portable consumer level laser engravers.
For more details, visit their official [English site](https://www.laserpecker.net/) or [Chinese site](http://www.laserpecker.cn/).


## Compatibility

Before generating Gcode for LP, please select the correct model and firmware number.
* LP1 (v1.0.0-1.4.9)
* LP1 Pro (v2.0.0-2.4.9)
* LP1z (v2.5.0-2.6.9)
* LP1z Pro (v2.0.0-2.6.9)
* LP2 (v3.0.0-3.1.3)
* LP2 (v3.1.4-3.4.9)
* LP2 (v3.5.0-3.5.7)
* LP2 (v3.5.8-3.6.9)
* LP2 (v3.7.0-3.7.2)
* LP2 (v3.7.3-3.9.9)
* LP3 (v5.5.0.0-5.5.9.9)
* LP3 (v5.5.0-5.9.9)
* LP4 (v6.5.0-6.9.9)

## Installation

1) Install Inkscape v0.92 or newer and watch [this video](https://youtu.be/GIJdfuAoqFI?t=19) on how to download a file from GitHub.
2) Depending on your Inkscape version and operating system, download `laserpecker.inx` and `laserpecker.py` from [extension/](/extension/)`<your_inkscape_version>/` directory into...
	* For Linux: `~/.config/inkscape/extensions/`
		* Flatpak: `~/.var/app/org.inkscape.Inkscape/config/inkscape/extensions/`
	* For Mac: Launch Inkscape > `Preferences` > `System` > Look for `User extensions` > click `Open`
	* For Windows: `C:\Program Files\Inkscape\share\inkscape\extensions\`
3) Restart Inkscape and you should be able to access the extension from `Extensions` > `LaserPecker` > `Gcode Generator for L1/Pro/L2`


## Settings and Limitations

* Laser head idle movement speed is hard-coded to 6000mm/min.
  * Faster or slower than the engraver's top speed does not matter much. It does not affect engraving quality.
* 1st Gen LP Only:
  * The lowest laser speed is limited to 70mm/min, as this is the lowest **effective** speed that LaserPecker App allows. i.e. I tested speeds from 0.01mm/min to 70mm/min and they all came out the same on the engraver end.
  * Laser power can be set from 1 (min) to 255 (max). (0=off, which makes the Gcode useless, so I disallowed it.)

* Maximum engraving range depends on the model of your LP. It is noted in the dropdown list of the entension for your reference.
* This extension warns if the target graphics are larger than allowed engraving range, and you should scale it down and try again.
* The origin (X=0,Y=0) could be in the **centre** or **top-left** of the maximum engraving range depending on the model. This is taken care of by this entension. This is one of the reasons why a generic Gcode file may not work.
* The position of your graphics on Inkscape canvas is irrelevant. This extension will automatically center your graphics in the LP's engraving range for the best engraving quality.
* Output Gcode file should end in `.txt` otherwise the LaserPecker App won't recognise it.
* **Note**
  * Generated Gcode file should not exceed 1MB each for L1/Pro, or 4MB each for LP2. This is a hard limit by the engravers' physical memory.
  * You can use arbitrary settings for *power* and *speed* if you are generating Gcode for LP2 or newer LP engravers, because these settings will be overridden by the app's power and depth settings. For L1/Pro, choose your settings carefully at generation time as these can't be changed via the app.


## Image to Gcode

Click to watch video tutorial (using Inkscape 0.92 here, v1.x looks slightly different):

[![](https://img.youtube.com/vi/neA5kYvSX6w/0.jpg)](https://www.youtube.com/watch?v=neA5kYvSX6w)

1) Launch Inkscape.
2) Import an image, preferably a black and white image onto the blank canvas.
3) Select the image, then "Path" > "Trace Bitmap"
4) Use the following optimal settings (using Inkscape 0.92 here, v1.x is slightly different):
	* Inkscape v1.0/1.1: use "Multiple scans > Colours"
	* Colours: 2
	* Scans: 2
	* Remove background: check
	* Live Preview: check (Inkscape v1.x: click "Update" button to preview)
	* the rest is up to you to poke around and figure out what's best for your image.
5) Click "OK" button **once** and close this pop up.
6) The vectorised image is stacked on top of your bitmap image. (Optional: Move it away, and then select and delete your bitmap image underneath to avoid confusion.)
7) It does not matter where you position the vectorised graphics, as long as its size is within 100mm x 100mm. Use the W and H values displayed in the tool bar to help scale your graphics.
8) Select all of your shapes if you have more than one. They do not have to be grouped. Now, just in case, double convert them to path from "Path" > "Object to Path".
9) `Extensions` > `LaserPecker` > `LaserPecker Gcode Generator`
10) Fill in the values as prompted and click `Apply` to generator Gcode.
11) Ignore any warnings. The auto generated markers overlay on top of your graphics can be deleted.


## Filling Your Shapes With Lines

You may have noticed that only the edges of your graphic are converted to paths, and therefore to Gcode. While this is desireable in some situations, like for cutting shapes out of your materials, we sometimes want to fill the shapes so they look like the original image, not just a hollow trace.

Here is how:

* you need to download and install KM-Laser extension ([for Inkscape 0.92](https://github.com/KnoxMakers/KM-Laser/tree/pre_0.92), [for Inkscape 1.0](https://github.com/KnoxMakers/KM-Laser))
* and learn how to fill your shape with lines by watching this video tutorial:
[![](https://img.youtube.com/vi/2Ee6yDaLod4/0.jpg)](https://www.youtube.com/watch?v=2Ee6yDaLod4)

There are three options you can/should tweak:

* **Hatch spacing:** first to reduce your shape stroke thickness to very low, so you can see the paths clearly. Then enable live preview and try out different spacing for your desired effect.
* **Hatch angle:** commonly we use 0 or 45 degrees.
* **Crosshatch:** cross fill or one-way parallel fill. Note that cross fill is twice long as parallel fill.

It is that easy! After filling your shape, generate Gcode as you would and optionally inspect your Gcode (read the next section) before engraving.


## Convert B&W Images to Single Line Sketches

### Inkscape 0.92 users
1) follow this [guide (TL;DR part)](https://github.com/yy502/autotrace#tldr) to compile & install `autotrace` (linux-only I'm afraid).
2) Use the single-line command shown in the link above to convert your bitmap (png) image to svg
3) Use this Gcode extension to generate Gcode for LaserPecker.
	* Note that svg file generated by `autotrace` is using px as default unit, and there's **no need** to change it to mm before resizing your graphic. As long as the width x height numerical values are within 100x100, the Gcode entension will work and treat them as mm.
4) Note that you may see some warning messages during generation. As long as there's no error, you can ignore them. In the end, if you see some horrible overlay of arrows appear on top of your graphic, the Gcode is generated OK, and you can move or delete this layer as you wish.

### Inkscape 1.x users
see https://lp.systemd.one/how-to/inkscape-1-x-converting-bw-images-to-single-line-sketches-for-gcode-engraving/


## Optional: Inspect Generated Gcode

Click to watch video tutorial:

[![](https://img.youtube.com/vi/yJpaMI9OOb0/0.jpg)](https://www.youtube.com/watch?v=yJpaMI9OOb0)

1) Open up the generated file with a text editor
2) Select all texts and copy
3) Open [NC Viewer](https://ncviewer.com/)
4) Clear the sample Gcode and paste your Gcode in
5) Click the blue "Plot" button to visualise your Gcode.


## Sending Gcode Files to App

Once the `.txt` Gcode files are generated...

* **Android:** copy files to phone storage using USB cable, your favourite cloud sotrage app, email, FB Message, etc...... into `Download` directory for example. Then in LP app, go to `Examples > G-code` tab, click on the `+` symbol and add your Gcode file to the app. 
* **iOS:** ~copy your Gcode file to any Cloud drive, and **Open** or **Export** it on your iOS device. When prompted, choose **Open in** or **Save to** `Files` App, and then save it to `Laserpecker > matarialgcode` directory (yes, the directory name is misspelt by LP).~ (app has changed a lot and I don't have an iOS device, so this needs to be confirmed)

Finally, your Gcode file is available in LP App under `Examples > G-code` tab.

## Sample Images

I have included a few sample images for you to test convert to Gcode and engrave with LaserPecker. The reason why I did not include any sample Gcode is because you will need to choose the best settings (power,speed) for your material at the point of generation.


## Helper Files

**L1/Pro only:** In `testing` directory, I have created some Gcode files to help you quickly test and find out the optimal power+speed settings for cutting or engraving your target material.

* `engraving_test_p160-255,s500-800.txt`: Sweep across different power and speeds with small step sizes to help you map different engraving results to accurate Gcode settings (power,speed).
* `cutting_test_p200-255,s70-400.txt`: This helps you to find the lowest possible setting that your material can be cut with. If even the highest setting (p255,s70) is unable to cut your material, consider cutting multiple times.
* `sample_result.jpg`: Test results on a recycled paper.

In `resources` directory, there are several sets of `grid` files, aiming to help you position your object under the laser. Each set has the following files:
* `.svg`: The SVG file of the grid. Open it with Inkscape and convert to Gcode with your choice of settings and test your LaserPecker's engraving distortion and sizing.
* `.txt`: Gcode for the grid with speed=500 and power=200. This is MUCH faster than using a bitmap image to engrave the grid over the 100mm x 100mm area.
* `.png`: PNG image of the grid only for quick preview. I do not suggest engraving this as it's MUCH slower than using Gcode.


## Experimental Extension for L1

This extension helps you to utilise absolute Gcode coordinates and engrave over 200mm x 140mm area with L1 model.
However, the oversize engraving result has been inconsistent around the far ends. In my opinion it's not worth the hassle, so I have stopped working on this. There's a chance that LaserPecker will officially unlock this capability, if they manage to reduce distortion via their App.


## Credit
This extension is based on [J Tech Laser Tool Plugin V 2_2 for Inkscape](https://jtechphotonics.com/?page_id=1980) for laser engraving and cutting.


## License


This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
