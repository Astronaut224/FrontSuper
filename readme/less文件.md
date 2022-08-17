# less文件

less是一个CSS预处理器，扩充了CSS语言使其具备逻辑能力和计算能力，浏览器不识别less文件。

## 1. 嵌套

less可以通过嵌套的方式，生成后代CSS代码。`&:hover`可以生成hover代码。

```less
.father {
    width: 100px;
    .son {
        background-color: pink;

        // 子集的hover
        &:hover {
            color: skyblue;
        }
    }

    &:hover {
        color: green;
    }
}
```

```css
.father {
  width: 100px;
}
.father .son {
  background-color: pink;
}
.father .son:hover {
  color: skyblue;
}
.father:hover {
  color: green;
}
```

## 2. 计算

less文件可以完成代码中的计算，将结果输出到生成的css文件中。

**需要注意除法的写法。**

```less
.box {
    width: 10+100px;
    width: 100-100px;
    width: 10*10px;

    // 除法需要放在括号里
    width: (68 / 37.5rem);
}
```

```css
.box {
  width: 110px;
  width: 0px;
  width: 100px;
  width: 1.81333333rem;
}
```

## 3. 变量

定义变量：@变量名: 值

使用变量：CSS属性: @变量名

变量在批量修改属性时很方便。

```less
.box {
    color: @colora;
}

.father {
    background-color: @colora;
}
```

```css
.box {
  color: pink;
}
.father {
  background-color: pink;
}
```

## 4. 导入

通过`@import '路径';`导入多个less文件

```less
@import '体验less.less';
// 如果是less文件，后缀.less可以省略
@import '变量';
```

## 5. 导出

vscode中默认less文件是导出到相同的文件目录下，通过**设置-easy less-setting.json**中可以修改导出路径。

```json
"less.compile": {
        "out": "../css/"
    }
```

如果要单独设置某一less文件的导出路径，在文件最上面加`// out: 导出路径`来单独导出某一文件。ps：到处路径可以是具体文件，也可以是文件夹下。

```less
// out: ./hello/world.css

.box {
    color: red;
}
=============================================
// out: ./out/

.box {
    color: red;
}
```

## 6. 禁止导出

在文件开头添加`// out: false`来控制less不生成css文件

