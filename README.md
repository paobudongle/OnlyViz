# OnlyViz

OnlyViz 是装在本机的、可供智能体调用的数据作图软件，支持 Codex、DeepSeek harness、Hermes 等直接调用。也可以打开 CSV、JSON 或 Excel 出图；解析与渲染都在本机完成。图表存成一份自包含的 `.onlyviz` 文档，双击即可在桌面应用里还原数据和配置。

智能体负责选图和落文档，人负责最后一版。

## 下载（v0.1.0）

| 平台 | 安装包 |
|------|--------|
| Windows（x64） | [OnlyViz_0.1.0_x64-setup.exe](./OnlyViz_0.1.0_x64-setup.exe) |
| Linux（amd64，Debian/Ubuntu） | [OnlyViz_0.1.0_amd64.deb](./OnlyViz_0.1.0_amd64.deb) |

### 安装

**Windows：** 运行 `OnlyViz_0.1.0_x64-setup.exe`。

**Linux：**

```bash
sudo dpkg -i OnlyViz_0.1.0_amd64.deb
sudo apt-get install -f   # 若缺少依赖
```

安装后，`onlyviz-cli` 会出现在 PATH 中（CLI 需要 Node.js 18+）。

## 能做什么

- **本地优先。** 文件在本机读取与渲染，无需云端账号，不上传数据。
- **便携图文档。** `.onlyviz` 内含图类型、字段映射、样式，以及重绘所需的数据行。双击或拖进 OnlyViz 即可还原。
- **60+ 图型。** 折线、柱状、散点、饼图、桑基、热力、甘特、K 线、漏斗、子弹图，以及箱线、小提琴、蜂群、QQ、残差、累积分布、自相关、火山图、控制图等统计图。分组柱与箱线支持误差棒和显著性括号。
- **人与智能体同一条路径。** Codex、Claude、DeepSeek harness、Hermes 等能在本机执行命令的智能体，直接调用 `onlyviz-cli`：查图类型、映射列、生成并校验 `.onlyviz`，再把文件路径交回对话。你在桌面应用里打开该文件，调样式并导出 PNG/JPEG。

## 智能体调用流程

```bash
onlyviz-cli charts
onlyviz-cli params scatter
onlyviz-cli create \
  --data data.csv \
  --chart scatter \
  --map x_axis=height,y_axis=weight \
  --title "身高 vs 体重" \
  --out figures/scatter_demo.onlyviz
onlyviz-cli validate figures/scatter_demo.onlyviz
```

1. 用 `charts` / `params` 查看图类型、必填字段和样式选项。
2. 用 `create` 与 `--map` 写出 `.onlyviz` 文件。
3. 用 `validate` 检查必填字段、列名和嵌入行数。
4. 在 OnlyViz 中打开该文件，完成样式调整并导出图片。

## 隐私

解析、聚合与渲染均在本机完成。智能体调用的是本机 CLI 或本机 HTTP 接口（默认 `127.0.0.1:3921`），数据不会发往在线作图服务。

## 许可证

MIT

英文说明见 [readme.en.md](./readme.en.md)。开发与构建说明见 [readme.dev.md](./readme.dev.md)。
