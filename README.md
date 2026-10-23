# 屏幕自由 ScreenUnlock

一个 Android Xposed（LSPosed）模块：解除受保护界面的截图与录屏限制，屏蔽系统下发的截图、录屏检测回调，并隐藏 OPPO 互联投屏在系统里留下的公开显示设备。

## 关于原仓库

本项目基于 [LSPosed/DisableFlagSecure](https://github.com/LSPosed/DisableFlagSecure)（现名 Enable Screenshot）二次开发，遵循上游的 GPL-3.0 许可证。

上游解决的是「内容能不能被截到」：解除 `FLAG_SECURE`、强制捕获安全图层、屏蔽各家 ROM 的截图拦截判断。本项目保留其全部能力，并补充了一项上游没有覆盖的方向——「屏幕正在共享」这件事本身的可观测性。

此外，ColorOS 17 的 Oplus 私有类截图判定改动，其类名与方法签名的实证来源是社区仓库 [a422015028/screenshot](https://github.com/a422015028/screenshot)，详见「与上游的差异」对应章节的声明。

## 功能

- **解除截图限制**：让设置了 `FLAG_SECURE` 的窗口可以被截图、录屏采集到内容
- **屏蔽截图检测**：切断 `ActivityTaskManagerService#registerScreenCaptureObserver`，Android 14+ 的截图回调不再通知应用
- **屏蔽录屏检测**：切断 `WindowManagerService#registerScreenRecordingCallback`，Android 15+ 的录屏回调不再通知应用
- **隐藏 OPPO 互联投屏显示**：把投屏创建的虚拟屏标记为私有，第三方应用无法枚举到它
- **厂商适配**：OPPO、小米 HyperOS、三星 OneUI、魅族的截图流程同步处理

## 支持范围

- Android 12 至 17
- 小米 HyperOS
- OPlus OS（ColorOS、Realme UI、OxygenOS）
- 三星 One UI
- **不支持**自定义 ROM
- **不支持**非官方 LSPosed 构建

隐藏投屏显示仅覆盖 `com.oplus.cast`。其他投屏方式（USB 有线、第三方投屏应用、其他厂商互联工具）仍会暴露公开虚拟屏。

该特性在 OPPO 设备（Android 17）上验证通过：投屏画面与系统状态正常，第三方应用枚举不到该显示。其余能力继承自上游，验证范围以上游为准。


## 许可

[GNU GPL v3](LICENSE)  

上游版权归 LSPosed 贡献者所有。
