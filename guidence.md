# BUPT 本科毕业设计（论文）模板速览与使用指引

面向 Github / Overleaf 用户，快速说明这个仓库的结构、写作顺序、编译方法、字体准备、参考文献用法。

## 目录结构速览
- `main.tex`：论文入口文件，按顺序包含封面、诚信声明、摘要、目录、正文各章、参考文献、致谢、附录。
- `BUPTBachelorThesis.sty`：版式样式定义（字体、页边距、页眉页脚、章节标题、附录、代码、算法等）。
- `BUPTBachelor.bst`：BibTeX 参考文献样式。
- `ref.bib`：论文正文的文献数据库。
- `chapters/`：正文各部分
  - `cover.tex` 封面（LaTeX 版）——填姓名、学院、学号、导师等。
  - `abstract.tex` 中英文摘要与关键词。
  - `chapter1.tex` 引言示例，需要换成你的课题内容。
  - `chapter2.tex` 文献综述骨架，可复制生成更多章节（chapter3、4…）。
  - `acknowledgment.tex` 致谢。
- `appendix/appendix1.tex`：附录示例（缩略语表、如何用 `\hyperlink` 引用）。
- `docs/statement.pdf`：诚信声明 PDF（需从学校 Word 模板导出，命名后放这里）。
- `assets/`：封面用的校名、校徽等图片。
- `Proposal/`：开题报告的独立模板（与论文主体分开编译）。

## 建议的写作顺序
1) 在 `main.tex` 里改题目：`\thesistitle{中文题目}`、`\thesisenglishtitle{英文题目}`。  
2) 在 `chapters/cover.tex` 填姓名、学院/专业、班级、学号、导师。  
3) 在 `chapters/abstract.tex` 写中文摘要和关键词；英文摘要和 KEY WORDS。  
4) 依次写 `chapter1.tex`（引言、研究意义/目标/问题）、`chapter2.tex`（文献综述）。如需更多章节，复制 `chapter2.tex` 为 `chapter3.tex` 等，并在 `main.tex` 里增加 `\subfile{chapters/chapter3}`。  
5) 写实验/设计/实现/结果等后续章节（自己命名），更新 `ref.bib` 和正文引用。  
6) 写附录（如需要），参考 `appendix1.tex` 的用法，用 `\appendixsection{标题}{label}` 建立附录并在正文用 `\hyperlink{label}{附录名}` 引用。  
7) 最后完善致谢 `acknowledgment.tex`。  
8) 确认 `docs/statement.pdf` 存在（诚信声明），编译前放好。

## 本地编译
- 需要 XeLaTeX + BibTeX（TeX Live 或 MiKTeX）。  
- 推荐：`latexmk main.tex`（已在 `.latexmkrc` 配好 XeLaTeX 流程）；或手动 `xelatex -> bibtex -> xelatex -> xelatex`。  
- 入口文件是仓库根目录下的 `main.tex`，不要用 Proposal 目录的 main。

## Overleaf 使用
- 上传根目录下除 `Proposal/` 外的文件，入口设为 `main.tex`，编译器选 `XeLaTeX`。  
- 如果需要写开题报告，单独上传 `Proposal/` 里的文件，入口改为 `Proposal/main.tex`。  
- 字体提示见下节：Overleaf 默认没有 Windows 中文字体，需要额外处理。

## 字体准备（重点）
样式文件 `BUPTBachelorThesis.sty` 使用 `\usepackage[fontset=windows]{ctex}`，默认依赖 Windows 常见中文字体：
- 宋体：`SimSun`（正文）
- 黑体：`SimHei`（粗体）
- 楷体：`KaiTi`（斜体/楷体）
- 西文字体：`Times New Roman`

在 Windows 本机通常自带，直接编译即可。  
在 macOS / Linux / Overleaf：
- 方案 A：将 `SimSun`、`SimHei`、`KaiTi` 的 TTF/TTC连同工程一起上传，并在 `BUPTBachelorThesis.sty` 用 `\setCJKmainfont{SimSun}[Path=fonts/]` 等方式指向这些字体。  
- 方案 B（简易，字体效果略有差异）：把 `BUPTBachelorThesis.sty` 里 `\usepackage[fontset=windows]{ctex}` 改成 `\usepackage[fontset=fandol]{ctex}`，使用 TeX 自带的 Fandol 中文字体。  
缺字/缺字体时编译会有 fontspec 警告或报错，按以上两种方案二选一处理。

## 参考文献写法
- 所有条目放在根目录 `ref.bib`，BibTeX 格式。可用 Zotero / Google Scholar 导出粘贴。  
- 正文引用：`正文\cite{your-key}`。  
- 参考文献区在 `main.tex` 中已设好：`\bibliographystyle{BUPTBachelor}` + `\bibliography{ref}`。  
- 编译顺序要包含 BibTeX（用 `latexmk` 或手动 xelatex-bibtex-xelatex-xelatex），否则会出现 “Citation ... undefined” 警告。  
- 英文文献请不要加 `language` 字段，避免生成“见”而不是“In”。

## 常见操作提示
- 新增章节：复制 `chapters/chapter2.tex` 为 `chapterN.tex`，然后在 `main.tex` 增加 `\subfile{chapters/chapterN}`。  
- 插图/子图：已加载 `graphicx`、`subcaption`，可直接用 README 里的示例。  
- 代码/算法：已加载 `listings` 和 `algorithm/algpseudocode`，直接使用相关环境。  
- 诚信声明：`docs/statement.pdf` 不在时模板会跳过，但正式提交需放入正确 PDF。

## Proposal（开题报告）
- 独立入口：`Proposal/main.tex`，样式在 `Proposal/BUPTBachelorProposal.cls`。  
- 需要时单独编译，不影响毕业论文主体。
