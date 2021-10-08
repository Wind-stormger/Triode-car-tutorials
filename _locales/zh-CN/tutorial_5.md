```package
bluetooth
```

# 教程5：蓝牙控制

## step 1 @unplugged

本节教程将指导学员应用扩展积木与micro:bit蓝牙通信功能控制TriodeCar的电机启停及行进方向，使用具备蓝牙功能的移动设备如Apple或Android设备来对TriodeCar进行遥控。

## step 2

从``||Bluetooth:蓝牙||`` 中将``||Bluetooth:当蓝牙连接时||``积木放置到编辑区。

将``||basic:显示图标||``积木置入``||Bluetooth:当蓝牙连接时||``中。

```blocks
bluetooth.onBluetoothConnected(function () {
    basic.showIcon(IconNames.Heart)
})
```
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
