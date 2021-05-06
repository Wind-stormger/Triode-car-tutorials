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