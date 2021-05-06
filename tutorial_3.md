# 教程3：采集巡线检测电路的电压模拟信号

## step 1 @unplugged

本节教程将指导学员应用扩展积木来读取巡线检测电路传给micro:bit引脚的电压模拟信号，并通过USB串口将数据实时传输到PC终端，让我们可以通过串口工具读取到电压模拟信号。

## step 2

从 ``||serial:串行||`` 中把``||serial:向串口写入一行||``积木放至编辑区的``||basic:无限循环||``中。

```blocks
basic.forever(function () {
    serial.writeLine("")
})
```

## step 3

从``||text:文本||``中将``||text:组合字符串"你好" "世界"||``积木置入``||serial:向串口写入一行||``积木之中。

将``||text:组合字符串"你好" "世界"||``积木中的"你好"与"世界"两条文本内容删除。

```blocks
basic.forever(function () {
    serial.writeLine("" + "")
})
```

## step 4

复制``||basic:无限循环||``中的``||serial:向串口写入一行||``积木之中。

将复制出的积木放入``||basic:无限循环||``中。

``||text:组合字符串"" ""||``积木也会被一同复制。

```blocks
basic.forever(function () {
    serial.writeLine("" + "")
    serial.writeLine("" + "")
})
```
## step 5

在第一个``||serial:向串口写入一行||``中的``||text:组合字符串"" ""||``积木里的第一个编辑区内写入"Left:"。

在第二个``||serial:向串口写入一行||``中的``||text:组合字符串"" ""||``积木里的第一个编辑区内写入"Right:"。

```blocks
basic.forever(function () {
    serial.writeLine("Left:" + "")
    serial.writeLine("Right:" + "")
})
```

## step 6

从``||TriodeCar:TriodeCar||``中把``||TriodeCar:read left line tracking sensor||``积木置入第一个``||serial:向串口写入一行||``中的``||text:组合字符串"Left:" ""||``积木里的第二个编辑区内。

把``||TriodeCar:read left line tracking sensor||``积木置入第二个``||serial:向串口写入一行||``中的``||text:组合字符串"Right:" ""||``积木里的第二个编辑区内，并将其可选项改为"right"。

```blocks
basic.forever(function () {
    serial.writeLine("Left:" + triodecar.ReadLDR(triodecar.Patrol.PatrolLeft))
    serial.writeLine("Right:" + triodecar.ReadLDR(triodecar.Patrol.PatrolRight))
})
```

## step 7

将``||basic:暂停(ms)100||``积木放入``||basic:无限循环||``中的最下层。

```blocks
basic.forever(function () {
    serial.writeLine("Left:" + triodecar.ReadLDR(triodecar.Patrol.PatrolLeft))
    serial.writeLine("Right:" + triodecar.ReadLDR(triodecar.Patrol.PatrolRight))
    basic.pause(100)
})
```

## step 8

通过USB连接micro:bit,点击``|Download|``将程序下载进micro:bit。

现在每间隔100ms，micro:bit会将采集到的巡线检测电路的两路电压模拟信号转化为1024级精度的电压模拟值，再通过USB串口传输到PC终端。

将micro:bit插入TriodeCar，保持micro:bit与PC终端的连接，点击显示控制台，即可在makecode编辑器里查看USB串口传来的数据。

<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
