# Flex布局

## 1. 组成使用

flex布局由弹性容器、弹性盒子、主轴和交叉轴组成。

使用Flex布局可以使盒子在一行展示，相对于浮动，浏览器更推荐用Flex。

```html
	<style>
        * {
            margin: 0;
            padding: 0;
        }
        .box {
            /* 视觉效果：弹性盒子水平排列，原因是主轴默认水平方向，弹性盒子沿着主轴排列。 */
            display: flex;
            height: 200px;
            border: 1px solid #000;
        }
        .box div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
```

## 2. 轴对齐方式

**主轴对齐效果**

1. 水平居中

```html
display: flex;
justify-content: center;
```

2. 间距在弹性盒子（子元素）之间

```html
justify-content: space-between;
```

3. 间距在弹性盒子两侧，视觉效果是盒子之间间距大，边上间距小

```html
justify-content: space-around;
```

4. 所有间距都一样，无论边上还是盒子之间。

```html
justify-content: space-evenly;
```

**侧轴对齐效果**

1. 垂直居中

```html
align-items: center
```

2. 默认值，视觉效果是弹性盒子被拉伸，测试时不能设置弹性盒子的高

```html
align-items: stretch;
```

## 3. 弹性伸缩比

使用flex属性修改弹性盒子伸缩比，也就是设置弹性盒子（子集）的尺寸。

`flex: 整数值;` 整数值表示占父级剩余尺寸的份数

```html
	<style>
        * {
            margin: 0;
            padding: 0;
        }

        .box {
            display: flex;
            height: 300px;
            border: 1px solid #000;
        }

        .box div {
            height: 200px;
            margin: 0 20px;
            background-color: pink;
        }

        .box div:nth-child(1) {
            width: 50px;
        }

        .box div:nth-child(2) {
            /* flex: 整数值; 表示占父级剩下部分的份数 */
            /* 上面的写法表示除去已用的宽度，父级剩下的宽度分成3份，div2占2份，div3占1份 */
            flex: 2;
        }

        .box div:nth-child(3) {
            flex: 1;
        }
    </style>
```



**弹性盒子尺寸特点**

**flex布局**下，**主轴和侧轴如果不定义**，

弹性盒子的宽如果不设置，盒子的宽就是内容的宽（被内容撑开）；

弹性盒子的高如果不设置，盒子的高默认被拉伸成父级元素的高。

个人总结：宽缩高胀

## 4. 修改主轴方向

主轴方向默认是水平的，可以设置`flex-direction`的值来修改主轴的方向。

```html
.box li {
	display: flex;
	/* 修改主轴的方向为垂直方向 */
	flex-direction: column;
	
	/* 因为主轴方向变成垂直方向，所以这句作用变成了水平居中 */
	align-items: center;

	/* 这行的作用变成了垂直居中 */
	justify-content: center;
}
```

所以在设置主轴和侧轴对齐方式时，需要先确定主轴的方向。



## 5. 弹性盒子换行

Flex布局下，弹性盒子默认沿着主轴排列。

当弹性模型的宽不够的时候，会挤压弹性盒子的宽，使弹性盒子在一行排列。

默认情况下弹性盒子不会换行，可以通过设置`flex-wrap`来换行。

```html
.box {
	display: flex;
	/* 默认情况下弹性盒子不换行 */
    /* flex-wrap: nowrap; */
	
	/* 换行 */
	flex-wrap: wrap;
}
```



## 6. 行对齐方式

弹性盒子换行后，发现行间距均分了父级元素剩下的尺寸。

可以通过设置`align-content`设置行间距，用法和`justify-content`差不多。

```html
.box {
	display: flex;
	
	/* 换行 */
	flex-wrap: wrap;

	/* 行间距分配在上下两侧，弹性盒子紧挨着居中 */
	align-content: center;
	/* 行间距分配在所有弹性盒子的两侧，效果是盒子之间较宽，上下两侧较窄 */
	align-content: space-around;
	/* 行间距分配在弹性盒子之间，上下两侧紧贴着模型的边 */
	align-content: space-between;
}
```

