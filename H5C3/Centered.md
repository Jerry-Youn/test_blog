## 水平居中

### 行内/行内块元素

```css
text-align: center;
```

### 块级元素

##### margin

###### 子元素宽度确定

```css
margin: 0 auto;
```

###### 子元素宽度不确定

```css
margin: 0 20px; //这里20只是随便给一个值
```

### 任意元素（块或者行内均适用）

##### 绝对定位实现

> 原理：子绝父相 left+translate 实现居中

```css
#parent {
  position: relative;
  width: 200px;
  height: 200px;
  background-color: pink;
}
#child {
  position: absolute;
  width: 100px;
  height: 100px;
  left: 50%; //
  transform: translateX(-50%); //
  background-color: skyblue;
}
```

##### flex 实现

```css
#parent {
  display: flex;
  justify-content: center;
}
```

## 垂直居中

### 行内/行内块元素

> 可以用 padding 去撑开 height

```css
height: 150px;
line-height: 150px;
```

### 图片

> 除去 line-height = height 外 还要设置 vertical-align = middle

```css
#parent {
  height: 700px;
  line-height: 700px;
  background-color: pink;
}
#child {
  vertical-align: middle;
}
```

### 块元素

> child 高度不管确定与否都可以给上下 padding

##### 绝对定位实现

```css
.parent {
  // 核心代码
  position: relative;
  // 凑数代码
  height: 200px;
  width: auto;
  background-color: pink;
}
.child {
  // 核心代码
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  // 凑数代码
  width: 100px;
  height: 100px;
  background-color: #fff;
}
```

###### 方案 2

> 当绝对定位的元素 top 和 bottom 为 0 时，margin-top&bottom 会无限延伸占满空间并平分

```css
#parent {
  position: relative;
}
#son {
  position: absolute;
  margin: auto 0;
  top: 0;
  bottom: 0;
  height: 50px;
}
```

##### flex 方案

### 任意元素

##### flex

> 方案 1

```css
#parent {
  display: flex;
  align-items: center;
}
```

> 方案 2

```css
#parent {
  display: flex;
}
#son {
  align-self: center;
}
```

> 方案 3

```css
#parent {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
```

## 水平垂直居中

### 行内元素/图片

> font-size:0; 消除近似居中的 bug

```css
#parent {
  height:150px;
  line-height:150px;
  text-align-center;
  font-szie:0;
}
#son {
 vertical-align:middle;
}
```

### 块元素

#### 绝对定位

```css
#parent {
  position: relative;
}
#son {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

#### 绝对居中

> 当绝对元素的 top 和 bottom 设置为 0 后 margin 的 auto 会自动延生填充去 left 和 right 也是一样

```css
#parent {
  position: relative;
}
#son {
  position: absolute;
  margin: auto;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
```

### flex 方案

```css
#parent {
  display: flex;
}
#son {
  margin: auto;
}
```

```css
#parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

```css
#parent {
  display: flex;
  justify-content: center;
}
#son {
  align-items: center;
}
```

## 视口居中

> magin 最后的 0 是为了隐藏滚动条

```css
#son {
  margin: 50vh auto 0;
  transform: translateY(-50%);
}
```
