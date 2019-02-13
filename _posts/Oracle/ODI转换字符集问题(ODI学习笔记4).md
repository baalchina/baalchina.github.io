Title: ODI转换字符集问题（ODI学习笔记4）
Date:
URL: 
Tags: 

一个Oracle库到MySQL库的转换，字符集，其中Oracle 11gR2，很常规的`NLS_CHARACTERSET=AL32UTF8`，MySQL也是标准`UTF8`。

但是转换过程中，中文的文字始终是???乱码。尝试了多种办法，最后试了一个最笨的：
1. 将源表新建一个视图，中文的内容使用`  utl_raw.cast_to_raw(REMARK) as REMARK,`转换成`RAW`格式
2. 此时在视图中看，内容变成了`E7AB9EE7A780E6A5BCE58D97E6A5BC73333033`这样的格式
3. 使用视图进行映射，注意此时查看源视图，内容变成了`<unsupported image format>`
4. 表达式中使用convert函数，如下：`convert(viewname.colname using utf8)`，执行位置设置为目标
5. 需注意的是，这个`convert`函数是mysql，也就是目标的函数
6. 最终问题解决。

感觉方法有点笨，不过能解决就好~