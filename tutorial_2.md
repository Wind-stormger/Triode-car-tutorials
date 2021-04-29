# 教程2：调整电机转速

## step 1 @unplugged

本节教程将指导学员应用扩展积木来控制TriodeCar左右俩电机的转速，并设计一套程序通过按钮来控制转速增减。

## step 2

在 ``||variables:变量||`` 中创建一个``||variables:speed||``变量。

从 ``||input:输入||`` 中将``||input:当按钮A被按下时||``积木拖放至编辑区内。

从``||variables:变量||`` 中将``||variables:以1为幅度更改speed||``拖放至``||input:当按钮A被按下时||``积木中。

```blocks
input.onButtonPressed(Button.A, function () {
    speed += 1
})
let speed = 0
```

## step 3

基于第2步的方法创建一个``||input:当按钮B被按下时||``积木。

置入``||variables:以1为幅度更改speed||``积木，将其内的数字修改为"-1",即变更为``||variables:以-1为幅度更改speed||``。

```blocks
input.onButtonPressed(Button.B, function () {
    speed += -1
})
let speed = 0
```

## step 4

现在按一次按钮A，``||variables:speed||``变量自加1，按一次按钮B，``||variables:speed||``变量自减1。

## step 5

将``||basic:显示数字0||``积木放入``||basic:无限循环||``中。

将``||variables:speed||``变量放置在``||basic:显示数字0||``积木的"0"上。

```blocks
basic.forever(function () {
    basic.showNumber(speed)
})
```

## step 6

现在受到按钮AB所控制的``||variables:speed||``变量数值将显示在micro:bit的5x5LED矩阵上。

点击左侧仿真micro:bit的按钮AB可以预览效果。

## step 7

从``||TriodeCar:TriodeCar||``中把``||TriodeCar:Left Motor move Foward at speed 0||``积木放入``||basic:无限循环||``中。

将``||variables:speed||``变量放置在``||TriodeCar:Left Motor move Foward at speed 0||``积木的"0"上。

```blocks
basic.forever(function () {
    triodecar.motorRun(triodecar.motor.left, speed)
    basic.showNumber(speed)
})
```

## step 8

复制``||TriodeCar:Left Motor move Foward at speed speed||``积木并将其改为``||TriodeCar:Right Motor move Foward at speed peed||``放入``||basic:无限循环||``中。

最好将这两个积木放在``||basic:显示数字speed||``上面，使其优先执行。

```blocks
basic.forever(function () {
    triodecar.motorRun(triodecar.motor.left, speed)
    triodecar.motorRun(triodecar.motor.right, speed)
    basic.showNumber(speed)
})
```

## step 9

从``||TriodeCar:TriodeCar||``中将``||TriodeCar:let the car go foward||``积木置入 ``||basic:当开机时||``，将可选项改为"stop"。

此处实现的功能为：micro:bit开机或重置时停止TriodeCar的电机。

```blocks
 triodecar.CarDirection(triodecar.direction.stop)
```


## step 10

现在按钮AB控制的``||variables:speed||``变量将控制TriodeCar左右电机的转速。

值得注意的是``||TriodeCar:Left Motor move Foward at speed 0||``积木的取值范围为0-10，我们需要限制``||variables:speed||``变量的范围。

## step 11

从``||logic:逻辑||``中将``||logic:如果为true则||``积木放入``||basic:无限循环||``中的最前排。

在这个``||logic:如果为true则||``中添加复合条件，``||variables:speed||``<0 或 10<``||variables:speed||`` 。

相关会应用的积木都在``||logic:逻辑||``中。

从``||variables:变量||`` 中将``||variables:将speed设为0||``放入``||logic:如果||``内。

```blocks
basic.forever(function () {
    if (speed < 0 || speed > 10) {
        speed = 0
    }
    triodecar.motorRun(triodecar.motor.left, speed)
    triodecar.motorRun(triodecar.motor.right, speed)
    basic.showNumber(speed)
})
```

## step 12

通过USB连接micro:bit,点击``|Download|``将程序下载进micro:bit。

现在按钮AB可以对TriodeCar左右电机的转速进行控制且``||variables:speed||``不会溢出范围，当将要溢出时可以将数值归零。

<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
