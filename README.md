# LaserPecker Extension for Inkscape Inkscape的激光啄木鸟插件
This is a Gcode generator extension for Inkscape, tailored for LaserPecker laser engraver.
这是一个为激光啄木鸟生成Gcode的Inkscape插件。

## LaserPecker 激光啄木鸟
LaserPecker is an affordable and portable cunsumer level laser engraver.
For more details, visit their official [English site](https://www.laserpecker.net/) or [Chinese site](http://www.laserpecker.cn/). 
激光啄木鸟是便宜好用的小型家用激光雕刻机器。具体信息请访问上面的官网链接。

## Installation 安装方法

1) Install Inkscape 0.92. Inkscape 1.0 is not supported yet.
2) Copy **laserpecker.inx** and **laserpecker.py** into...
	* For Linux and Mac: `~/.config/inkscape/extensions/`
	* For Windows: `C:\Program Files\Inkscape\share\extensions\`
3) Start Inkscape and you should be able to access the extension from "Extensions" > "LaserPecker" > "LaserPecker Gcode Generator" 

1) 安装Inkscape 0.92版。暂时还不支持1.0版。
2) 复制 **laserpecker.inx** 和 **laserpecker.py** 文件到...
	* Linux和Mac系统: `~/.config/inkscape/extensions/`
	* Windows系统: `C:\Program Files\Inkscape\share\extensions\`
3) 运行Inkscape，插件应该在"扩展"菜单下的"LaserPecker" > "LaserPecker Gcode Generator" 

## Settings and Limitations 设置和限制

* Laser head idle movement speed is hard-coded to 3000mm/min, as this is what's used in LaserPecker's official sample Gcode files.
* Laser power can be set from 0 (off) to 255 (max).
* Engraving area is limited to 100mm x 100mm in size.
* This extension warns if the target graphics are larger than 100x100.
* The origin (0,0) is in the centre of the 100mm x 100mm engraving area. i.e. the absolute coordinates for this 100x100 area is from (-50,-50) to (50,50). Although LaserPecker L1 is capable of engraving a much larger area from (-100,-70) to (100,70), it is limited by the App and the machine to minimise distortion and ensure consistent engraving quality.
* The position of target graphics on Inkscape canvas is irrelevant. This extension will automatically offset X,Y coordinates, so that the resulting absolute Gcode coordinates are centred to the origin (0,0).  
* Output Gcode file should end in .txt. The extension does not normally matter, as it's just a plain text file, but here .txt is what's recognised as Gcode files by LaserPecker App (in Android at least).
* Output Gcode file should not exceed 1MB in size.
* 激光头空走速度固定设置为3000mm/分，因为这是官方示例Gcode文件里用的值.
* 激光功率可以设成0（关闭）到255（最大）之间.
* 雕刻区域限制在100mm x 100mm.
* 如果图形超过100mm x 100mm，插件会提示.
* 雕刻原点 (0,0) 在100mm x 100mm雕刻区域的中心。也就是说，有效的绝对雕刻坐标实际上是(-50,-50)到(50,50)这么个方形范围之内。虽然通过测试，我发现激光啄木鸟一代的实际雕刻范围在(-100,-70)到(100,70)这么大的范围，厂商还是限制了100x100这个保守的区域来减小形变，保证雕刻质量。
* 你在Inkscape的画布上可以随意放置图形。此插件在输出Gcode坐标的时候会自动修正到整体图形以原点为中心。  
* 输出的Gcode文件是纯文本文件。一般来说扩展名不重要。但要传给安卓app的话，需要用txt扩展名才能被app识别。
* 输出的Gcode文件体积不能超过1MB，否则机器内存不够。

## Image to Gcode 位图转Gcode操作流程

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

1) 运行Inkscape
2) 导入图像
3) 选中图像，点"Path"菜单，然后选"Trace Bitmap"
4) 推荐用以下设置（没有中文版，直接翻译了选项名称）:
	* 颜色: 2
	* 扫描次数: 2
	* 顺滑: 选中
	* 层叠扫描图层: 选中
	* 删除背景: 选中
	* 实时预览: 选中
	* 其他选项自己随便测试效果
5) 点"OK"按钮**一次**就好。然后关掉对话框。
6) 生成的矢量图现在重叠在你的位图上面。你可以吧矢量图移开一点，选中位图然后把它删掉，免得碍事。
7) 矢量图形放画布的什么位置不重要，只要尺寸在100mm x 100mm以内就行。工具栏有显示宽高尺寸。利用这个缩放到你需要的尺寸。
8) 选中你要雕刻的图形，从"Path"菜单中选"Object to Path"转换成路径。
9) "扩展"菜单 > "LaserPecker" > "LaserPecker Gcode Generator" 
10) 填入功率，速度，文件夹和文件名，点Apply生成Gcode文件。图形复杂的话可能会花几秒钟。之后会有重叠雕刻路径预览。不用管它。选中删掉也行。这个跟Gcode文件没关系了。


## Bonus: Inspect Generated Gcode 检测生成的Gcode

1) Open up the generated file with a text editor
2) Select all texts and copy
3) Open [NC Viewer](https://ncviewer.com/)
4) Clear the sample Gcode and paste your Gcode in
5) Click the blue "Plot" button to visualise your Gcode.

1) 打开Gcode文件
2) 复制所有内容
3) 访问[NC Viewer](https://ncviewer.com/)
4) 清除左边已经有的Gcode，把你的贴进去
5) 点下面的"Plot"按钮就可以看到Gcode路径了

## Sample Images

I have included a few sample images for you to test convert to Gcode and engrave with LaserPecker. The reason why I did not include any sample Gcode is because you will need to choose the best settings (power,speed) for your material at the point of generation.


## Useful Gcode Files 实用Gcode文件

In `gcode` directory, I have created some Gcode files to help you quickly test and find out the optimal power+speed settings for cutting or engraving your target material.

* `engraving_test_p160-255,s500-800.txt`: Sweep across different power and speeds with small step sizes to help you map different engraving results to accurate Gcode settings (power,speed). 
* `cutting_test_p200-255,s70-400.txt`: This helps you to find the lowest possible setting that your material can be cut with. If even the highest setting (p255,s70) is unable to cut your meterial, consider cutting multiple times.
* `sample_result.jpg`: Test results on a recycled paper. 


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
