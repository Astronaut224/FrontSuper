# rem移动适配

rem是一种尺寸标准。

## 1. 基本使用

使用rem的第一步是设置html标签字号大小，1 rem = 1 html标签字号。

比如设置html标签字号为20px。

```html
<style>
    html {
        font-size: 20px;
    }
    
    .box {
        width: 5rem;
        height: 3rem;
        background-color: pink;
    }
</style>
```

这时候，盒子的大小就是 5x20px * 3x20px，也就是100px * 60px。

## 2. 媒体查询

媒体查询，根据不同设备的视口，设置不通的CSS。

使用方式和if语句很像，if满足视口条件，CSS就生效。

比如iPhone 6/7/8 视口为375*667，满足视口宽度375px，设置html标签字号为37.5px。一般html标签字号是视口的1/10。

```html
<style>
    @media (width: 375px) {
        html {
            font-size: 37.5px;
        }
    }
</style>
```

## 3. 使用流程

iPhone 6/7/8 有一个目标盒子是68px * 29px，现在要完成移动适配：

```html
<style>
    @meida (width: 375px) {
        html {
            font-size: 37.5px;
        }
    }
    
    .box {
        /* 视口是375px，html字号是37.5px，width=68/37.5 rem */
            width: 1.813rem;
            height: 0.773rem;
            background-color: pink;
    }
</style>
```

步骤：

1. 根据媒体查询视口，设置html标签字号。
2. 根据得到的html标签字号，设置盒子的宽高，单位为rem。

## 4. flexible.js

flexible.js是用来适配移动端的js框架，引入这个js文件就可以不用一个个媒体查询了。

核心原理：根据不同视口宽度给网页中的html根节点设置font-size

```html
<style>
	.box {
            /* 目标盒子在iPhone 6/7/8中是68px * 29px */
            /* 视口是375，html字号是37.5，width=68/37.5 */
            width: 1.813rem;
            height: 0.773rem;
            background-color: pink;
        }
</style>

<body>
    <div class="box"></div>

    <!-- 使用flexible.js就不用一个个添加媒体查询了，会自动检测视口并设置html字号 -->
    <script src="./js/flexible.js"></script>
</body>
```



