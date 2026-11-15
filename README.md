# PCL CHCE

> **第三方基于 PCL（Plain Craft Launcher）源代码独立进行二次创作的修改版。**
> 本项目不是 PCL 官方版本，不是官方后续作品，与龙腾猫跃及 PCL 官方发布渠道无隶属关系。
> 名称含义：`PCL`（Plain Craft Launcher 的开头）+ `CHCE`（本项目自有的修改版标识）。

基于 [Meloong-Git/PCL](https://github.com/Meloong-Git/PCL) 的 tag `2.14.0.0`
（commit `ade6e04c6eab65e945b0fc51faae1ba8e714245c`，2026-10-16）——即 `2.99.0.0` 因合规原因关闭 Minecraft 下载功能之前的最后一个版本。
游戏本体、Mod、整合包的下载与安装功能按原版保留；启动、登录、版本隔离、联机等功能均未改动。

## 更新方式

**PCL CHCE 不提供自动更新**：不检查新版本、不联网获取新版程序、不替换自身 exe。
设置页与关于页的「检查更新」入口、`--update` 启动参数、自定义事件【检查更新】、
相关的更新设置项与提示文案均已移除。新版由发布渠道直接分发 `.exe` 文件，用户手动覆盖即可。

## 本版相对 2.14.0.0 的改动

| 类别 | 内容 |
| --- | --- |
| 名称 | 窗口标题、单实例查找标题、程序集标题、关于页软件名 → `PCL CHCE`；关于页标注「第三方基于 PCL 独立二次创作」 |
| 更新 | 移除上述全部自动更新入口；整合包导出改为复制当前运行的 exe，不再联网下载官方最新版 |
| 其余 | 功能逻辑、下载模块、User-Agent、LICENCE、作者署名与赞助入口一律原样 |

**刻意未改的部分**（改动会破坏兼容性或违反分发规则）：
- `AssemblyProduct` 仍为 `Plain Craft Launcher`（`ModModpack.vb` 用它识别自身 exe）
- 程序集名 / 资源 URI / 输出 exe 仍为 `Plain Craft Launcher 2`，配置目录与原版兼容
- `MeloongCore` 子模块已实体化为普通目录，`.gitmodules` 已移除，可直接 push 到本仓库

## 编译

有两种方式，详见仓库内 [`BUILD-NOTES.md`](BUILD-NOTES.md)：

- **零本地占用**：push 到 GitHub 后由 `.github/workflows/build.yml` 在 `windows-2022` runner 上编译，从 Actions 的 Artifacts 下载 `PCL CHCE.exe`。本地不装 Visual Studio，C 盘无需空间。
- **本地编译**：Windows + VS 2022（17.8+）+ .NET Framework 4.8 目标包，把 `build.bat` 放在本仓库根目录双击，产物在 `dist\PCL CHCE.exe`。

两种都走 **Release / Any CPU** 的整解决方案生成。Release 是硬性要求：`McLaunchPrecheck` 的正版购买劝导与赞助劝导仅在 `BuildType = Release` 时执行。

- 目标框架：v4.8；WPF / VB.NET 项目，必须在 Windows 上构建
- 产物是单文件 exe（依赖 DLL 已嵌入 `Resources.resx`，运行时 `AssemblyResolve` 加载），分发时不要附带任何 dll
- 开源版缺少的密钥仍按原版方式从环境变量读取：`PCL_MS_CLIENT_ID`（微软登录）、`PCL_CURSEFORGE_API_KEY`（CurseForge）

## PCL 分发规则对照（重度使用）

| 规则 | 本仓库状态 |
| --- | --- |
| 明确表示为第三方基于 PCL 独立二次创作 | README 顶部 + 关于页软件信息已标注 |
| 名称以 Plain Craft Launcher (PCL) 开头，后缀表明第三方修改 | `PCL CHCE` |
| 关于页首位保留龙腾猫跃署名及赞助链接，公开源代码，继续附带本 LICENCE | 原样保留；本仓库公开；根目录 `LICENCE` 未改动 |
| 保留与 `McLaunchPrecheck` 一致的正版购买劝导与赞助劝导 | 原样保留，未削弱 |
| Windows 下不得有类似 PCL 赞助解锁的功能或表现，界面主色相保持蓝色 | 未添加任何赞助/解锁入口；`ColorHue = 210`（蓝色）未改动 |

关于页「赞助 PCL !」按钮原样指向 PCL 原作者的赞助页面。
**本项目没有、也不会添加本项目维护者本人的赞助链接或收款入口。**

## 许可与风险提示

- 许可为根目录 `LICENCE` 中的《PCL 分发有限许可》与《PCL 存储库合理使用指南》，
  **不是 MIT**；衍生使用请完整阅读该文件。LICENCE 原样保留，未作任何修改。
- PCL 官方自 `2.99.0.0`（2026-10-20）起以「为遵守相关法律法规」为由不再提供 MC 下载功能。
  本仓库基于其前一版本，保留了该下载能力；公开发布与分发前请自行评估所在地区的合规风险，
  并自行承担相应责任。
- 请勿将本项目描述为官方版本、官方续作或由原作者维护。

## 致谢

原作者 **龙腾猫跃**（LTCatt）、协力开发者 HerobrineXia，以及 Meloong-Git/PCL 的所有贡献者。
PCL CHCE 仅在其公开源码基础上做了上表列出的修改。

---

以下为原仓库 README 原文：

# Plain Craft Launcher

[![Stars](https://img.shields.io/github/stars/Meloong-Git/PCL?style=flat&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZlcnNpb249IjEiIHdpZHRoPSIxNiIgaGVpZ2h0PSIxNiI+PHBhdGggZD0iTTggLjI1YS43NS43NSAwIDAgMSAuNjczLjQxOGwxLjg4MiAzLjgxNSA0LjIxLjYxMmEuNzUuNzUgMCAwIDEgLjQxNiAxLjI3OWwtMy4wNDYgMi45Ny43MTkgNC4xOTJhLjc1MS43NTEgMCAwIDEtMS4wODguNzkxTDggMTIuMzQ3bC0zLjc2NiAxLjk4YS43NS43NSAwIDAgMS0xLjA4OC0uNzlsLjcyLTQuMTk0TC44MTggNi4zNzRhLjc1Ljc1IDAgMCAxIC40MTYtMS4yOGw0LjIxLS42MTFMNy4zMjcuNjY4QS43NS43NSAwIDAgMSA4IC4yNVoiIGZpbGw9IiNlYWM1NGYiLz48L3N2Zz4=&logoSize=auto&label=Stars&labelColor=444444&color=eac54f)](https://github.com/Meloong-Git/PCL/)
[![Issues](https://img.shields.io/github/issues/Meloong-Git/PCL?style=flat&label=Issues&labelColor=444444&color=1F883D)](https://github.com/Meloong-Git/PCL/issues)
[![哔哩哔哩](https://img.shields.io/badge/动态-BiliBili-00A4DB?style=flat&labelColor=444444&logoSize=auto)](https://space.bilibili.com/11343203/dynamic)
[![爱发电](https://img.shields.io/badge/赞助-爱发电-946ce6?style=flat&labelColor=444444&logoSize=auto)](https://meloong.com/afd/a/LTCat)

包含 PCL 的大部分源代码，包括 UI 库、动画模块、下载模块、Minecraft 启动模块等！<br/>
代码并不是实时更新的，它会在每次 PCL 发布更新时同步一次。<br/>
非常感谢社区的大力支持！

<br/>

### 相关资源
- [PCL 下载](https://meloong.com/pcl)：下载可免费使用的正式版 PCL！
- [PCL 功能投票](https://github.com/Meloong-Git/PCL/discussions/2)：来参加投票吧，开发者会优先处理票数较高的项目！
- [帮助文档库](https://github.com/LTCatt/PCL2Help)：PCL 内置帮助文档的存储库
