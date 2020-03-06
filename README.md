# LaserPecker Extension for Inkscape
This is a Gcode generator extension for Inkscape, tailored for LaserPecker laser engraver.


## LaserPecker
LaserPecker is an affordable and portable cunsumer level laser engraver.
For more details, visit their official [English site](https://www.laserpecker.net/) or [Chinese site](http://www.laserpecker.cn/). 


## Installation

1) Install Inkscape 0.92. Inkscape 1.0 is not supported yet.
2) Copy **laserpecker.inx** and **laserpecker.py** into...
	* For Linux and Mac: `~/. config/inkscape/extensions/`
	* For Windows: `C:\Program Files\Inkscape\share\extensions\`
3) Start Inkscape and you should be able to access the extension from "Extensions" > "LaserPecker" > "LaserPecker Gcode Generator" 


## Settings and Limitations

* Laser head idle movement speed is hard-coded to 3000mm/min, as this is what's used in LaserPecker's official sample Gcode files.
* Laser power can be set from 0 (off) to 255 (max).
* Engraving area is limited to 100mm x 100mm in size.
* This extension warns if the target graphics are larger than 100x100.
* The origin (0,0) is in the centre of the 100mm x 100mm engraving area. i.e. the absolute coordinates for this 100x100 area is from (-50,-50) to (50,50). Although LaserPecker L1 is capable of engraving a much larger area from (-100,-70) to (100,70), it is limited by the App and the machine to minimise distortion and ensure consistent engraving quality.
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
6) The vectorised image is stacked on top of your bitmap image. Move it away and select and delete your bitmap image underneath.
7) It does not matter where you position the vectorised image, as long as its size is within 100x100. Use the W and H values displayed in the tool bar to help scale your graphics.
8) Select all of your shapes if you have more than one. They do not have to be grouped. Now, just in case, double convert them to path from "Path" > "Object to Path".
9) "Extensions" > "LaserPecker" > "LaserPecker Gcode Generator" 
10) Fill in the values as prompted and click "Apply" to generator Gcode.



## Bonus: Inspect Generated Gcode

1) Open up the generated file with a text editor
2) Select all texts and copy
3) Open [NC Viewer](https://ncviewer.com/)
4) Clear the sample Gcode and paste your Gcode in
5) Click the blue "Plot" button to visualise your Gcode.


## Credit
This extension is based on [J Tech Laser Tool Plugin V 2_2 for inkscape 0.92](https://jtechphotonics.com/?page_id=1980) for laser engraving and cutting.
