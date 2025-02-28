---
​---
title: Export in Typora
author: John Snow
​---
---

# Make Cover

## YAML方式修改标题和作者

默认的title是文件名, 可通过在md文件的head添加YAML方式修改导出pdf时的封面标题*(前提是在导出设置的pdf设置中勾选“允许YAML front matters 覆盖当前设置”)*

通过 *段落->YAML front matter*插入:

```yaml
---
title: Export in Typora
author: John Snow
---
```

由于此模版导出pdf的html设置中只使用了${title} 和 \${author}宏, 所以只需要设置这两个即可

## 完整的pdf导出插入html封面设置

```html
<meta name="title" content="${title}">
<meta name="author" content="${author}">

<div id="cover-container">
  <div class="cover" style="page-break-after:always;font-family:方正公文仿宋;width:100%;height:100%;border:none;margin: 0 auto;text-align:center;">
      </br></br></br></br>
      
      <!-- 自动填充标题（加粗） -->
      <p id="export-title" style="font-family:Times New Roman, 宋体;text-align:center;font-size:22pt;font-weight:bold;margin: 0 auto"></p>
      <p id="export-subtitle" style="font-family:Times New Roman, 宋体;text-align:center;font-size:25pt;font-weight:bold;margin: 0 auto"></p>

      <div style="width:60%;margin: 0 auto;height:0;padding-bottom:10%;">
          </br></br>
          <img src="https://raw.githubusercontent.com/canUuuu/UESTC-logo/master/svg_source/UESTClogo.svg" alt="校徽" style="width:70%;"/>
      </div>
      </br></br></br></br></br></br></br></br></br></br></br></br></br></br></br></br></br>
      
      <!-- 自动填充作者信息 -->
      <p id="export-author" style="font-family:Times New Roman, 宋体;text-align:center;font-size:18pt;margin: 0 auto"></p>
      </br></br>
      
      <!-- 自动填充当前日期 -->
      <p id="current-date" style="text-align:center;font-size:17pt;margin: 0 auto;font-family:Times New Roman;"></p>
      </br></br></br></br></br></br></br>
  </div>
</div>

<script>
  // 确保封面始终是 PDF 的第一页
  var coverContainer = document.getElementById("cover-container");
  document.body.insertBefore(coverContainer, document.body.firstChild);

  // 获取 Typora 自动生成的标题
  var titleMeta = document.querySelector("meta[name='title']");
  var title = titleMeta ? titleMeta.getAttribute("content") : "";
  // 备用方案：如果 title 为空，尝试使用 document.title
  if (!title || title === "${title}") {
      title = document.title || "Untitled Document";  // 如果都获取不到，则用默认值
  }
  document.getElementById("export-title").textContent = title;

  // 获取作者信息，如果未定义，则默认 "Kevin"
  var authorMeta = document.querySelector("meta[name='author']");
  var author = authorMeta ? authorMeta.getAttribute("content") : "";
  if (!author || author === "${author}") {
      author = "Kevin";  // 默认作者
  }
  document.getElementById("export-author").textContent = author;

  // 生成当前日期，格式：DD MMM YYYY（例如：28 FEB 2025）
  var today = new Date();
  var monthNames = ["JAN", "FEB", "MAR", "APR", "MAY", "JUN", 
                    "JUL", "AUG", "SEP", "OCT", "NOV", "DEC"];
  var formattedDate = today.getDate() + " " + 
                      monthNames[today.getMonth()] + " " + 
                      today.getFullYear();
  document.getElementById("current-date").textContent = formattedDate;
</script>

```

