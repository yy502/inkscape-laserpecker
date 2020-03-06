# LaserPecker Extension for Inkscape
This is a Gcode generator extension for Inkscape, tailored for LaserPecker laser engraver.

## LaserPecker
LaserPecker is an affordable and portable cunsumer level laser engraver.
For more details, visit their official [English site](https://www.laserpecker.net/) or [Chinese site](http://www.laserpecker.cn/). 

## Settings and Limitations

* Engraving area is limited to 100mm x 100mm in size.
* This extension warns if the target graphics are larger than 100x100.
* The origin (0,0) is in the centre of the 100mm x 100mm engraving area. i.e. the absolute coordinates for this 100x100 area is from (-50,-50) to (50,50). Although LaserPecker L1 is capable of engraving a much larger area from (-100,-70) to (100,70), it is limited by the App and the machine to minimise distortion and ensure consistent engraving quality.
* The position of target graphics on Inkscape canvas is irrelevant. This extension will automatically offset X,Y coordinates, so that the resulting absolute Gcode coordinates are centred to the origin (0,0).  
* Output Gcode file should end in .txt
* Output Gcode file should not exceed 1MB in size.



## Credit
This extension is based on [J Tech Laser Tool Plugin V 2_2 for inkscape 0.92](https://jtechphotonics.com/?page_id=1980) for laser engraving and cutting.
