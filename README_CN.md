# 激光啄木鸟Inkscape插件
这是一个为激光啄木鸟生成Gcode的Inkscape插件。

## 激光啄木鸟
激光啄木鸟是便宜好用的小型家用激光雕刻机器。具体信息请访问[官方网站](http://www.laserpecker.cn/)（[英文官网](https://www.laserpecker.net/)） 。

## 兼容性

中文版说明文档可能未被及时更新。请以英文版说明文档为准。

## 安装方法

1) 安装Inkscape 0.92或更新版。
2) 取决于你的Inkscape版本以及操作系统，复制`extension/<inkscape版本号>`文件夹中的`laserpecker.inx`和`laserpecker.py`两个文件到...
   * Linux: `~/.config/inkscape/extensions/`
     * Flatpak: `~/.var/app/org.inkscape.Inkscape/config/inkscape/extensions/`
   * MacOS: 运行Inkscape > `首选项` > `系统` > 找到`用户扩展`然后点击`打开`打开文件夹。
   * Windows: `C:\Program Files\Inkscape\share\inkscape\extensions\`
3) 重启Inkscape，插件应该在`扩展`菜单下的`LaserPecker` > `Gcode Generator for L1/Pro/LP2`

## 设置和限制

* 激光头空走速度固定设置为3000mm/分，因为这是官方示例Gcode文件里用的值.
* 最低激光速度限制在70mm/分，因为这是机器允许的最慢速度。 （我测试过从0.01到70mm/分之间的各种速度设置，到了激光啄木鸟输出的时候没有区别，都等同设成70mm/分。）
* 激光功率可以设成1（最小）到255（最大）之间。（0=关闭，这样设置的话Gcode等于没用，所以禁止设成0。）
* 雕刻区域限制在100mm x 100mm。
* 如果图形超过100mm x 100mm，插件会提示。
* 雕刻原点 (0,0) 在100mm x 100mm雕刻区域的中心。也就是说，有效的绝对雕刻坐标实际上是(-50,-50)到(50,50)这么个方形范围之内。虽然通过测试，我发现激光啄木鸟一代(不是Pro)的实际雕刻范围在(-100,-70)到(100,70)这么大的范围，厂商还是限制了100x100这个保守的区域来减小形变，保证雕刻质量。演示效果请参考`misc`文件夹中的`engraving_over_200mm_x_140mm.mp4`和`engraving_over_200mm_x_140mm.jpg`。
* 你在Inkscape的画布上可以随意放置图形。此插件在输出Gcode坐标的时候会自动修正到整体图形以原点为中心。
* 输出的Gcode文件是纯文本文件。一般来说扩展名不重要。但要传给安卓app的话，需要用txt扩展名才能被app识别。
* 特别说明
  * 给LP2使用的Gcode不需要在意功率和速度设置，因为实际雕刻时会使用手机app里的设置。只有给L1/Pro使用的Gcode需要预先设置，并且无法在手机app里修改。
  * 给L1/Pro输出的Gcode文件体积不能超过1MB，否则机器内存不够。给LP2使用的Gcode文件体积上限是4MB。

## 位图转Gcode操作流程

点击观看演示视频：

[![](https://img.youtube.com/vi/neA5kYvSX6w/0.jpg)](https://www.youtube.com/watch?v=neA5kYvSX6w)

1) 运行Inkscape
2) 导入图像
3) **选中**图像，点"路径"菜单，然后选"临摹位图轮廓"
4) 在“临摹位图轮廓”页面推荐用以下设置（以下以Inkscape 1.0为例描述，上面视频演示用的是0.92版，界面有少许不同）
   * 多次扫描 > 颜色
   * Scans(扫描次数/颜色数量): 2
   * 删除背景: 选中
   * 其他选项自己随便测试效果
   * 改变了设置后点“更新”按钮预览效果
5) 点"应用"按钮**一次**就好。然后关掉对话框。
6) 生成的矢量图现在重叠在你的位图上面。你可以把矢量图移开一点，选中位图然后把它删掉，免得碍事。
7) 矢量图形放画布的什么位置不重要，只要尺寸在100mm x 100mm以内就行。工具栏有显示宽高尺寸。利用这个缩放到你需要的尺寸。
8) 选中你要雕刻的图形，从"Path"菜单中选"Object to Path"转换成路径。
9) `扩展`菜单 > `LaserPecker` > `LaserPecker Gcode Generator`
10) 填入功率，速度，文件夹和文件名，点Apply生成Gcode文件。图形复杂的话可能会花几秒钟。如果弹出警告信息的话就忽略。之后会有重叠雕刻路径预览。不用管它，选中删掉也行。这个跟Gcode文件没关系了。

## 填充图形

你应该已经注意到了我们生成的Gcode是图形的外框。这个适用于切割，但是如果我们想要用Gcode来雕刻原始图像的话，就需要用到另外一个插件来用直线填充有色的图形部分了。

首先，下载并安装KM-Laser插件([for Inkscape 0.92](https://github.com/KnoxMakers/KM-Laser/tree/pre_0.92), [for Inkscape 1.0](https://github.com/KnoxMakers/KM-Laser))。注意`extensions`和`palettes`内的文件都要复制。然后观看这个演示视频学习怎么使用这个填充插件：

[![](https://img.youtube.com/vi/2Ee6yDaLod4/0.jpg)](https://www.youtube.com/watch?v=2Ee6yDaLod4)


这个填充插件有三个设置值得尝试：

* **Hatch spacing:** 首先把图形线条粗细减到非常细，便于查看路径。然后勾选实时预览，最后改变线间距并查看效果。
* **Hatch angle:** 一般用0度或者45度。
* **Crosshatch:** 交叉填充或者平行线填充。注意交叉填充的路径是平行填充的2倍，所以雕刻时间就是2倍。


## 将黑白图转换为单线骨架图

点击观看演示视频：

[![](https://img.youtube.com/vi/-6GmyB0oL9I/0.jpg)](https://www.youtube.com/watch?v=-6GmyB0oL9I)

### Inkscape 0.92 用户
1) 依照[此处说明(TL;DR部分)](https://github.com/yy502/autotrace#tldr)编译并安装`autotrace`工具。 (仅限Linux平台)
2) 使用以上说明中的命令将位图（推荐png格式）转换为svg矢量图。
3) 使用上面的Gcode插件为激光啄木鸟生成Gcode文件。
	* 注意在改变矢量图案尺寸的时候可以忽略`autotrace`默认的px（像素）单位，不需要改变成mm。所以长x宽的数字值在100x100范围以内就可以了。插件在转换Gcode的时候会默认以mm为单位。
4) 在生成Gcode的过程中可能会跳出一些警告信息，可以忽略。如果Gcode文件成功生成，你的图上会出现一层令人不安的巨大的箭头图案。你可以移动或删除这一图层，它只是显示激光所走的路径顺序。

### Inkscape 1.x 用户
1) autotrace工具已经内置! \o/
2) 运行Inkscape，把你要转换的图拖进去。暂时不需要担心图像尺寸。
3) 选中图案，从`Path`（路径？）菜单选择 `Trace Bitmap`。 在弹出窗口的下拉菜单中切换到 `Centerline tracing (autotrace)`模式。使用默认设置应该就可以了。最后点 `OK`按钮。
4) 生成的单线图案重叠在位图上方，不容易看到。你可以点选它并拖到空白处。
5) 保持选中生成的矢量线图，在工具栏上方锁定比例并且调整图案尺寸到不超过100x100mm。
6) 使用上面的Gcode插件为激光啄木鸟生成Gcode文件。
7) 在生成Gcode的过程中可能会跳出一些警告信息，可以忽略。如果Gcode文件成功生成，你的图上会出现一层令人不安的巨大的箭头图案。你可以移动或删除这一图层，它只是显示激光所走的路径顺序。

<img src="tutorial/centerline_01.png" width="800px">
<img src="tutorial/centerline_02.png" width="800px">


## 可选步骤：检测生成的Gcode

点击观看演示视频：

[![](https://img.youtube.com/vi/yJpaMI9OOb0/0.jpg)](https://www.youtube.com/watch?v=yJpaMI9OOb0)

1) 打开Gcode文件
2) 复制所有内容
3) 访问[NC Viewer](https://ncviewer.com/)
4) 清除左边已经有的示范Gcode，把你的Gcode贴进去
5) 点下面的"Plot"按钮就可以看到图形化的Gcode路径了。


## 传送Gcode文件到手机

Gcode文件生成以后，
* **安卓：** 通过USB线或网盘或其他你最喜爱的方法把Gcode文件传入手机，比如在Downlaod文件夹中。打开啄木鸟app，在Examples页面的G-code分页中可以点击`+`符号添加Gcode文件，然后就可以选择并雕刻了。
* **iOS：** ~通过任何网盘App上传Gcode文件，在iOS设备下载或导出Gcode文件，选择用**Files** App打开并保存到`Laserpecker > matarialgcode`文件夹中。~（过期信息。啄木鸟app已经多次更新，我没有iOS设备，所以无法提供准确信息。欢迎用户指正。）

## 例图

我在`sample_images`文件夹中存了一些适合切割的图片。我没有直接提供Gcode文件的原因，是想留给你在生成Gcode文件时可以选择最适合你的切割材料的设置的机会。


## 实用帮助文件

在`testing`文件夹中有两个Gcode文件，可以帮助你快速测试和找到最合适你的材料的雕刻或者切割的设置组合（功率+速度）。

* `engraving_test_p160-255,s500-800.txt`: 用不同的功率和速度扫灰度来测试雕刻效果。
* `cutting_test_p200-255,s70-400.txt`: 这个是给你测试切割设置组合的。如果连最高有效设置(功率255,速度70)都无法一次切割你的材料的话，就只能考虑切多次了。
* `sample_result.jpg`: 我自己用回收纸的测试结果。

在`resources`文件夹中有若干`grid`定位网格文件，每套定位网格文件包含以下格式：
* `.svg`: 定位网格SVG矢量文件，建议用Inkscape打开编辑。
* `.txt`: 定位网格Gcode文件，速度500,功率200。
* `.png`: 定位网格PNG格式位图。注意这只是为了方便预览定位网格图样。雕刻位图要远远慢于雕刻Gcode。


## 声明

这个插件是在[J Tech Laser Tool Plugin V 2_2 for Inkscape](https://jtechphotonics.com/?page_id=1980)的基础上为激光啄木鸟改进和优化的。


## 使用许可

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
