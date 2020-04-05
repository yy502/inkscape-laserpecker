[中文介绍点此处](README_CN.md)

# LaserPecker Extension for Inkscape
This is a Gcode generator extension for Inkscape, tailored for LaserPecker laser engraver. The LaserPecker App has a built-in Gcode feature. This extension allows you to manually set power and speed beyond the App's limitations. (Hardware limitations still apply. Read on...)


## LaserPecker
LaserPecker is an affordable and portable cunsumer level laser engraver.
For more details, visit their official [English site](https://www.laserpecker.net/) or [Chinese site](http://www.laserpecker.cn/). 


## Compatibility

This extension has been tested with LaserPecker L1 (1st generation) and Pro version. There are 2nd and 3rd generations to be released soon, and I will keep updating this extension to support those.


## Installation

1) Install Inkscape 0.92. Inkscape 1.0 is not supported yet.
2) Copy **laserpecker.inx** and **laserpecker.py** from `extension` directory into...
	* For Linux and Mac: `~/.config/inkscape/extensions/`
	* For Windows: `C:\Program Files\Inkscape\share\extensions\`
3) Start Inkscape and you should be able to access the extension from "Extensions" > "LaserPecker" > "LaserPecker Gcode Generator" 


## Settings and Limitations

* Laser head idle movement speed is hard-coded to 3000mm/min, as this is what's used in LaserPecker's official sample Gcode files.
* Lowest laser speed is limited to 70mm/min as this is the lowest effective speed that LaserPecker allows. i.e. I tested speeds from 0.01 to 70 and they are all the same to LaserPecker.
* Laser power can be set from 1 (min) to 255 (max). (0=off, which makes the Gcode useless, so I disallowed it.)
* Engraving area is limited to 100mm x 100mm in size.
* This extension warns if the target graphics are larger than 100x100.
* The origin (0,0) is in the centre of the 100mm x 100mm engraving area. i.e. the absolute coordinates for this 100x100 area is from (-50,-50) to (50,50). Although LaserPecker L1 is capable of engraving a much larger area from (-100,-70) to (100,70), it is limited by the App and the machine to minimise distortion and ensure consistent engraving quality. See `engraving_over_200mm_x_140mm.mp4` and `engraving_over_200mm_x_140mm.jpg` in `misc` directory.
* The position of target graphics on Inkscape canvas is irrelevant. This extension will automatically offset X,Y coordinates, so that the resulting absolute Gcode coordinates are centred to the origin (0,0).  
* Output Gcode file should end in .txt. The extension does not normally matter, as it's just a plain text file, but here .txt is what's recognised as Gcode files by LaserPecker App (in Android at least).
* Output Gcode file should not exceed 1MB in size.


## Image to Gcode

1) Launch Inkscape.
2) Import an image, preferably a black and white image onto the blank canvas.
3) Select the image, then "Path" > "Trace Bitmap"
4) Use the following optimal settings:
	* Colours: 2
	* Scans: 2
	* Smooth: check
	* Stack scans: check
	* Remove background: check
	* Live Preview: check
	* the rest is up to you to poke around and figure out what's best for your image.
5) Click "OK" button **once** and close this pop up.
6) The vectorised image is stacked on top of your bitmap image. (Optional: Move it away, and then select and delete your bitmap image underneath to avoid confusion.)
7) It does not matter where you position the vectorised graphics, as long as its size is within 100mm x 100mm. Use the W and H values displayed in the tool bar to help scale your graphics.
8) Select all of your shapes if you have more than one. They do not have to be grouped. Now, just in case, double convert them to path from "Path" > "Object to Path".
9) "Extensions" > "LaserPecker" > "LaserPecker Gcode Generator" 
10) Fill in the values as prompted and click "Apply" to generator Gcode.



## Bonus: Inspect Generated Gcode

1) Open up the generated file with a text editor
2) Select all texts and copy
3) Open [NC Viewer](https://ncviewer.com/)
4) Clear the sample Gcode and paste your Gcode in
5) Click the blue "Plot" button to visualise your Gcode.


## Sample Images

I have included a few sample images for you to test convert to Gcode and engrave with LaserPecker. The reason why I did not include any sample Gcode is because you will need to choose the best settings (power,speed) for your material at the point of generation.


## Helper Files

In `gcode` directory, I have created some Gcode files to help you quickly test and find out the optimal power+speed settings for cutting or engraving your target material.

* `engraving_test_p160-255,s500-800.txt`: Sweep across different power and speeds with small step sizes to help you map different engraving results to accurate Gcode settings (power,speed). 
* `cutting_test_p200-255,s70-400.txt`: This helps you to find the lowest possible setting that your material can be cut with. If even the highest setting (p255,s70) is unable to cut your meterial, consider cutting multiple times.
* `sample_result.jpg`: Test results on a recycled paper. 

In `misc` directory, there are several sets of `markers` files. Each set has the following files:
* `.svg`: The SVG file of the markers. Open it with Inkscape and convert to Gcode with your choice of settings and test your LaserPecker's engravng distorsion and sizing.
* `.txt`: Gcode for the markers with speed=500 and power=200. This is MUCH faster than using a bitmap image to engrave the markers over the 100mm x 100mm area.
* `.png`: PNG image of the markers only for quick preview. I do not suggest engravng this as it's MUCH slower than using Gcode.


## Credit
This extension is based on [J Tech Laser Tool Plugin V 2_2 for inkscape 0.92](https://jtechphotonics.com/?page_id=1980) for laser engraving and cutting.


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
