# ZJU Beamer Skill 🎓

浙江大学 LaTeX Beamer 演示文稿模板，封装为 AI Agent 可调用的 Skill。

## 预览

| 封面 | 正文 |
|:---:|:---:|
| 浙大蓝渐变顶栏 + 校徽 Logo | Block / 表格 / TikZ 图 |

## 特性

- 🏫 **浙江大学官方配色**（浙大蓝 RGB: 0, 63, 136）
- 📐 **16:9 宽屏**（默认，也支持 4:3）
- 🔤 **中英文混排**（xeCJK + ctex）
- 📊 **学术常用组件**：表格（booktabs）、流程图（TikZ）、代码高亮（listings）
- 🤖 **AI Skill 格式**：包含 `SKILL.md`，可被 AI 编程助手自动识别和调用

## 快速开始

### 1. 克隆到你的项目

```bash
# 方式 A：作为 git submodule（推荐）
git submodule add https://github.com/zsy00701/zju-beamer-skill.git skills/zju-beamer

# 方式 B：直接克隆
git clone https://github.com/zsy00701/zju-beamer-skill.git
```

### 2. 创建演示文稿

```bash
mkdir -p presentation/figures
cp skills/zju-beamer/resources/zju_beamer.sty presentation/
cp skills/zju-beamer/resources/figures/* presentation/figures/
```

### 3. 编写 main.tex

```latex
\PassOptionsToPackage{quiet}{fontspec}
\documentclass[10pt,aspectratio=169]{beamer}
\usepackage{zju_beamer}
\graphicspath{{./figures/}}
\zjusectioncolor{blue}

\title[短标题]{完整标题}
\subtitle{副标题}
\author[Author]{作者名}
\institute[ZJU]{浙江大学}
\date{\today}

\begin{document}
\begin{frame}
    \titlepage
\end{frame}

\section{示例}
\begin{frame}{Hello ZJU}
    \begin{block}{浙江大学 Beamer 模板}
        这是一个示例页面。
    \end{block}
\end{frame}
\end{document}
```

### 4. 编译

```bash
cd presentation
xelatex -interaction=nonstopmode main.tex
xelatex -interaction=nonstopmode main.tex  # 第二次确保目录正确
open main.pdf
```

> ⚠️ **必须使用 XeLaTeX 编译**，不支持 pdfLaTeX。

## 文件结构

```
zju-beamer-skill/
├── README.md               # 本文件
├── SKILL.md                # AI Agent 使用说明（含完整语法速查）
└── resources/
    ├── zju_beamer.sty      # ZJU Beamer 样式文件
    └── figures/
        ├── background.png  # 幻灯片背景图
        ├── char.pdf        # "浙江大学" 矢量字样
        └── logo.pdf        # ZJU 校徽矢量图
```

## 常用语法

详见 [SKILL.md](./SKILL.md)，包含：

- 分栏布局（columns）
- 彩色方框（block / alertblock / exampleblock）
- 插入图片、表格
- TikZ 流程图模板
- 自定义颜色（浙大蓝 + 辅助色）
- 特殊符号（✓ ✗ ★）

## 主题切换

```latex
\zjusectioncolor{blue}   % 蓝色顶栏（默认）
\zjusectioncolor{black}  % 黑色顶栏
```

## 环境要求

- **TeX 发行版**：TeX Live 2022+ 或 MacTeX
- **编译器**：XeLaTeX
- **编辑器建议**：VS Code + LaTeX Workshop 插件（保存自动编译）

## 参考资料 & 致谢

本模板基于以下开源项目，感谢原作者的贡献：

| 项目 | 作者 | 说明 |
|------|------|------|
| [ZJU-Beamer-Template](https://github.com/qychen2001/ZJU-Beamer-Template) | [qychen2001](https://github.com/qychen2001) (光头哥), [PhilFan](https://github.com/PhilFan) | 主要模板来源，提供 `zju_beamer.sty`、Logo 和背景资源 |
| [ZJU-beamer-template](https://github.com/pan2013e/ZJU-beamer-template) | [pan2013e](https://github.com/pan2013e) | 早期浙大 Beamer 模板参考 |
| [Beamer User Guide](https://ctan.org/pkg/beamer) | Till Tantau et al. | LaTeX Beamer 官方文档 |

### 许可证

模板样式文件 `zju_beamer.sty` 遵循原项目许可：
- [LaTeX Project Public License (LPPL) v1.3c](https://www.latex-project.org/lppl.txt)
- 或 [GNU General Public License (GPL) v3](https://www.gnu.org/licenses/gpl-3.0.html)

## License

MIT © [zsy00701](https://github.com/zsy00701)
