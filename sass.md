

# Sass用法指南

## 一、什么是Sass
Sass是一种css开发工具，提供许多便利的写法，使得css开发变得简单和可维护。

## 二、安装和使用

- 安装ruby；
 
- 安装sass；

- 运行转换器；

具体安装操作可参考网上教程。

## 三、基本用法

### 3.1 变量

SASS允许使用变量，所有变量以$开头。
    
    $blue : #1875e7;
    
    div {
      color: $blue;
    }

如果变量需要镶嵌在字符串之中，就必须需要写在#{}之中。

    $side : left;
    
    .round {
      border-#{$side}-radius : 5px;
    }

### 3.2 计算功能

    body {
      margin : (14px/2);
      top : 50px + 100px;
    }

### 3.3  嵌套

    div {
      h1 {
        margin : 10px;
      }
    }
    属性也可以嵌套
    p {
      border: {
        color:red;
      }
    }
    在嵌套的代码块内，可以使用&引用父元素。
    a {
      &:hover {
        color: #ffb3ff;
      }
    }

### 3.4 注释

标准的CSS注释 /* comment */ ，会保留到编译后的文件。

单行注释 // comment，只保留在SASS源文件中，编译后被省略。

在/*后面加一个感叹号，表示这是"重要注释"。即使是压缩模式编译，也会保留这行注释，通常可以用于声明版权信息。


## 四、代码的重用

### 4.1 继承

使用@extend命令

    .class1 {
      border:1px solid #ccc;
    }
    
    .class2 {
      @extend .class1;
      font-size:20px;
    }

### 4.2 Mixin

使用@mixin命令，定义一个代码块。

    @mixin left {
      float: left;
      margin-left:10px;
    }

使用@include命令，调用这个mixin。

    div {
      @include left;
    }

mixin的强大之处，在于可以指定参数和缺省值。
参数用$添加，可添加默认值；
使用的时候，根据需要加入参数。

    @mixin right($value : 10px) {
      float: right;
      margin-right: $value;
    }
    
    div {
      @include right(20px)
    }
    
    @mixin round($vert, $horz, $radius:10px) {
      border-#{$vert}-#{$horz}-radius:$radius;
      -moz-border-#{$vert}-#{$horz}-radius:$radius;
      -webkit-border-#{$vert}-#{$horz}-radius:$radius;
    }
    
    #nav li {
      @include round(top, left, 20px);
    }


### 4.3 颜色函数

### 4.4 插入文件

## 五、高级用法

### 5.1 条件语句

@if可以用来判断：

    p {
    　　　　@if 1 + 1 == 2 { border: 1px solid; }
    　　　　@if 5 < 3 { border: 2px dotted; }
    　　}

配套的还有@else命令：

    　　@if lightness($color) > 30% {
    　　　　background-color: #000;
    　　} @else {
    　　　　background-color: #fff;
    　　}


### 5.2 循环语句

SASS支持for循环：

    　　@for $i from 1 to 10 {
    　　　　.border-#{$i} {
    　　　　　　border: #{$i}px solid blue;
    　　　　}
    　　}

也支持while循环：

    　　$i: 6;
    　　@while $i > 0 {
    　　　　.item-#{$i} { width: 2em * $i; }
    　　　　$i: $i - 2;
    　　}

each命令，作用与for类似：

    　　@each $member in a, b, c, d {
    　　　　.#{$member} {
    　　　　　　background-image: url("/image/#{$member}.jpg");
    　　　　}
    　　}

### 5.3 自定义函数















