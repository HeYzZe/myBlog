# SVG基础

## svg适用范围

1. 直接写入html文件。

   ```html
   <!DOCTYPE html>
   <html>
   <head></head>
   <body>
   <svg
     id="mysvg"
     xmlns="http://www.w3.org/2000/svg"
     viewBox="0 0 800 600"
     preserveAspectRatio="xMidYMid meet">
     <circle id="mycircle" cx="400" cy="300" r="50" />
   </svg>
   </body>
   </html>
   ```


2. SVG 代码也可以写在一个独立文件中，然后用`<img>`、`<object>`、`<embed>`、`<iframe>`等标签插入网页。

   ```html
   <img src="circle.svg">
   <object id="object" data="circle.svg" type="image/svg+xml"></object>
   <embed id="embed" src="icon.svg" type="image/svg+xml">
   <iframe id="iframe" src="icon.svg"></iframe>
   ```

3. CSS 也可以使用 SVG 文件。

   ```css
   .logo {
     background: url(icon.svg);
   }
   ```

4. SVG 文件还可以转为 BASE64 编码，然后作为 Data URI 写入网页。

   ```html
   <img src="data:image/svg+xml;base64,[data]">
   ```

## 语法

1. `<svg>`标签

   包裹svg代码的根标签，**<svg>**的`width`属性和`height`属性，指定了 SVG 图像在 HTML 元素中所占据的宽度和高度。除了相对单位，也可以采用绝对单位（单位：像素）。如果不指定这两个属性，SVG 图像默认大小是300像素（宽） x 150像素（高）。

   如果只想展示 SVG 图像的一部分，就要指定`viewBox`属性。

   `<viewBox>`属性的值有四个数字，分别是左上角的横坐标和纵坐标、视口的宽度和高度。上面代码中，SVG 图像是100像素宽 x 100像素高，`viewBox`属性指定视口从`(50, 50)`这个点开始。所以，实际看到的是右下角的四分之一圆。

   注意，视口必须适配所在的空间。上面代码中，视口的大小是 50 x 50，由于 SVG 图像的大小是 100 x 100，所以视口会放大去适配 SVG 图像的大小，即放大了四倍。

   如果不指定`width`属性和`height`属性，只指定`viewBox`属性，则相当于只给定 SVG 图像的长宽比。这时，SVG 图像的默认大小将等于所在的 HTML 元素的大小。

   SVG 的 CSS 属性与网页元素有所不同。

   > - fill：填充色
   > - stroke：描边色
   > - stroke-width：边框宽度

2. `<circle>`圆形

   > ```html
   > <circle cx="90"  cy="50" r="25" class="red" />
   > ```
   >
   > 上面的代码定义了三个圆。`<circle>`标签的`cx`、`cy`、`r`属性分别为横坐标、纵坐标和半径，单位为像素。坐标都是相对于`<svg>`画布的左上角原点。`class`属性用来指定对应的 CSS 类。

3. `<line>`直线

   > ```html
   > <line x1="0" y1="0" x2="200" y2="0" style="stroke:rgb(0,0,0);stroke-width:5" />
   > ```
   >
   > 上面代码中，`<line>`标签的`x1`属性和`y1`属性，表示线段起点的横坐标和纵坐标；`x2`属性和`y2`属性，表示线段终点的横坐标和纵坐标；`style`属性表示线段的样式。

4. `<polyline>`折线

   > ```html
   > <polyline points="3,3 30,28 3,53" fill="none" stroke="black" />
   > ```
   >
   > `<polyline>`的`points`属性指定了每个端点的坐标，横坐标与纵坐标之间与逗号分隔，点与点之间用空格分隔。

5. `rect`矩形

   > ```html
   > <rect x="0" y="0" height="100" width="200" style="stroke: #70d5dd; fill: #dd524b" />
   > ```
   >
   > `<rect>`的`x`属性和`y`属性，指定了矩形左上角端点的横坐标和纵坐标；`width`属性和`height`属性指定了矩形的宽度和高度（单位像素）。

6. `<ellipse>`椭圆

   > ```html
   > <ellipse cx="60" cy="60" ry="40" rx="20" stroke="black" stroke-width="5" fill="silver"/>
   > ```
   >
   > `<ellipse>`的`cx`属性和`cy`属性，指定了椭圆中心的横坐标和纵坐标（单位像素）；`rx`属性和`ry`属性，指定了椭圆横向轴和纵向轴的半径（单位像素）。

7. `<polygon>`多边形

   > ```html
   > <polygon fill="green" stroke="orange" stroke-width="1" points="0,0 100,0 100,100 0,100 0,0"/>
   > ```
   >
   > `<polygon>`的`points`属性指定了每个端点的坐标，横坐标与纵坐标之间与逗号分隔，点与点之间用空格分隔。

