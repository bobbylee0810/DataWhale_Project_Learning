# 1 创建标题

```markdown
# 一级标题

## 二级标题
```

# 2 段落换行与空格

```markdown
这是一个换行符<br>
换行后的内容<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;这是不断行的空格  
&ensp;一个半角空格，长度为中文空格的一半  
&emsp;一个全角空格  
&emsp;&emsp;首行缩进两个字符
```

这是一个换行符<br>
换行后的内容<br>
<br>
&nbsp;&nbsp;&nbsp;&nbsp;这是不断行的空格  
&ensp;一个半角空格，长度为中文空格的一半  
&emsp;一个全角空格  
&emsp;&emsp;首行缩进两个字符

# 3 文本处理

```markdown
文本**加粗**<br>
文本**_加粗斜体_**
```

文本**加粗**<br>
文本**_加粗斜体_**  
~~删除线~~

# 4 创建引用

```markdown
> 这是一段引用的文字
>
> > 二级引用
```

> 这是一段引用的文字
>
> > 二级引用

# 5 创建有序列表：

```markdown
1. 第一项
2. 第二项
3. 第三项

创建无序列表：<br>

- 列表 1
- 列表 2
  - 子列表
    - 子子列表
  - 子列表
- 列表 3

列表中嵌套其他元素（使用制表符 tab 或者 4 个空格）

- 列表 1
- 列表 2  
   这是其他元素
  > 这是一个引用
- 列表 3
```

1. 第一项
2. 第二项
3. 第三项

创建无序列表：<br>

- 列表 1
- 列表 2
  - 子列表
    - 子子列表
  - 子列表
- 列表 3

列表中嵌套其他元素（使用制表符 tab 或者 4 个空格）

- 列表 1
- 列表 2  
   这是其他元素
  > 这是一个引用
- 列表 3

# 6 嵌入单行或代码：

```markdown
嵌入单行代码`import numpy as np`

嵌入多行代码：  
 `python import numpy as np import pandas as pd def main(): print('hello,world') `
```

嵌入单行代码`import numpy as np`

嵌入多行代码：

```python
import numpy as np
import pandas as pd
def main():
    print('hello,world')
```

# 7 创建分割线：

```markdown
&nbsp 用于创建空行，以下三种 3 连续字符都可以用来创建下划线
&nbsp;

---

## &nbsp;

&nbsp;

---
```

&nbsp;

---

&nbsp;

---

&nbsp;

---

# 8 创建链接

```markdown
这是一个链接[百度](www.baidu.com)  
创建一个可以点击的链接  
<www.baidu.com>
```

这是一个链接[百度](www.baidu.com)  
创建一个可以点击的链接  
<www.baidu.com>

# 9 插入图片

![自由之翼](./pic/576999.png)
使用 html 插入图片并约束大小

<div  align="center"> 
<img src="./pic/576999.png" width = "300" height = "200" alt="图片名称" align=center />
</div>

# 10 html

在 markdown 中可以直接使用 html 语言

<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

# 11 创建表格

| 项目 | Value |  ni |
| :--- | :---: | --: |
| 电脑 | $1600 | xin |
| 手机 |  $12  | xin |
| 导管 |  $1   | xin |
