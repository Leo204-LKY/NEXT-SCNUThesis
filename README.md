# NEXT-SCNUThesis

> [!CAUTION]
> 中方和英方的论文格式可能会发生变化，因此本模板不一定能完全满足最新的格式要求。建议检查最新的论文格式要求，多将论文发给指导老师检查，并根据需要调整模板。

- 基于 [FaterYu/NEXT-SCNUThesis](https://github.com/FaterYU/NEXT-SCNUThesis) 修改而来，支持在同一套模板中使用 $\LaTeX$ 编写同时适用于中方（华师）和英方（阿伯丁）的毕业论文，并根据需要渲染成符合中方或英方要求的论文格式。

### 如何使用

1. 克隆或下载本仓库，上传至 Overleaf 或在本地使用 LaTeX 编辑器打开。
2. 获取英方论文模板（由于英方有标准 LaTeX 论文模板，为避免英方模板更新，而新版本格式有较大改变，此处不提供英方模板），复制其中的 `main.tex`、`abdnthesis.cls` 和 `abdnshield.pdf` 文件到本仓库的根目录。
3. 在 `main.tex` 中修改以下内容：

   ```diff
   ...

   - \usepackage[round,colon,authoryear]{natbib}
   + \usepackage[numbers,sort&compress]{natbib}
   \setlength{\bibsep}{0pt}
   - \bibliographystyle{apalike}
   + \bibliographystyle{unsrt}
   \usepackage{hyperref}

   \usepackage[T1]{fontenc}

   + \newif\ifTableCaptionTop
   + \TableCaptionTopfalse

   ...

   \begin{abstract}
   -  An expansion of the title and contraction of the thesis.
   +  \input{content/abstract-en.tex}
   \end{abstract}

   \begin{acknowledgements}
   -  Much stuff borrowed from elsewhere
   + \input{content/acknowledgements.tex}
   \end{acknowledgements}

   ...

   - \bibliography{mybib}
   + \bibliography{reference}

   ...
   ```

4. 在 `content` 目录下创建各章节的 tex 文件，并在 `main.tex` 和 `main-scnu.tex` 中使用 `\include{content/xxx.tex}` 或 `\input{content/xxx.tex}` （取决于你需要新建一页展示章节，还是与之前的内容展示在同一页）插入到对应位置。
   - 摘要（中文/英文）和致谢直接在 `abstract-zh.tex`、`abstract-en.tex` 和 `acknowledgements.tex` 中编辑内容，无需修改 `main.tex` 和 `main-scnu.tex`。
   - 图片建议放在 `fig` 目录下，在 `\includegraphics` 用相对根目录的路径引用，如 `\includegraphics{fig/example.png}`。

### 注意事项

> [!IMPORTANT]
> 请务必阅读并遵守以下注意事项，以确保论文格式符合要求。

- **表格**的标题需特殊处理
  - 中方论文表格标题需放在表格上方，英方论文表格标题需放在表格下方。
  - 请按以下格式编写表格（尤其是标题 `\caption` 和 `\label` 部分）

    ```tex
    \begin{table}[h]
        \centering
        \ifTableCaptionTop
          \caption{Your caption here}
          \label{tab:label-here}
        \fi

        \begin{table}
          % Your table here
        \end{table}

        \ifTableCaptionTop\else
          \caption{Your caption here}
          \label{tab:label-here}
        \fi
    \end{table}
    ```
    - 需要编写两次 `\caption` 和 `\label`，分别放在表格的上方和下方，并使用 `\ifTableCaptionTop` 条件判断来控制显示位置。

- 中方论文需使用 XeLaTeX 编译，英方论文需使用 pdfLaTeX 编译。
  - 在 Overleaf 中，点击页面左下角的 ⚙ → 编译器（Compiler），修改“主文档（Main document）”和“编译器（Compiler）”两个选项即可在两种论文格式之间切换。
    - 英方论文主文档选 `main.tex`，编译器选 `pdfLaTeX`
    - 中方论文主文档选 `main-scnu.tex`，编译器选 `XeLaTeX`
- 其他内容请参考原始仓库中的 README 和 Wiki，我会在之后尝试合并这些内容。

---

以下为原始 README

# NEXT-SCNUThesis

华南师范大学本科毕业论文 LaTeX 模板 **[更新中]**

[Overleaf Template | NEXT-SCNUThesis](https://www.overleaf.com/read/cztdbznzmfwm#891a33)

[![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/FaterYU/NEXT-SCNUThesis/tex_build.yml)](https://github.com/FaterYU/NEXT-SCNUThesis/actions/workflows/tex_build.yml)
[![release](https://img.shields.io/github/v/release/FaterYU/NEXT-SCNUThesis?include_prereleases&style=flat)](https://github.com/FaterYU/NEXT-SCNUThesis/releases/latest)

[![GitHub Issues or Pull Requests](https://img.shields.io/github/issues/FaterYU/NEXT-SCNUThesis)](https://github.com/FaterYU/NEXT-SCNUThesis/issues)
[![GitHub Issues or Pull Requests](https://img.shields.io/github/issues-closed/FaterYU/NEXT-SCNUThesis)](<[https://github.com/FaterYU/NEXT-SCNUThesis/issues](https://github.com/FaterYU/NEXT-SCNUThesis/issues?q=is%3Aissue%20state%3Aclosed)>)

[![GitHub Issues or Pull Requests](https://img.shields.io/github/issues-pr/FaterYU/NEXT-SCNUThesis)](https://github.com/FaterYU/NEXT-SCNUThesis/pulls)
[![GitHub Issues or Pull Requests](https://img.shields.io/github/issues-pr-closed/FaterYU/NEXT-SCNUThesis)](https://github.com/FaterYU/NEXT-SCNUThesis/pulls?q=is%3Aissue%20state%3Aclosed)

<details>
  <summary>动机 & 碎碎念</summary>
  起因是作者毕业论文需要将同一篇论文内容以两种不同的模板（华南师范大学和阿伯丁大学）分别提交，而阿伯丁提供了 LaTeX 模板，华南师范大学的模板则是 Word 的。而要将 1.5万词的英文论文（公式、引用、图表）从 LaTeX 模板迁移到 Word 模板，懂的都懂。更窒息的是，在华师的毕业论文要求中，不能完全不出现中文，而本专业又要求英文写作，这就导致必须在 LaTeX 模板中混排中文和英文。作者已经基本完成英文 LaTeX 模板下的毕业论文，鉴于此，一个能无痛迁移且符合华南师范大学本科毕业论文格式要求的 LaTeX 模板就成为刚需了。本项目部分细节参考了scnuthesis，从空白模板头尽可能简洁地手撕了这个项目。亲测从本人的英文 LaTeX 论文初步迁移到本模板耗时约 10 分钟，即可大致符合要求。至于是否最终符合还待今年作者毕业的检验。
</details>

## News 👌

- [ ] 适配纯中文论文
- [x] **25/04/19**🗓️ 测试查重 / AIGC 均正常
- [x] **25/04/14**🗓️ 完成 GitHub CI
- [x] **25/04/14**🗓️ Overleaf 私有模板发布
- [x] **25/04/07**🗓️ GitHub Release 发布
- [x] **25/04/06**🗓️ 适配纯英文论文

## 👀 预览

[example.pdf](https://github.com/user-attachments/files/19797473/NEXT_SCNUThesis.pdf)

![preview](https://github.com/user-attachments/assets/778e8a08-5011-430a-8fd3-273fe29a735d)

## 特性

🔥 基本符合华南师范大学本科毕业论文格式要求

🔥 更好的中英混排

🔥 更高级别的封装

🔥 从英文模板无痛迁移

🔥 持续集成 (Continuous integration) 跟踪修改的有效性

## 使用方法

**务必阅读后使用**

📖 [Wiki - How To Use](https://github.com/FaterYU/NEXT-SCNUThesis/wiki/How-To-Use)

## 反馈

若已经使用 / 计划使用此模板，希望能花1分钟完成以下表单，若有交流需要可加q群： 963592181

[点击此处填写反馈表单](https://forms.office.com/e/ESdiTbCaPt)

## 遇到问题❓

1. 检查 [Wiki - How To Use | 常见问题](https://github.com/FaterYU/NEXT-SCNUThesis/wiki/How-To-Use#%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)
2. 检查 [ISSUE](https://github.com/FaterYU/NEXT-SCNUThesis/issues)
3. 提出 [ISSUE](https://github.com/FaterYU/NEXT-SCNUThesis/issues) or 联系作者

## 参考

🔗 [scnuthesis](https://github.com/scnu/scnuthesis)

🔗 [University of Aberdeen thesis template](https://www.overleaf.com/latex/templates/university-of-aberdeen-thesis-template/jzrbyqmggygd)

🔗 [SCNU-ABD-Thesis-template](https://github.com/kikixiong/SCNU-ABD-Thesis-template)

🔗 [GB/T 7714](https://github.com/zepinglee/gbt7714-bibtex-style)

🔗 [IEEE Conference Template](https://www.overleaf.com/latex/templates/ieee-conference-template/grfzhhncsfqn)

## ⭐

[![Star History Chart](https://api.star-history.com/svg?repos=FaterYU/NEXT-SCNUThesis&type=Date)](https://www.star-history.com/#FaterYU/NEXT-SCNUThesis&Date)

## Contribute

1. 提交 [Pull Requests](https://github.com/FaterYU/NEXT-SCNUThesis/pulls)
2. 确保通过触发的 [Action CI](https://github.com/FaterYU/NEXT-SCNUThesis/actions)，通过需要 `example.tex` 与 `main.tex` 无 `ERROR`
3. 等待作者处理
