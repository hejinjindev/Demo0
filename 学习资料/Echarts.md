Echarts(数据可视化插件)

1.Echarts五步骤：

​        1.1下载并引用echarts.js文件

​		1.2准备一个具有大小的Dom容器

​		1.3初始化echarts实例对象：echarts.init(dom容器)

​		1.4指定配置项和数据(option)

​		1.5将配置项设置给echarts实例对象：echarts实例对象.setOption(option)

2.

​		title：标题组件

​		legend:图例组件

​		toolbox：工具栏

​		xAxis(x轴)

​		xAxis(y轴)

​		tooltip:提示框组件

​		grid：绘图网格

​		color：线的颜色

​		series：系列列表

![image-20220128114347117](C:\Users\ROG\AppData\Roaming\Typora\typora-user-images\image-20220128114347117.png)

3.边框图片:border-image

​	使用场景:用于大小不一样但边框样式一致

​	边框图片语法：

​			border-image-source:用在边框的图片的路径(使用的那个图片)

​			border-image-slice:图片边框向内偏移(裁剪的尺寸，一定不加单位，上右下左)

​			border-image-width:图片边框的宽度(需要加单位)(不是边框的宽度指的是边框图片的宽度)

​        	border-image-repeat:图像边框是否应平铺(repeat),铺满（round）或**拉伸(stretch)默认是拉伸**

