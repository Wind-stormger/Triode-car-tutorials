# 教程2：调整电机转速

## step 1 @unplugged

本节教程将指导学员应用扩展积木来控制TriodeCar左右俩电机的转速，并设计一套程序使人可以通过按钮来控制转速增减。

## step 2

在 ``||variables:变量||`` 中创建一个``||variables:speed||``变量。

从 ``||input:输入||`` 中将``||input:当按钮A被按下时||``积木拖放至编辑区内

从``||variables:变量||`` 中将``||variables:以1为幅度更改speed||``拖放至``||input:当按钮A被按下时||``积木中。

```blocks
input.onButtonPressed(Button.A, function () {
    speed += 1
})
let speed = 0
```

## step 3

基于第2步的方法创建一个``||input:当按钮B被按下时||``积木

置入``||variables:以1为幅度更改speed||``积木，将其内的数字修改为"-1",即变更为``||variables:以-1为幅度更改speed||``

```blocks
input.onButtonPressed(Button.B, function () {
    speed += -1
})
let speed = 0
```

<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
