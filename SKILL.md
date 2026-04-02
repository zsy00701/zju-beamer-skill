---
name: zju-beamer
description: 使用浙江大学 Beamer 模板创建学术 PPT 演示文稿
---

# ZJU Beamer 模板 Skill

## 概述

使用浙江大学官方配色的 LaTeX Beamer 模板，快速生成学术风格 PPT。模板包含 ZJU Logo、浙大蓝渐变顶栏、自动导航和页脚。

## 何时使用

当用户要求：
- 做 PPT / 幻灯片 / presentation / slides
- 使用浙江大学模板
- 使用 Beamer 做学术演示

## 资源文件位置

模板资源存放在本 skill 的 `resources/` 目录：

```
skills/zju-beamer/resources/
├── zju_beamer.sty          # ZJU Beamer 样式文件
└── figures/
    ├── background.png      # 背景图
    ├── char.pdf            # "浙江大学" 字样矢量图
    └── logo.pdf            # ZJU 校徽矢量图
```

## 使用步骤

### Step 1: 创建项目目录并复制模板资源

```bash
# 在用户工作目录下创建 presentation 文件夹
mkdir -p <target_dir>/figures

# 复制模板资源
cp skills/zju-beamer/resources/zju_beamer.sty <target_dir>/
cp skills/zju-beamer/resources/figures/* <target_dir>/figures/
```

### Step 2: 创建 main.tex

使用下面的模板结构创建 `main.tex`。根据用户需求填充内容。

```latex
%# -*- coding:utf-8 -*-
\PassOptionsToPackage{quiet}{fontspec}
\documentclass[10pt,aspectratio=169]{beamer}
\usepackage{zju_beamer}
\graphicspath{{./figures/}}
\zjusectioncolor{blue}    % 顶栏右上角颜色: blue 或 black

% 额外需要的包
\usepackage{booktabs}     % 表格美化
\usepackage{tikz}         % 绘图
\usetikzlibrary{arrows.meta, positioning, shapes.geometric}
\usepackage{pifont}       % \ding 符号

% 自定义颜色（与浙大蓝搭配）
\definecolor{AccentTeal}{HTML}{14B8A6}
\definecolor{AccentAmber}{HTML}{F59E0B}
\definecolor{DangerRed}{HTML}{EF4444}
\definecolor{SuccessGreen}{HTML}{22C55E}
\definecolor{ZJUBlue}{RGB}{0,63,136}

% 标题页信息
\title[短标题]{完整标题}
\subtitle{副标题}
\author[短名]{作者名}
\institute[ZJU]{浙江大学}
\date{\today}

\begin{document}

% 标题页
\begin{frame}
    \titlepage
\end{frame}

% 目录页
\begin{frame}
    \frametitle{Outline}
    \tableofcontents
\end{frame}

% === 正文内容 ===

\section{章节名}

\begin{frame}{页面标题}
    内容...
\end{frame}

% === 结束页 ===

\begin{frame}
    \begin{center}
        \vspace{2cm}
        {\Huge\bfseries Thank You}\\[1em]
        {\Large Questions \& Discussion}\\[2em]
        {\normalsize 作者名~$\vert$~浙江大学}
    \end{center}
\end{frame}

\end{document}
```

### Step 3: 编译

必须使用 **XeLaTeX** 编译（因为中文支持）：

```bash
cd <target_dir>
xelatex -interaction=nonstopmode main.tex
xelatex -interaction=nonstopmode main.tex   # 第二次确保目录正确
```

### Step 4: 打开预览

```bash
open main.pdf
```

## 常用 Beamer 语法速查

### 分栏布局
```latex
\begin{columns}[T]
    \begin{column}{0.48\textwidth}
        左边
    \end{column}
    \begin{column}{0.48\textwidth}
        右边
    \end{column}
\end{columns}
```

### 彩色方框
```latex
\begin{block}{标题}           % 蓝色
    内容
\end{block}

\begin{alertblock}{标题}      % 红色警告
    内容
\end{alertblock}

\begin{exampleblock}{标题}    % 绿色示例
    内容
\end{exampleblock}
```

### 插入图片
```latex
% 先把图片放到 figures/ 文件夹
\includegraphics[width=0.6\textwidth]{图片名.png}
```

### 表格
```latex
\begin{tabular}{lcc}
    \toprule
    \textbf{方法} & \textbf{指标A} & \textbf{指标B} \\
    \midrule
    Baseline & 0.75 & 0.80 \\
    Ours     & \textbf{0.85} & \textbf{0.88} \\
    \bottomrule
\end{tabular}
```

### TikZ 流程图
```latex
\begin{tikzpicture}[
    block/.style={rectangle, draw=ZJUBlue, fill=ZJUBlue!8,
        rounded corners=4pt, minimum height=1cm, minimum width=2cm,
        align=center, font=\small\bfseries},
    arrow/.style={-{Stealth[length=5pt]}, thick, ZJUBlue!70!black}
]
    \node[block] (a) {模块A};
    \node[block, right=1cm of a] (b) {模块B};
    \node[block, right=1cm of b] (c) {模块C};
    \draw[arrow] (a) -- (b);
    \draw[arrow] (b) -- (c);
\end{tikzpicture}
```

### 文字颜色
```latex
\textcolor{ZJUBlue}{浙大蓝}
\textcolor{DangerRed}{红色警告}
\textcolor{SuccessGreen}{绿色成功}
\textcolor{AccentAmber}{琥珀色强调}
```

### 特殊符号
```latex
\ding{51}   % ✓ 勾号
\ding{55}   % ✗ 叉号
\ding{72}   % ★ 星号
```

## 注意事项

1. **编译器**: 必须用 `xelatex`，不能用 `pdflatex`
2. **字体警告**: Fira Sans/Mono 字体警告可忽略，不影响输出
3. **中英文混排**: 模板已配置 `xeCJK` + `ctex`，可直接混排
4. **16:9 宽屏**: 默认 `aspectratio=169`，如需 4:3 改为 `aspectratio=43`
5. **颜色主题切换**: `\zjusectioncolor{blue}` 改为 `\zjusectioncolor{black}` 可切换顶栏颜色
