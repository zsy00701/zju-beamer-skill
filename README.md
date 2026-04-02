# ZJU Beamer Skill 🎓

> 浙江大学 LaTeX Beamer 演示文稿模板，封装为 **AI Agent 可自动调用的 Skill**。
>
> 只需一句话，AI 自动完成资源复制、内容生成、编译和预览，用户零操作。

## ✨ 特性

- 🏫 **浙江大学官方配色**（浙大蓝 RGB: 0, 63, 136）+ 校徽 Logo
- 📐 **16:9 宽屏**（默认，也支持 4:3）
- 🔤 **中英文混排**（xeCJK + ctex，开箱即用）
- 📊 **学术常用组件**：表格（booktabs）、流程图（TikZ）、代码高亮（listings）、彩色 Block
- 🤖 **AI Skill 全自动**：包含 `SKILL.md`，AI Agent 读取后自动完成资源复制 → 生成 tex → 编译 → 打开 PDF

## 📁 文件结构

```
zju-beamer-skill/
├── README.md               # 本文件
├── SKILL.md                # AI Agent 自动化使用指南 + Beamer 语法速查
└── resources/
    ├── zju_beamer.sty      # ZJU Beamer 样式文件
    └── figures/
        ├── background.png  # 幻灯片背景图
        ├── char.pdf        # "浙江大学" 矢量字样
        └── logo.pdf        # ZJU 校徽矢量图
```

## 🚀 快速开始

### 方式 A：作为 AI Skill 使用（推荐）

将本仓库引入你的项目后，只需对 AI Agent 说：

> "用浙大模板做一个关于 XXX 的 PPT"

AI 会自动：
1. 复制模板资源到 `presentation/` 目录
2. 根据你的需求生成 `main.tex`
3. 用 XeLaTeX 编译
4. 打开 PDF 预览

### 方式 B：手动使用

#### 1. 引入模板

```bash
# 作为 git submodule（推荐，便于更新）
git submodule add https://github.com/zsy00701/zju-beamer-skill.git skills/zju-beamer

# 或直接克隆
git clone https://github.com/zsy00701/zju-beamer-skill.git
```

#### 2. 复制资源

```bash
mkdir -p presentation/figures
cp skills/zju-beamer/resources/zju_beamer.sty presentation/
cp skills/zju-beamer/resources/figures/* presentation/figures/
```

#### 3. 编写 main.tex

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

\begin{frame}
    \frametitle{Outline}
    \tableofcontents
\end{frame}

\section{示例}
\begin{frame}{Hello ZJU}
    \begin{block}{浙江大学 Beamer 模板}
        这是一个示例页面。支持中英文混排。
    \end{block}
\end{frame}

\begin{frame}
    \begin{center}
        \vspace{2cm}
        {\Huge\bfseries Thank You}\\[1em]
        {\Large Questions \& Discussion}
    \end{center}
\end{frame}
\end{document}
```

#### 4. 编译 & 预览

```bash
cd presentation
xelatex -interaction=nonstopmode main.tex
xelatex -interaction=nonstopmode main.tex  # 第二次确保目录正确
open main.pdf
```

> ⚠️ **必须使用 XeLaTeX 编译**，不支持 pdfLaTeX。

## 🎨 主题切换

```latex
\zjusectioncolor{blue}   % 蓝色顶栏（默认）
\zjusectioncolor{black}  % 黑色顶栏
```

## 📖 Beamer 语法速查

详见 [SKILL.md](./SKILL.md)，包含：

| 语法 | 说明 |
|------|------|
| `columns` | 分栏布局 |
| `block` / `alertblock` / `exampleblock` | 彩色方框 |
| `\includegraphics` | 插入图片 |
| `tabular` + `booktabs` | 学术表格 |
| `tikzpicture` | 流程图 / 架构图 |
| `\textcolor{ZJUBlue}{...}` | 浙大蓝等自定义颜色 |
| `\ding{51}` / `\ding{55}` | ✓ / ✗ 符号 |

## 🖥️ 环境要求

| 项目 | 要求 |
|------|------|
| **TeX 发行版** | TeX Live 2022+ 或 MacTeX |
| **编译器** | XeLaTeX |
| **操作系统** | macOS / Linux / Windows |
| **编辑器建议** | VS Code + LaTeX Workshop（保存自动编译）|

## 🙏 参考资料 & 致谢

本模板基于以下开源项目，感谢原作者的贡献：

| 项目 | 作者 | 说明 |
|------|------|------|
| [ZJU-Beamer-Template](https://github.com/qychen2001/ZJU-Beamer-Template) | [qychen2001](https://github.com/qychen2001) (光头哥), [PhilFan](https://github.com/PhilFan) | 主要模板来源，提供 `zju_beamer.sty`、Logo 和背景资源 |
| [ZJU-beamer-template](https://github.com/pan2013e/ZJU-beamer-template) | [pan2013e](https://github.com/pan2013e) | 早期浙大 Beamer 模板参考 |
| [Beamer User Guide](https://ctan.org/pkg/beamer) | Till Tantau et al. | LaTeX Beamer 官方文档 |

## 📄 许可证

模板样式文件 `zju_beamer.sty` 遵循原项目许可：
- [LaTeX Project Public License (LPPL) v1.3c](https://www.latex-project.org/lppl.txt)
- 或 [GNU General Public License (GPL) v3](https://www.gnu.org/licenses/gpl-3.0.html)

其余文件采用 MIT License。

---

**Made with ❤️ for ZJU students and researchers.**
