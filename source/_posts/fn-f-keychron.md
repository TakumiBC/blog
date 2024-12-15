---
title: 使用键盘宏解决 Fn + F 快捷键在 Mac 第三方键盘失效的问题
license: all_rights_reserved
abbrlink: 2018365746
date: 2024-12-15 21:15:00
---

## 缘由

一个月之前过生日的时候，[@ZigaoWang](https://github.com/ZigaoWang) 送了一个 Keychron K2 Max 香蕉轴给我。

然而，我在 Mac 上常用的全屏快捷键 Fn + F 竟然失效了。

深入研究后，我发现这是因为 Mac 只会将来自 Apple 自家键盘的 Fn 键视为 Globe 修饰键，而对于第三方键盘则会直接自动忽略。

解决方法是设置一个键盘宏，将 Fn + F 映射为 Command + Control + F。

## 具体步骤

首先，将 Keychron K2 Max 通过 USB-C 数据线连接到 Mac 上，并将键盘开关切换到 Cable 模式。

然后，打开 [Keychron Launcher](https://launcher.keychron.com/)，选择自己的键盘并连接，然后选择左边的 Macro。

![](https://www.takumibc.com/CleanShot_2024-12-15_at_21.13.29@2x.png)

紧接着，录制一个鼠标宏，比如我使用 M0 作为示范，内容为：

```
{+KC_LGUIX+KC_LCTLX+KC_FX-KC_LGUIK-KC_LCTLX-KC_F}
```

即按下左 Control 键、左 Command 键和 F 键，然后松开这三个键，并点击 Submit 按钮。

![](https://www.takumibc.com/CleanShot_2024-12-15_at_21.13.39@2x.png)

然后，点击左边的 Keyboard，选择 Layer 1，并将 F 键映射为对应的鼠标宏（此处即为 M0）。

大功告成，Enjoy～