8. `<path>`路径

   > ```html
   >  <path d="M51,25 A11,11 100 1,1 69,32 L51,48 Z" transform="rotate(0, 50, 50)" fill="#f33">
   > ```
   >
   > `<path>`的`d`属性表示绘制顺序，它的值是一个长字符串，每个字母表示一个绘制动作，后面跟着坐标。
   >
   > - M：移动到（moveto）
   > - A：画圆（x半径，y半径 0 1,1 结束横坐标，结束纵坐标）
   > - L：画直线到（lineto）
   > - Z：闭合路径

9. `<text>`文本

   > ```html
   > <text x="50" y="25">Hello World</text>
   > ```
   >
   > `<text>`的`x`属性和`y`属性，表示文本区块基线（baseline）起点的横坐标和纵坐标。文字的样式可以用`class`或`style`属性指定。

10. `<use>`复制

    > ```html
    > <circle id="myCircle" cx="5" cy="5" r="4"/>
    > <use href="#myCircle" x="10" y="0" fill="blue" />
    > ```
    >
    > `<use>`的`href`属性指定所要复制的节点，`x`属性和`y`属性是`<use>`左上角的坐标。另外，还可以指定`width`和`height`坐标。

11. `<g>`组

    > ```html
    > <g id="myCircle">
    >     <text x="25" y="20">圆形</text>
    >     <circle cx="50" cy="50" r="20"/>
    > </g>
    > ```

12. `<defs>`自定义块

    > ```html
    > <defs>
    >     <g id="myCircle">
    >         <text x="25" y="20">圆形</text>
    >         <circle cx="50" cy="50" r="20"/>
    >     </g>
    > </defs>
    > 
    > <use href="#myCircle" x="0" y="0" />
    > ```
    >
    > `<defs>`标签用于自定义形状，它内部的代码不会显示，仅供引用。

13. `<pattern>`自定义形状

    > ```html
    > <defs>
    >     <pattern id="dots" x="0" y="0" width="100" height="100" patternUnits="userSpaceOnUse">
    >         <circle fill="#bee9e8" cx="50" cy="50" r="35" />
    >     </pattern>
    > </defs>
    > <rect x="0" y="0" width="100%" height="100%" fill="url(#dots)" />
    > ```
    >
    > `<pattern>`标签用于自定义一个形状，该形状可以被引用来平铺一个区域。
    >
    > 上面代码中，`<pattern>`标签将一个圆形定义为`dots`模式。`patternUnits="userSpaceOnUse"`表示`<pattern>`的宽度和长度是实际的像素值。然后，指定这个模式去填充下面的矩形。
    >
    > ![1546573834460](C:\Users\my\AppData\Roaming\Typora\typora-user-images\1546573834460.png)

14. `<image>`插入图片

    > ```html
    > <image xlink:href="path/to/image.jpg"
    >     width="50%" height="50%"/>
    > ```
    >
    > 上面代码中，`<image>`的`xlink:href`属性表示图像的来源。

15. `<animate>`动画

    > ```html
    > <rect x="0" y="0" width="100" height="100" fill="#feac5e">
    >     <animate attributeName="x" from="0" to="500" dur="2s" repeatCount="indefinite" />
    > </rect>
    > ```
    >
    > 上面代码中，矩形会不断移动，产生动画效果。
    >
    > `<animate>`的属性含义如下。
    >
    > > - attributeName：发生动画效果的属性名。
    > > - from：单次动画的初始值。
    > > - to：单次动画的结束值。
    > > - dur：单次动画的持续时间。
    > > - repeatCount：动画的循环模式。
    >
    > 可以在多个属性上面定义动画。
    >
    > > ```markup
    > > <animate attributeName="x" from="0" to="500" dur="2s" repeatCount="indefinite" />
    > > <animate attributeName="width" to="500" dur="2s" repeatCount="indefinite" />
    > > ```

16. `<animateTransform>`transform动画

    > ```html
    > <rect x="250" y="250" width="50" height="50" fill="#4bc0c8">
    >     <animateTransform attributeName="transform" type="rotate" begin="0s" dur="10s" from="0 200 200" to="360 400 400" repeatCount="indefinite" />
    > </rect>
    > ```
    >
    > 上面代码中，`<animateTransform>`的效果为旋转（`rotate`），这时`from`和`to`属性值有三个数字，第一个数字是角度值，第二个值和第三个值是旋转中心的坐标。`from="0 200 200"`表示开始时，角度为0，围绕`(200, 200)`开始旋转；`to="360 400 400"`表示结束时，角度为360，围绕`(400, 400)`旋转。
    >
    > **<mark>注</mark>：`<animate>`标签对 CSS 的`transform`属性不起作用，如果需要变形，就要使用`<animateTransform>`标签。**

参考文档：

 	1. [SVG图像入门教程](http://www.ruanyifeng.com/blog/2018/08/svg.html)
 	2. [SVG](https://blog.csdn.net/qq_31792281/article/details/80161032)
 	3. [超级强大的SVG](https://www.zhangxinxu.com/wordpress/2014/08/so-powerful-svg-smil-animation/)

