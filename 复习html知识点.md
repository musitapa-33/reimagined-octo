
 一、HTML基本结构
- 文档声明：`<!DOCTYPE html>` 声明当前文档为HTML5文档，位于最开头。
- 根标签：`<html>` 是所有HTML元素的根容器。
- 头部标签：`<head>` 包含文档元数据，如字符编码、标题等：
  - `<meta charset="utf-8">`：指定文档字符编码为UTF-8（支持中文）。
  - `<title>`：定义网页标题（显示在浏览器标签页）。
- 主体标签：`<body>` 包含网页可见内容（文本、图片、链接等）。

 示例（来自所有文件）：
 ```html
 <!DOCTYPE html>
 <html>
   <head>
     <meta charset="utf-8">
     <title></title>
   </head>
   <body> <!-- 可见内容 --> </body>
 </html>
 ```


二、文本与排版标签
1. 标题标签：`<h1>` 到 `<h6>`，字体大小依次递减，用于层级标题。
   - 示例（电影.html）：`<h1 align="center">电影赏析网</h1>`、`<h2>《当幸福来敲门》剧情介绍</h2>`

2. 段落标签：`<p>` 用于定义段落，自动换行。
   - 示例（个人成长.html）：`<p>额敏县位于中国新疆维吾尔自治区塔城地区...</p>`

3. 预格式标签：`<pre>` 保留文本原有格式（空格、换行），常用于诗词、代码等。
   - 示例（唐诗宋词.html）：`<pre>` 包裹多首诗词，保留排版。

4. 水平线标签：`<hr>` 插入水平线，可通过`size`（厚度）、`color`（颜色）属性设置。
   - 示例（首页.html）：`<hr size="5px" color="blue">`
5.<br/> 换行
6. <strong> 加粗强调
7. <ins> 下划线标注
8. <em> 斜体强调
9. <mark>高亮标记
10. sup sub
11. &nbsp; 空格


 三、链接与锚点
1. 超链接标签：`<a>` 用于页面跳转，核心属性：
   - `href`：指定链接地址（如`href="首页.html"`跳转到本地页面）。
   - `target`：指定打开方式（`_blank`在新窗口打开，代码中`_biank`为笔误，正确为`_blank`）。
   - 示例（课程表.html）：`<a href="首页.html" target="_biank">返回首页</a>`

2. 锚点链接：用于页面内跳转，通过`id`属性定位目标位置。
   - 示例（唐诗宋词.html）：
     ```html
     <a href="#静夜思">《静夜思》-李白</a> <!-- 点击跳转到id为"静夜思"的元素 -->
     <h2 id="静夜思">1. 《静夜思》 - 李白 </h2> <!-- 目标位置 -->
     ```

四、图像标签
- `<img>` 用于插入图片，核心属性：
  - `src`：图片路径（本地路径如`src="img/musitapa.jpg"`或网络URL）。
  - `alt`：图片加载失败时显示的替代文本。
  - `title`：鼠标悬停时显示的提示文本。
  - `width`/`height`：设置图片宽高。
  - `align`：图片对齐方式（如`align="left"`左对齐）。

 示例（首页.html）：
 ```html
 <img src="img/musitapa.jpg" alt="mu" title="mu" align="left" width="50" height="70">
 ```


五、表格标签
- 用于展示结构化数据（如课程表、简历），核心标签：
  - `<table>`：表格容器，属性`border`（边框宽度）、`width`（表格宽度）、`align`（对齐方式）等。
  - `<tr>`：表格行。
  - `<td>`：表格单元格，属性`colspan`（跨列合并，如`colspan="2"`占2列）、`rowspan`（跨行合并，如`rowspan="5"`占5行）。

 示例（课程表.html）：
 ```html
 <table border="1">
   <tr> <!-- 第一行 -->
     <td>星期节次</td>
     <td>星期一</td>
     <!-- 其他单元格 -->
   </tr>
   <tr> <!-- 第二行 -->
     <td>1-2</td>
     <td>高等数学</td>
     <td rowspan="5" colspan="2" align="center">双休</td> <!-- 跨5行2列 -->
   </tr>
 </table>
 ```


六、表单标签
- 用于收集用户输入（如注册页），核心标签：
  - `<input>`：单标签，通过`type`属性定义输入类型：
    - `type="text"`：文本框（如用户名）。
    - `type="password"`：密码框（输入内容隐藏）。
    - `type="radio"`：单选按钮（`name`相同为一组，`checked`默认选中）。
    - `type="checkbox"`：复选框（可多选）。
    - `type="file"`：文件上传。
    - `type="submit"`：提交按钮（提交表单数据）。
    - `type="reset"`：重置按钮（清空表单）。
    - `type="button"`：普通按钮。

 示例（注册.html）：
 ```html
 用户名:<input type="text" value="穆斯塔怕" maxlength="10" /><br />
 密码：<input type="password" size="20"><br />
 性别：<input type="radio" name="sex" checked="checked">男
       <input type="radio" name="sex">女<br />
 ```


七、多媒体标签
- `<video>`：插入视频，核心属性：
  - `src`：视频路径。
  - `controls`：显示播放控制条。
  - `autoplay`：自动播放（部分浏览器需配合`muted`静音）。
  - `loop`：循环播放。

 示例（电影.html）：
 ```html
 <video src="dangxingfulaiqiaomeng.mp4" controls="controls" autoplay="autoplay" loop="loop"></video>
 ```


八、其他常用标签
1. 折叠/展开标签：`<details>`（容器）和`<summary>`（折叠标题），点击可展开内容。
   - 示例（电影.html）：

     ```html
     <details>
       <summary>展开评论</summary> <!-- 折叠时显示的标题 -->
       <h4>评论者A:</h4>
       <p>《当幸福来敲门》是一部非常值得一看的电影...</p>
     </details>
     ```

2. 进度与度量标签：
   - `<progress>`：展示任务进度（如评分进度），`value`为当前值，`max`为最大值。
   - `<meter>`：展示度量值（如评分），`min`/`max`为范围，`low`/`high`为高低阈值。
   - 示例（电影.html）：
   - 
     ```html
     综合评分:<progress value="50" max="100"></progress>
     电影画质:<meter value="56" min="0" max="100" low="60" high="80"></meter>
     ```
	 
3.列表
无序：
<ul>
	<li></li>
</ul>
示例：

```html
<ul>
<li><h2 id="静夜思">《静夜思》-李白 </h2></li>
	床前明月光，疑是地上霜。
	举头望明月，低头思故乡。
</ul>
```


有序：
<ol>
	<li></li>
</ol>

示例：
```html
<ol>
<li><a href="#静夜思">《静夜思》-李白</a></li>
</ol>
```

属性start reversed