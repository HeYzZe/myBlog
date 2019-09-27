# Macdown语法 #

## Macdown的基本语法 ##

### 标题语法

* `#`~`######`依次为1~6级标题

### 有序列表无序列表

* 有序列表：`*`+` `
* 无序列表：`num`+`.`

### 强调

* 斜体`*斜体内容*`eg：*斜体示*

* 加黑 `**加黑的内容**`eg：**加黑示例**

* 斜体加黑`***斜体加黑内容***`eg：***斜体加黑示例***

* 加黄 `<mark>要加黄的内容</mark>` eg：<mark>黄底示例</mark>

* 删除线`<del>删除内容</del>/~~删除内容~~`eg：<del>删除示例</del>

* 下划线`<u>下划线</u>`eg：<u>下划线示例</u>

* 角标`<sub>下角标</sub>正常<sup>上角标</sup>`eg：<sub>下角标</sub>正常<sup>上角标</sup>

* 加链接`<url>`eg：<www.baidu.com>；给链接备注名字`[name](url)`[MacDown的基本使用](https://blog.csdn.net/flt_ustc/article/details/78364452)

* 在文章中添加很多链接会显得很凌乱，特别是当链接比较长的时候，这样的情况下，我们可以这样做。将定义统一放在文章末尾，文中进行引用即可。

  ```javascript
  定义：[name]:URL
  引用：[name]
  ```

### 代码语法

* 插入代码：代码两侧加`

* 插入代码块：`~~~代码内容`

  * eg：

    ~~~javascript
    const word = '这是一段代码语句'
    ~~~

### 多选框

* `* [x] finished /* [] unfinished` ps：需要另起一行

  * eg：

    * [ ] 选择框
