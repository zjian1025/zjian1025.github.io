---
title: Sass基础
date: 2021-12-01 17:00:00
tags: 技术
categories: 常用
---

# Sass基础

## 简介
  sass的一个重要特性就是它为css引入了变量。 
  你可以把反复使用的css属性值 定义成变量，然后通过变量名来引用它们，而无需重复书写这一属性值。
  或者，对于仅使用过一 次的属性值，你可以赋予其一个易懂的变量名，让人一眼就知道这个属性值的用途。
***
## 1.使用变量
    //声明变量
	  $bg-color : #606060;
	  //使用变量
	  div{
      $width: 100px;
      width: $width;
      height:100px;
      background-color:$bg-color;
	  }
  * $width只能用在代码块儿div内，$bg-color 可以在整个样式中用（ $bg-color 与$bg_color 是一样的 ）
***
## 2.嵌套CSS 规则
    //sass中可以这样写
    #content {
      article {
      h1 { color: #333 }
      p { margin-bottom: 1.4em }
      }
      aside { background-color: #EEE }
    }
    //编译后为
    #content article h1 { color: #333 }
    #content article p { margin-bottom: 1.4em }
    #content aside { background-color: #EEE }
  ### 2.1 父选择器的标识符&
      //样例1
      article a {
        color: blue;
        &:hover { color: red }
      }
      //样例2
      #content aside {
        color: red;
        body.ie & { color: green }
      }
  ### 2.2 群组选择器的嵌套
      //样例1
      article a {
        color: blue;
        &:hover { color: red }
      }
      //样例2
      #content aside {
        color: red;
        body.ie & { color: green }
      }
  ### 2.3 子组合选择器和同层组合选择器：>、+和~
      //选择article下紧跟着的子元素中命中section选择器的元素
      article > section { border: 1px solid #ccc } 
      //选择header元素后紧跟的p元素
      header + p { font-size: 1.1em }
      //选择所有跟在article后的同层article元素，不管它们之间隔了多少其他元素
      article ~ article { border-top: 1px dashed #ccc }
      
      //总样例
      article {
        ~ article { border-top: 1px dashed #ccc }
        > section { background: #eee }
        dl > {
          dt { color: #333 }
          dd { color: #555 }
        }
        nav + & { margin-top: 0 }
      }
  ### 2.4 嵌套属性
      // 样例1
      nav {
        border: {
          style: solid;
          width: 1px;
          color: #ccc;
        }
      }
      // 样例2
      nav {
        border: 1px solid #ccc {
          left: 0px;
          right: 0px;
        }
      }
***
## 3.导入SASS文件
  css 的@import规则，只有执行到@import时，浏览器才会去下载其他css文件，这导致页面加载起来特别慢。  
	sass的@import规则，在生成css文件时就把相关文件导入进来
  ### 3.1 使用SASS部分文件
    通过@import把sass样式分散到多个文件，一般约定，sass局部文件的文件名以下划线开头
		例如：想导入themes/_night-sky.scss 只需 @import "themes/night-sky"
  ### 3.2 默认变量值
      //如果在导入局部文件之前声明了一个$fancybox-width变量，则局部文件中对$fancybox-width赋值400px的操作就无效。
      //如果用户没有做这样的声明，则$fancybox-width将默认为400px。
      $fancybox-width: 400px !default;
      .fancybox {
        width: $fancybox-width;
      }
  ### 3.3 嵌套导入
    .blue-theme {
      //@import "blue-theme"
    }  
  ### 3.4 原生的CSS导入
    不能用sass的@import直接导入一个原始的css文件,
		可以把原始的css文件改名为.scss后缀，即可直接导入了
***
## 4.静默注释
    body {
      color: #333; // 这种注释内容不会出现在生成的css文件中
      padding: 0; /* 这种注释内容会出现在生成的css文件中 */
    }
***
## 5.混合器
    可以通过sass的混合器实现大段样式的重用
    //定义一个混合器 @mixin 
    @mixin rounded-corners {
      -moz-border-radius: 5px;
      -webkit-border-radius: 5px;
      border-radius: 5px;
    }
    //使用混合器 @include
    notice {
      background-color: green;
      border: 2px solid #00aa00;
      @include rounded-corners;
    }
    //给混合器传参
    @mixin link-colors($normal, $hover, $visited) {
      color: $normal;
      &:hover { color: $hover; }
      &:visited { color: $visited; }
    }
    a {
      @include link-colors(blue, red, green);
    }
***
## 6.使用选择器继承来精简CSS *@extend*
    //通过选择器继承继承样式
    .error {
      border: 1px solid red;
      background-color: #fdd;
    }
    .seriousError {
      @extend .error;
      border-width: 3px;
    }
    //继承的高级用法
    //定义了一个名为disabled的类，样式修饰使它看上去像一个灰掉的超链接，
    //通过继承a这一超链接元素来实现
    .disabled {
      color: gray;
      @extend a;
    }
***