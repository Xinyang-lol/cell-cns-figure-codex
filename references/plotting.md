# 本地定量图的尺寸与导出

这是可按任务调整的 Matplotlib 基线。先核对输入数据和科学问题，再选择图型；不为适配模板改动真实数据。

## 尺寸、文字和颜色

用毫米定义最终物理尺寸，再换算为英寸。约 89 mm / 180 mm 仅作单栏 / 双栏初始宽度；目标期刊、图中信息量和用户指定尺寸优先。

最终尺寸的常用起点：正文与坐标标签 7–9 pt、面板字母 9–11 pt、线宽 0.6–1.0 pt。字体不可用时选择支持所需字符的相近字体，中文不能被缺字方框替代。

类别映射保持稳定。可从色盲友好的蓝 `#0072B2`、橙 `#E69F00`、绿 `#009E73`、朱红 `#D55E00` 与灰 `#777777` 中选择；不必每张图使用全部颜色。连续量用单调顺序色图，只有存在科学中点的有符号量才使用发散色图。

保留科学上必要的轴、单位、参考线和范围说明。柱状图应保留零基线；对数轴明确标记。不要将截断坐标轴或颜色范围用于夸大差异。

## 可编辑导出基线

```python
from pathlib import Path
import matplotlib as mpl
import matplotlib.pyplot as plt

out = Path("outputs")  # 当前工作区或用户指定的交付位置优先
out.mkdir(parents=True, exist_ok=True)
mm = 1 / 25.4

style = {
    "font.family": "sans-serif",
    "font.sans-serif": ["Arial", "Helvetica", "DejaVu Sans"],
    "font.size": 8,
    "axes.labelsize": 8,
    "xtick.labelsize": 7,
    "ytick.labelsize": 7,
    "legend.fontsize": 7,
    "axes.linewidth": 0.7,
    "lines.linewidth": 1.0,
    "svg.fonttype": "none",
    "pdf.fonttype": 42,
    "ps.fonttype": 42,
}

with mpl.rc_context(style):
    fig, ax = plt.subplots(figsize=(89 * mm, 65 * mm), layout="constrained")
    # 在这里从核对过的真实数据绘图；使用明确的轴标签与单位。
    ax.spines[["top", "right"]].set_visible(False)
    for fmt in ("svg", "pdf", "png"):
        fig.savefig(out / f"figure.{fmt}", dpi=300, facecolor="white")
    plt.close(fig)
```

保持所有格式的画布范围一致；需要准确物理尺寸时避免 `bbox_inches="tight"` 改变画布宽高，优先调整布局。字体选择影响中文支持，示例中的英文字体列表不能保证中文可用。

## 数据与统计表达

- 有少量观测点时展示原始数据；只画均值柱状图可能隐藏分布。
- 置信区间、SD、SEM 各自表达不同含义，用实际计算的结果并在图注注明。
- 统计标注对应实际比较、检验与多重比较处理。已有分析结果时沿用用户方法，不在绘图任务中无故替换统计模型。
- 缺失值、变换、归一化和排除标准应可追溯。保留输入文件，代码明确记录必要变换。
- 多面板比较使用可比较的范围；确需不同尺度时清楚标记。各面板统一类别颜色和顺序。

## 最终检查

查看导出的 PNG，以及必要时渲染的 SVG/PDF。检查所有标签、图例、误差线和面板字母的裁切、重叠与可读性。保存代码；矢量文字应保留为对象。大量散点或热图色块可以设 `rasterized=True`，但不要栅格化文字、坐标轴和图例。数据图之外的 AI 插画保持其真实栅格性质。
