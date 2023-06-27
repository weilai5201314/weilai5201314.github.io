# Markdown格式教程
> markdown格式的讲解
> 
> 面向初学者
> 
> 编写者：wzj
> 
> [参考网站](https://thu-ios.github.io/tutorials/lecture/markdown.html) —— 作者：yxj


[toc]

## *具体语法*
### 1.关于标题
1～6个井号加一个空格再加上标题的名称
标题的等级由`#`的数量来决定
```
# 一级标题
## 二级
......
###### 六级
```

### 2.关于文体
#### **加粗和斜体**

可以使用*或者_来加粗和添加斜体
```swift
*hello world*
_hello world_

**hello world**
__hello world__
```
输出样子：
*hello world*
_hello world_

**hello world**
__hello world__

注意：*或者_之间不能有空格，不然会失效。

### 3.链接语法
#### **链接网站**

`[题目](网站链接)` :中括号和小括号结合
```
[github](https://github.com)
```
输出结果：
[github](https://github.com)

#### **直接标出网站**
```
<https://github.com>
```
  输出结果：
  <https://github.com>

#### **链接图片**
`![自己选择写不写] (网站)`
这里`[]`内部可以不写任何文字，也可以输出，写了的话会在图片下方或某处显示说明，当因为某种原因图片无法加载的时候，显示时也会用说明替代图片。
```
![iphone13 pro](https://www.apple.com.cn/v/iphone-13-pro/f/images/overview/design/design_display_pro__d3dtminb414y_small_2x.png)
```
输出结果：
![iphone13 pro](https://www.apple.com.cn/v/iphone-13-pro/f/images/overview/design/design_display_pro__d3dtminb414y_small_2x.png)




### 4.行内代码
#### **行内代码，标注某一个**
使用英文标点符号   **`** ,在tab上面
``` swift
`swift`和`github`都是大大的好东西 
```

`swift`和`github`都是大大的好东西

#### **注释代码块**
一对，三个，英文符号  **`**  来包裹代码块，还可以第一个反撇后面添加语言来获得高亮支持

\```swift
var natural_number: Arrary<Int> = [0,1,2,3]
print(natural_numbers.capacity)
\```

```swift
var natural_number: Arrary<Int> = [0,1,2,3]
print(natural_numbers.capacity)

```
支持高亮的代码很多，比如：`shell`,`c`,` c++ `,`java`,`python`,`swift`,`html`.

#### **引用的格式**
```
>markdown的格式讲解
>面向初学者
```
>markdown的格式讲解
>面向初学者

一般可以用来在开头注释，标注讲稿内容。

#### **表格**
可以使用一些符号来直接制作文本表格
```
|name | gender
----- | -
wzj |    boy
c.c | girl
```
输出结果：
| name | gender |
| ---- | ------ |
| wzj  | boy    |
| C.C  | gir    |

**注** ：不同的`markdown`编辑器，语法也会有所不同，表格的书写方式可能不一样



## *其他Github支持的语法*
其他`Github`支持的语法可以看[Github Docs](https://docs.github.com/cn/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)




## *对文件路径的理解*
```
1.[Github](https://github.com)
2.查看[帮助文档](./doc/help.md)
3.跳转到[具体语法](#具体语法)
```
第一种一般是在文本中插入网站。

第二种是一种路径的写法，是相对路径，表示和当前md文件在同一个路径下的`doc`文件夹里的 `help.md` 文件,一般推荐写相对路径，只需要跟着总文件夹走。

第三种是一种链接，跳转到当前文档的某个标题处。

## *添加目录*
不少平台都支持使用`[toc]`来添加目录。你只需要输入`[toc]`，平台就会帮你自动渲染生成目录。但是也有一些平台不支持。

## *其他注意事项*
为了排版的顺利，建议在每结束一段话之后进行回车（多于两个的连续回车会被当成一个回车）