* 校徽logo的raw文件(https://raw.githubusercontent.com/canUuuu/UESTC-logo/master/svg_source/UESTClogo.svg)来自github仓库(https://github.com/canUuuu/UESTC-logo)
* 存在一直问题: 若勾选导出时页脚添加页码, 则封面也会有页码标注



另一种模仿学校论文封面的html模版:

<div class="cover" style="page-break-after:always;font-family:仿宋;width:100%;height:100%;border:none;margin: 0 auto;text-align:center;">
    <div style="width:80%;;margin: 0 auto;height:0;padding-bottom:25%;">
        <img src="https://raw.githubusercontent.com/canUuuu/UESTC-logo/refs/heads/master/svg_source/UESTCname.svg" alt="校名" style="width:100%;"/></div>
    <br><br>
    <div style="width:40%;margin: 0 auto;height:0;padding-bottom:40%;">
        <img src="https://raw.githubusercontent.com/canUuuu/UESTC-logo/refs/heads/master/svg_source/UESTClogo.svg" alt="校徽" style="width:100%;"/></div>
    <br><br>
    <p style="text-align:center;font-size:24pt;margin: 0 auto">[课程名称]</p>
    <p style="text-align:center;font-size:24pt;margin: 0 auto">[论文类型] </p>
    <br><br>
    <table style="border:none;text-align:center;width:80%;font-family:仿宋;margin: 0 auto;">
    <tbody style="font-family:仿宋;font-size:16pt;">
      <tr style="font-weight:bold;"> 
		<td style="width:25%;text-align:right;">题&emsp;&emsp;目</td><td style="width:5%">：</td> 
		<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[论文题目]</td></tr><tr style="font-weight:bold;"> 
	<td style="width:25%;text-align:right;">姓&emsp;&emsp;名</td><td style="width:5%">：</td> 
	<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[你的名字]</td></tr>
      <tr style="font-weight:bold;"> 
	<td style="width:25%;text-align:right;">学&emsp;&emsp;号</td><td style="width:5%">：</td> 
	<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[你的学号] </td></tr>
      <tr style="font-weight:bold;"> 
	<td style="width:25%;text-align:right;">专&emsp;&emsp;业</td><td style="width:5%">：</td> 
	<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[你的专业]</td></tr>

<tr style="font-weight:bold;"> 
	<td style="width:25%;text-align:right;">上课时间</td><td style="width:5%">：</td> 
	<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[上课时间]</td></tr>

<tr style="font-weight:bold;"> 
	<td style="width:25%;text-align:right;">授课教师</td><td style="width:5%">：</td> 
	<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[教师姓名]</td></tr>
	</tbody></table>
	<br><br>
</div>



代码如下:

```html
<div class="cover" style="page-break-after:always;font-family:仿宋;width:100%;height:100%;border:none;margin: 0 auto;text-align:center;">
    <div style="width:80%;;margin: 0 auto;height:0;padding-bottom:25%;">
        <img src="https://raw.githubusercontent.com/canUuuu/UESTC-logo/refs/heads/master/svg_source/UESTCname.svg" alt="校名" style="width:100%;"/></div>
    <br><br>
    <div style="width:40%;margin: 0 auto;height:0;padding-bottom:40%;">
        <img src="https://raw.githubusercontent.com/canUuuu/UESTC-logo/refs/heads/master/svg_source/UESTClogo.svg" alt="校徽" style="width:100%;"/></div>
    <br><br>
    <p style="text-align:center;font-size:24pt;margin: 0 auto">[课程名称]</p>
    <p style="text-align:center;font-size:24pt;margin: 0 auto">[论文类型] </p>
    <br><br>
    <table style="border:none;text-align:center;width:80%;font-family:仿宋;margin: 0 auto;">
    <tbody style="font-family:仿宋;font-size:16pt;">
     
    	<tr style="font-weight:bold;"> 
    		<td style="width:25%;text-align:right;">题&emsp;&emsp;目</td><td style="width:5%">：</td> 
    		<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[论文题目]</td></tr>
      
        <tr style="font-weight:bold;"> 
    		<td style="width:25%;text-align:right;">姓&emsp;&emsp;名</td><td style="width:5%">：</td> 
    		<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[你的名字]</td></tr>
      
    	<tr style="font-weight:bold;"> 
    		<td style="width:25%;text-align:right;">学&emsp;&emsp;号</td><td style="width:5%">：</td> 
    		<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[你的学号] </td></tr>
      
        <tr style="font-weight:bold;"> 
    		<td style="width:25%;text-align:right;">专&emsp;&emsp;业</td><td style="width:5%">：</td> 
    		<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[你的专业]</td></tr>
      
    	<tr style="font-weight:bold;"> 
    		<td style="width:25%;text-align:right;">上课时间</td><td style="width:5%">：</td> 
    		<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[上课时间]</td></tr>
      
    	<tr style="font-weight:bold;"> 
    		<td style="width:25%;text-align:right;">授课教师</td><td style="width:5%">：</td> 
    		<td style="font-weight:normal;border-bottom: 2px solid;text-align:center;">[教师姓名]</td></tr>
     
    </tbody></table>
 		<br><br>
</div>
```

使用方法为, 在需要导出的md文件head上复制html代码, 修改相应内容即可导出

## 中文版论文主题参考

https://github.com/Keldos-Li/typora-latex-theme







