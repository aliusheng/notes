# Less入门

## 一、Less的安装与使用

安装：npm install less;

下载less.js，并引用；

在命令行下使用：lessc style.less(找到正确目录下) > style.css(指定目录)

## 二、 基本了解

### 1.注释

- /* 我是被编译的 */；
- // 我是不会被编译的；

### 1.变量

@color: #4D926F;
想声明变量，@开头,如：@变量名：值。

    #header {
      color: @color;
    }

### 2.混合

1. 重复利用css，相同css，直接在后面使用前面定义过的class等名称；如下所示

        .box{
            width:100px;
            height:100px;
            .border;
        }
        .border{
            border:1px solid #ccc;
        }


2. 可带参数的混合
        
        .border2(@border_width){
          border:@border_width solid #ff0000;
        }
        .test-border2{
          .border2(5px);
        }


3. 混合 - 默认带值；
      
        .rounded-corners (@radius: 5px) {
          border-radius: @radius;
          -webkit-border-radius: @radius;
          -moz-border-radius: @radius;
        }
        
        #header {
        .rounded-corners;
        }
        #footer {
        .rounded-corners(10px);
        }

### 3.匹配模式

相当于JavaScript里的if，符合哪个参数，执行哪段代码。

    .triangle(top,@w:5px,@c:#ccc){
      border-width: @w;
      border-color: transparent transparent @c transparent;
      border-style:dashed dashed solid dashed;
    }
    .triangle(bottom,@w:5px,@c:#ccc){
      border-width: @w;
      border-color:@c transparent transparent transparent;
      border-style:solid dashed dashed  dashed;
    }
    .triangle(left,@w:5px,@c:#ccc){
      border-width: @w;
      border-color: transparent @c transparent transparent;
      border-style:dashed solid dashed  dashed;
    }
    .triangle(right,@w:5px,@c:#ccc){
      border-width: @w;
      border-color:transparent transparent transparent @c ;
      border-style:dashed dashed  dashed solid;
    }
    .triangle(@_,@w:5px,@c:#ccc){
      width:0;
      height:0;
      overflow: hidden;
    }
    .caret{
      .triangle(bottom,100px);
    }

@_ 相当于通配符，无论匹配哪段代码，都得加上这段通配的代码。

### 4.函数 & 运算

加减乘除括号通用。

    @test_w:300px;

    .box_w{
      width:(@test_w + 10) * 2;
    }

    @the-border: 1px;
    @base-color: #111;
    @red:        #842210;
    
    #header {
      color: @base-color * 3;
      border-left: @the-border;
      border-right: @the-border * 2;
    }
    #footer { 
      color: @base-color + #003300;
      border-color: desaturate(@red, 10%);
    }


### 5.嵌套

最有意思的小东西，
& 代表它的上一层选择器

    #header {
      h1 {
        font-size: 26px;
        font-weight: bold;
      }
      p { font-size: 12px;
        a { text-decoration: none;
          &:hover { border-width: 1px }
        }
      }
    }

### 6.@arguments变量

@arguments包含了所有传递进来的参数。


## 三、Less的编译

- node.js；
- koala自动编译工具；


