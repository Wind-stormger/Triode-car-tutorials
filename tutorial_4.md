# 教程4：使用两块micro:bit通过无线电通讯控制电机

## step 1 @unplugged

基于micro:bit上集成的无线通信模块同时具备无线电收发的功能，我们可以使多块micro:bit之间建立无线连接，并可互相控制。

本节教程将指导学员在MakeCode中应用无线电扩展积木与TriodeCar扩展积木进行编程，使两块micro:bit之间建立无线电通讯并能互相控制，以此实现对TriodeCar的遥控。

较复杂的操作步骤将不再用文字逐步繁琐的描述，积木搭建参考提示即可，以对程序的讲解为主。

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

从``||radio:无线||``中将``||radio:无线电发送数字0||``积木作为满足条件时应执行的程序加入``||logic:如果为（）则||``积木中的每一级条件之下。

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

将第6步创建的4个变量置入第五步操作所放置的4个``||radio:无线电发送数字0||``积木的可变量上，请参考提示。

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

关于5，6，7步中将数值赋值给变量，再使无线电发送变量的数值这样看似繁琐的操作，实际有着很重要的意义，那就是将我们人为确定下的数值用变量的名称"代指"。

例如在无线电传输数据的时候，用变量名代指某个数值，有利于我们从认知上确定此时要发送出去的数值要与什么具体的功能关联，无需再花费精力去记忆抽象的数值，特别是在我们的程序愈发复杂，所要应用的数值不断增多的情况下，用变量代指数值将极大提高我们的效率且降低错误概率。

另外，在我们对与同一个功能关联的数值在程序中被多次调用时，若需要改换数值，直接修改变量的数值即可，再一次增强了我们编程的效率。

## step 9

从``||radio:无线||``中将``||radio:无线电设置组1||``积木放置到``||basic:当开机时||``中。

这块积木将告诉micro:bit应该在哪个无线电通讯频道中进行通讯，确保仅与此通讯频道相同的micro:bit之间能收发无线电讯息。

最后可以添加一个``||basic:显示图标||``积木在``||basic:当开机时||``的最后面，程序执行到这里即意味着``||basic:当开机时||``运行完毕，将开始执行``||basic:无限循环||``一类的程序。

```blocks
stop = 0
go_foward = 1
turn_left = 2
turn_right = 3
radio.setGroup(1)
basic.showIcon(IconNames.Heart)
```

## step 10

无线电通讯频道设置及无线电发送程序已经被我们完成了，现在则需要无线电接收程序来用于对TriodeCar的控制。

从``||radio:无线||``中将``||radio:在无线接收到数据时运行(receivedNumber)||``积木拖放至编辑区。

```blocks
radio.onReceivedNumber(function (receivedNumber) {
})
```

## step 11

对于接收程序，我们同样利用``||logic:如果为（）则||``积木来实现对接收到的无线电讯息进行判断的功能，将其加入``||radio:在无线接收到数据时运行(receivedNumber)||``中。

从``||logic:逻辑||``中将比较积木``||logic:0=0||``置入``||logic:如果为（）则||``积木的条件框中。

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (0 == 0) {
    	
    }
})
```

## step 11

鼠标点击并按住``||radio:在无线接收到数据时运行(receivedNumber)||``积木上的``||variables:receivedNumber||``块，将其拖拽到``||logic:0=0||``比较积木左侧数值框中，再将``||variables:stop||``积木放置在比较积木右侧数值框中。

将``||TriodeCar:let the car stop||``积木放置在此条件之下。

以此类推将第6步中创建的另外3个变量调用起来将积木完善，可参考提示。

```blocks
radio.onReceivedNumber(function (receivedNumber) {
    if (receivedNumber == stop) {
        triodecar.CarDirection(triodecar.direction.stop)
    } else if (receivedNumber == go_foward) {
        triodecar.CarDirection(triodecar.direction.foward)
    } else if (receivedNumber == turn_left) {
        triodecar.CarDirection(triodecar.direction.left)
    } else if (receivedNumber == turn_right) {
        triodecar.CarDirection(triodecar.direction.right)
    }
})
```

## step 12

将程序下载进两台micro:bit中，一块插在Triode-Car上，一块拿在手上，两块都接通电源，即可通过手上的micro:bit的按钮AB控制Triode-Car的电机启停。

可以思考一下把无线电讯息上传，无线电讯息接收与控制分成两个独立程序下载进两台micro:bit中，实现上位机与下位机的功能区分。