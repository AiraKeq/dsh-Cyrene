# 昔涟桌宠与开机动画 · 制作手记

> **Making-of**: a Cyrene (昔涟) Live2D desktop pet & a full-screen boot splash,
> built with Electron + pixi-live2d-display on Windows.

一只会眨眼、视线会跟着光标、点她会应的 **Live2D 桌宠**；一段盖住应用启动等待的
**全屏开机动画**（开机最先起、点掉才见界面）。这个仓库是两件成品的**完整制作手记**：
每一步走法、踩到的坑、可以直接抄的模板 —— 写给「想照着做一份的人」。

| 桌宠 · 悬浮在桌面 | 开机动画 · 全屏播放中 | 退场片段 · 4K 帧 |
| --- | --- | --- |
| ![桌宠](assets/pet.png) | ![开机动画](assets/splash-intro.jpg) | ![退场片段](assets/splash-exit.jpg) |

> 截图截自作者本机实跑的成品；画面中所含素材的版权与出处见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

## 成品速览

| | 桌宠 | 开机动画 |
| --- | --- | --- |
| 形态 | Electron 无边框 / 透明 / 置顶小窗，Live2D Cubism 4 渲染（精灵图保留为回退路径） | Electron 全屏窗，**两层画面 + 三路声音** |
| 交互 | 视线跟光标、点她有反应、右键动作菜单、拖动带边界钳制 | 点击或按 Esc 触发退场（收手 → 托星 → 白光 → 花瓣 → 淡窗）；不点则 5 分钟后自动进 |
| 联动 | 读共享文件感知任务状态（不依赖宿主进程，可单独跑） | 盖的是「界面还没起来」那段等待 —— 界面在背后并行打开，**看动画不是额外等待** |
| 关键点 | `pet://` 协议、命中区判定搬进主进程、画布即画框 | `splash.cmd` 独占锁、窗口生来 `setOpacity(0.99)`（防遮挡停渲染） |

两件事的共同点：Electron 窗口 + 素材 + 一段时序编排。踩的坑有一半同源 ——
Windows 窗口行为、DPI 三坐标系、Chromium 渲染与遮挡、还有各种静默失败。

## 文档导航

| 文档 | 内容 |
| --- | --- |
| **[docs/制作手记.md](docs/制作手记.md)** | **主文档**：成品一览 / 桌宠篇（渲染链、取景、交互、动作菜单）/ 开机动画篇 / 经验总结 / 坑点速查表 / 当模板用 / 文件地图 / 工具库与教程 |
| [docs/本地部署记录.md](docs/本地部署记录.md) | 原始时间线（1600+ 行）：谁在第几轮踩了什么、哪次误判怎么纠正的 |
| [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) | 素材出处与授权（模型 / 精灵图 / 壁纸 / 录屏 / 依赖）—— **署名与再分发边界看这份** |
| [assets/](assets/) | README 用的少量实机截图 |

## 想复刻？按这个顺序走

1. **先读手记第一、二节** —— 成品长什么样、住在哪、渲染链怎么搭。
2. **素材从哪来、哪些能动**：先读 `THIRD_PARTY_NOTICES.md`。壁纸与录屏素材
   **未获再分发授权**，本仓库不附带任何素材源文件。
3. **配环境**：照手记 8.1 的依赖表（Electron / pixi.js / pixi-live2d-display /
   Cubism Core），**版本组合照抄、别追新**。
4. **遇到怪事翻第五节的坑点速查表**：取景、拖动、全屏、遮挡、静默失败，
   症状 → 病因 → 出处都列好了。

## 仓库结构

```
xilian-making-of/
├── README.md
├── LICENSE                    # CC BY-NC-SA 4.0（文档内容；不含第三方素材）
├── THIRD_PARTY_NOTICES.md     # 素材出处与授权声明
├── assets/                    # 实机截图（3 张）
│   ├── pet.png
│   ├── splash-intro.jpg
│   └── splash-exit.jpg
└── docs/
    ├── 制作手记.md            # 主文档（提炼版 + 真源码节选）
    └── 本地部署记录.md        # 原始时间线
```

> 源码不在本仓库：桌宠的代码基座是上游 DeskPet 项目，手记里给出了关键环节的
> 真源码节选，够把路子看明白。
> 文中所有路径、尺寸以作者本机（Windows 11，2560×1600 @150%）为例，换机器按自己的改。

## 出处与致谢

这两件东西站在这些作品和项目上（完整条款见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)）：

- **Live2D 模型**：B 站 UP 主「**是依七哒**」制作
  （[space.bilibili.com/457683484](https://space.bilibili.com/457683484)），
  经 [Playa-Cyrene/Cyrene-Agent](https://github.com/Playa-Cyrene/Cyrene-Agent) 分发。
- **开机动画素材**：Steam 创意工坊壁纸（Wallpaper Engine，物品 3644069061），
  作者 B 站「**星海昔涟**」。
- **退场片段**：取自《崩坏：星穹铁道》3.7「昔涟开门动画」的官方录屏（仅本机自用）。
- **上游项目**：DeskPet（[wind-001/dsh-xilian-pet](https://github.com/wind-001/dsh-xilian-pet)，
  MIT，桌宠代码基座）；[ayangweb/BongoCat](https://github.com/ayangweb/BongoCat)
  （Apache-2.0，窗口几何与输入状态的设计参照）。
- **渲染链**：[guansss/pixi-live2d-display](https://github.com/guansss/pixi-live2d-display)
  （MIT）+ Live2D Cubism SDK。

角色「昔涟 / Cyrene」及其形象、名称、设计的一切知识产权归 **HoYoverse / 米哈游** 所有。
本项目为**粉丝向、非商业**衍生作品，与米哈游无隶属关系、未获其背书。
截图与文档中出现的第三方素材版权归各原作者，仅作同人制作展示；
**如有作者不希望自己的作品出现在这里，请联系维护者移除。**

## 许可

本仓库的**文字与代码节选**（文档内容）采用
[CC BY-NC-SA 4.0](LICENSE)（署名 · 非商用 · 相同方式共享）。
文中引用的第三方代码版权归各自项目、随其原许可（如上游 DeskPet 为 MIT）。
第三方素材与依赖不在此授权范围内 —— 见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。
