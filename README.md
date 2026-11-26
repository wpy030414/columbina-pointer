# Columbina Pointer

面向 Windows 的《原神》哥伦比娅主题鼠标指针方案，提供**原版**与**像素化**两种风格，共两套独立方案。

> 图像为同人作品，版权归原权利方所有，仅供个人使用。

## 目录结构

```
.
├── Columbina/              # 原版风格（17 个 .ani）
│   ├── #InstallMe.inf
│   └── *.ani
└── Columbina.Pixelized/    # 像素化风格（17 个 .ani，格子更粗、体积更小）
    ├── #InstallMe.inf
    └── *.ani
```

两套方案的文件名、inf 结构与槽位映射完全一致，仅图像内容与方案身份不同，便于对照维护。

## 安装

1. 将整个方案目录（不要只拷贝 `.ani`）放到任意位置。
2. 在资源管理器中**右键 `#InstallMe.inf` → 安装**。
3. 安装过程会：
   - 把 17 个 `.ani` 复制到 `%SystemRoot%\Cursors\Columbina`（或 `Cursors\Columbina.Pixelized`）；
   - 在注册表 `HKCU\Control Panel\Cursors\Schemes` 下注册方案；
   - 直接写入当前指针设置并弹出「鼠标属性」窗口确认。

卸载：在「鼠标属性 → 指针」中选回默认方案，再删除 `%SystemRoot%\Cursors\` 下对应目录，并清除注册表 `Schemes` 中同名项。

## 槽位映射

| 注册表键 | 角色 | 文件 |
| --- | --- | --- |
| `Arrow` | 正常选择 | `Normal.ani` |
| `Help` | 帮助选择 | `Help.ani` |
| `AppStarting` | 后台运行 | `Working.ani` |
| `Wait` | 忙 | `Busy.ani` |
| `Crosshair` | 精确选择 | `Precision.ani` |
| `IBeam` | 文本选择 | `Text.ani` |
| `NWPen` | 手写 | `HandWriting.ani` |
| `No` | 不可用 | `Unavailable.ani` |
| `SizeNS` | 垂直调整 | `Vertical.ani` |
| `SizeWE` | 水平调整 | `Horizontal.ani` |
| `SizeNWSE` | 沿对角线调整 1 | `Diagonal1.ani` |
| `SizeNESW` | 沿对角线调整 2 | `Diagonal2.ani` |
| `SizeAll` | 移动 | `Move.ani` |
| `UpArrow` | 候选 | `Alternate.ani` |
| `Hand` | 链接选择 | `Link.ani` |
| `Pin` | 位置选择 | `Pin.ani` |
| `Person` | 个人选择 | `Person.ani` |

## inf 说明

两套 `#InstallMe.inf` 均为 CRLF 编码、结构相同，差异仅限：

- `SCHEME_NAME`：`Columbina` / `Columbina Pixelized`
- `CUR_DIR`：`Cursors\Columbina` / `Cursors\Columbina.Pixelized`
- `[SourceDisksNames]` 的描述文本

段落职责：

| 段落 | 职责 |
| --- | --- |
| `[SourceDisksNames]` / `[SourceDisksFiles]` | 声明随 inf 一起分发的光标文件 |
| `[Scheme.Cur]` | 复制到目标目录的文件清单 |
| `[Scheme.Reg]` | 在「指针」方案列表中注册整套方案 |
| `[Wreg]` | 写入当前指针并刷新「鼠标属性」面板 |

## 已知限制

- `.inf` 安装需要管理员权限（`HKLM` 写入 Runonce 项）。
- 修改图像文件后需保持文件名不变或同步修改 inf 三处清单（`[SourceDisksFiles]`、`[Scheme.Cur]`、`[Strings]`）。
