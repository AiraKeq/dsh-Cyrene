# 第三方素材与组件声明 / Third-Party Notices

本仓库是一份**文档仓库**：只放文字与少量实机截图，**不附带任何**模型、视频、
精灵图等素材源文件。文中与截图中出现的一切第三方素材，版权归原作者所有，
各有各的授权约束 —— 这份声明把它一件一件说清楚。

若你是其中某条素材的作者、不希望它以任何形式出现在这里，请联系维护者移除。

---

## 1. Live2D 模型：Cyrene（昔涟）　← 本项目最重要的一条声明，因为它是别人的作品

| 项 | 内容 |
| --- | --- |
| 作者 | B 站 UP 主 **是依七哒** |
| 原始链接 | https://space.bilibili.com/457683484 |
| 获取渠道 | [Playa-Cyrene/Cyrene-Agent](https://github.com/Playa-Cyrene/Cyrene-Agent) 的 `dist/renderer/models/cyrene/`（该仓库随附 `MODEL_LICENSE.md`） |

**授权范围（作者已完全授权）：**

- ✅ 个人使用
- ✅ 修改表情、动作、物理参数
- ✅ 随（来源）仓库再分发
- ✅ 用于其他粉丝向衍生项目，**前提是署名原作者**

**限制：**

- ❌ **不得商用**。这既来自作者条款，也来自米哈游 / HoYoverse 的同人创作规范。
- ⚠️ 角色「昔涟 / Cyrene」及其形象、名称、设计的一切知识产权归 **HoYoverse / 米哈游**
  所有；本声明只涵盖模型的技术资产，**不授予任何角色 IP 的权利**。
- 本模型是**粉丝同人衍生作品**，与米哈游 / HoYoverse 无隶属关系，未获其背书。

**本项目的遵守方式**：模型文件不纳入版本控制，由使用者在本地运行
`tools/fetch-cyrene-model.ps1` 自行获取 —— 让「再分发」发生在来源仓库（Cyrene-Agent），
而不是让本项目成为素材的分发点。

---

## 2. 精灵图：昔涟 spritesheet（历史方案 / 回退路径）

| 项 | 内容 |
| --- | --- |
| 作者 | codex-pet.org 上的 **lincat**（[codex-pet.org/zh/pets/xilian](https://codex-pet.org/zh/pets/xilian/)） |
| 性质 | 粉丝同人作品；**不得商用、不得再分发** |

现役方案是 §1 的 Live2D 模型；精灵图保留在本地仅作回退与对照。本仓库不附带。

---

## 3. 开机动画素材（视频与音频）

| 项 | 内容 |
| --- | --- |
| 来源 | Steam 创意工坊（Wallpaper Engine，app id 431960）物品 **3644069061**，Web 型壁纸 |
| 作者 | B 站「**星海昔涟**」 |
| 物品页 | https://steamcommunity.com/sharedfiles/filedetails/?id=3644069061 |
| 文件 | `intro.webm`（开场，4K）/ `loop.webm`（循环，4K）/ `intro.wav` / `loop.wav` / `atmos_loop.wav` |

素材**未获**再分发授权：在本机订阅、本地使用。**「能给自己用」不等于「能替作者转发」。**
本仓库不附带任何视频 / 音频文件；README 截图（`assets/splash-intro.jpg`）仅用于说明效果。

---

## 4. 退场片段（touch.webm）

| 项 | 内容 |
| --- | --- |
| 来源 | 《崩坏：星穹铁道》3.7 版本「昔涟开门动画」（游戏启动画面）的**官方录屏** |
| 制作链 | 从无水印录屏切 23 帧（29.97fps，约 0.77s）→ 逐帧去水印 → 本地超分（realesr-animevideov3 ×2 → 3840×2160）→ VP9 编码 |
| 权利 | 画面版权归 **miHoYo / HoYoverse**；仅本机自用，不随仓库分发 |

README 中的 `assets/splash-exit.jpg` 即该片段的一帧（4K 超分母版），
仅作同人制作流程展示，不用于任何商业用途。

---

## 5. 运行时依赖（渲染链）

| 组件 | 许可 | 用途 |
| --- | --- | --- |
| [Electron](https://www.electronjs.org/) | MIT | 桌面应用外壳（桌宠与开机动画共用同一份运行时） |
| [pixi.js](https://pixijs.com/) `^7.3.0` | MIT | WebGL 渲染 |
| [pixi-live2d-display](https://github.com/guansss/pixi-live2d-display) `0.5.0-beta` | MIT | Live2D 模型的 pixi 适配层 |
| `live2dcubismcore.min.js` | [Live2D Open Software License](https://www.live2d.com/eula/live2d-open-software-license-agreement_en.html) | Cubism 运行时（年营收超 1000 万日元者须另行取得发行许可） |

版本组合**照抄 Cyrene-Agent 的 `package.json`**，不自行挑选 —— 那是已验证可用的组合。

---

## 6. 参考实现与代码来源

- **上游 DeskPet 仓库**（[wind-001/dsh-xilian-pet](https://github.com/wind-001/dsh-xilian-pet)，MIT）：
  桌宠的代码基座。手记中的代码节选取自其本机分支上的实跑版本（含本项目改动）；
  其中引用的上游代码版权归上游，随 MIT 许可。
- **[ayangweb/BongoCat](https://github.com/ayangweb/BongoCat)**（Apache-2.0）：
  只借鉴设计结论（窗口几何、输入状态避免卡键、模型交互），**未复制其代码**
  （它用 Rust 编写，与本项目的 JavaScript 无共用代码）。
- **Cyrene-Agent**：渲染三件套版本组合与模型的出处（见 §1）。

---

## 7. README 截图说明

`assets/` 下三张截图截自作者本机实跑的成品，其中包含上述各条素材的画面。
它们仅用于说明制作效果，版权归各原作者 / miHoYo / HoYoverse，
不使用于任何商业用途；如原作者有异议，请联系移除。

---

## 8. 本仓库内容的许可

文档文字与代码节选：**CC BY-NC-SA 4.0**（见 [LICENSE](LICENSE)）。
第三方素材与运行时依赖**不在该授权范围内**，各自条款以上文为准。
