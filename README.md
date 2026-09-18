# Cell CNS Figure · Codex 原生版

在 Codex 中制作 Cell / Nature / Science 风格的科研图：真实数据图由本地 Python 绘制，机制图、科研插画和图形摘要使用 Codex 内置图像生成工具。

调用标识：`$cell-cns-figure`。

## 能做什么

- 根据研究摘要制作机制示意图、概念图或图形摘要。
- 从真实数据生成曲线、散点、箱线、热图等定量图。
- 统一多面板图的布局、配色、标签与单位。
- 修改现有科研图并检查科学关系、文字、裁切和可读性。
- 对本地数据图导出 SVG / PDF、PNG 预览与可复现绘图代码。

不调用小描、第三方中转或独立的 OpenAI API 客户端，也不要求填写 API Key。内置生图需要当前 Codex 环境提供相应工具，受账户正常用量限制；Python 绘图需要本地 Python 与任务实际使用的包。

## 安装

把下面这句话发给 Codex：

> 请从 https://github.com/Xinyang-lol/cell-cns-figure-codex 安装 cell-cns-figure。仓库根目录就是 skill，请保留 agents 和 references 目录。

也可以将仓库下载或克隆后，复制为用户 skill 目录中的 `cell-cns-figure` 文件夹：

- Windows：`%USERPROFILE%\.codex\skills\cell-cns-figure`
- macOS / Linux：`~/.codex/skills/cell-cns-figure`
- 如果配置了 `CODEX_HOME`，使用该目录下的 `skills/cell-cns-figure`。

保留完整目录结构。已有同名 skill 时，先比较并保留自己的修改。安装后，在下一条消息中调用；若客户端尚未刷新 skill 列表，重新加载会话。

## 使用示例

```text
$cell-cns-figure
根据下面的研究摘要，制作英文标签的机制示意图。
核心结论是……，已证实的关系是……，假说部分是……
```

```text
$cell-cns-figure
根据我提供的 CSV 绘制双面板科研图，保留原始观测点。
分组列为 treatment，结果列为 response，单位为 mg/L。
导出可编辑 SVG、PDF 和 PNG 预览，并保存绘图代码。
```

```text
$cell-cns-figure
修改这张图的文字和布局，保持实体、箭头方向和科学关系不变。
```

只有摘要、没有数值数据时，可以生成示意图；定量结果必须来自真实数据或明确标注的模拟数据。图像生成输出为栅格图，不冒充可编辑矢量。具体期刊投稿规格应以该期刊的官方指南为准。

## 文件结构

```text
SKILL.md                 核心工作流程和科学表达约束
agents/openai.yaml       Codex 显示名称、调用提示和发现策略
references/plotting.md   本地绘图的尺寸、字体、配色与导出基线
```

## 来源与许可证

由 [yrui-cmd/Cell_CNS_Figure](https://github.com/yrui-cmd/Cell_CNS_Figure) 改写为 Codex 原生流程。工作流已重写，本仓库不包含原版远程 API 客户端或其配置助手。

以 MIT 许可证发布，保留原项目版权声明，见 [LICENSE](LICENSE)。许可证适用于仓库中的说明与代码，不授予 Codex 服务使用额度，也不改变输入资料或生成内容的权利。
