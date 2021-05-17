# 教程4：使用两块micro:bit通过无线电通讯控制电机

## step 1 @unplugged

基于micro:bit上集成的无线通信模块同时具备无线电收发的功能，我们可以使多块micro:bit之间建立无线连接，并可互相控制。

本节教程将指导学员在MakeCode中应用无线电扩展积木与TriodeCar扩展积木进行编程，使两块micro:bit之间建立无线电通讯并能互相控制，以此实现对TriodeCar的遥控。

## step 2

在``||basic:无限循环||``中加入``||logic:如果为（）则||``积木，将``||input:当按钮A+B被按下时||``积木作为条件加入其条件框中。

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
})
```

## step 3

在``||logic:如果为（）则||``积木上点击``||logic:+||``添加一个``||logic:否则||``，再点击``||logic:+||``添加两个``||logic:否则如果为（）则||``

将``||input:当按钮A被按下时||``积木与``||input:当按钮B被按下时||``积木作为条件分别放入两个``||logic:否则如果为（）则||``的条件框中。

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
    } else if (input.buttonIsPressed(Button.A)) {
    } else if (input.buttonIsPressed(Button.B)) {
    } else {
    }
})
```

## step 4

我们需要理解为什么``||input:当按钮A+B被按下时||``作为条件被放置在整个``||logic:如果||``积木的最前面。

这是因为``||logic:如果||``在程序执行到此处时会从最前面的条件开始一级一级的判断，每一级判断将得到返回值"True"或"False"。

"False"意味着不符合条件，执行下一级判断，若到最后一条都不符合则退出退出整个``||logic:如果||``程序，"True"意味着符合条件，执行对应程序后立刻退出整个``||logic:如果||``程序，不再进行下一级的判断。

如果``||input:当按钮A被按下时||``条件被放置在前面，那么按钮AB被同时按下时，程序运行到此处将直接触发``||input:当按钮A被按下时||``条件执行程序并退出整个``||logic:如果||``程序，无法进展到对``||input:当按钮A+B被按下时||``条件进行判断。

## step 5

从``||radio:无线||``中将``||radio:无线电发送数字0||``积木作为满足条件时应执行的程序加入``||logic:如果为（）则||``积木中的每一级。

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        radio.sendNumber(0)
    } else if (input.buttonIsPressed(Button.A)) {
        radio.sendNumber(0)
    } else if (input.buttonIsPressed(Button.B)) {
        radio.sendNumber(0)
    } else {
        radio.sendNumber(0)
    }
})
```

## step 6

创建4个变量``||variables:stop||``,``||variables:go_foward||``,``||variables:turn_left||``,``||variables:turn_right||``。

在``||basic:当开机时||``中放置并设置``||variables:将stop设为0||``,``||variables:将go_foward设为1||``,``||variables:turn_left设为2||``,``||variables:turn_right设为3||``。

变量名在保证不与保留字和其他变量名（例如扩展积木使用的变量）重名的前提下可以随意我们设置。

```blocks
stop = 0
go_foward = 1
turn_left = 2
turn_right = 3
```

## step 7

将第六步创建的4个变量置入第五步操作所放置的4个``||radio:无线电发送数字0||``积木的可变量上，请参考提示。

```blocks
basic.forever(function () {
    if (input.buttonIsPressed(Button.AB)) {
        radio.sendNumber(go_foward)
    } else if (input.buttonIsPressed(Button.A)) {
        radio.sendNumber(turn_left)
    } else if (input.buttonIsPressed(Button.B)) {
        radio.sendNumber(turn_right)
    } else {
        radio.sendNumber(stop)
    }
})
```

## step 8

