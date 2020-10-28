# CJK

1. 下载下列字体（因涉及到版权，请自行搜索下载）
   1. 方正书宋 GBK：FZSSK.TTF
   2. 方正楷体 GBK：FZKTK.TTF
   3. 方正黑体 GBK：FZHTK.TTF
   4. 方正仿宋 GBK：FZFSK.TTF
   5. 华文隶体：STLITI.ttf（安装 Office 之后自带）
   6. 华文琥珀：STHUPO.TTF（安装 Office 之后自带）
2. 安装字体（以 FZSSK.TTF 为例）
3. 安装成功后，在 Font Book.app 当中应当可见相应字体（以 FZSSK.TTF 为例）安装在 ~/Library/Fonts/FZSSK.TTF

## 修改 TeX Live 配置文件

1. 打开 Finder.app
2. 按下快捷键 Command + Shift + G，输入 /usr/local/texlive 而后点击「Go」（如果目录不存在，说明你没有将 macTeX 安装在默认位置，请自行调整
3. 进入相应的年份目录（我这里是 `2020`），而后用 `TextEdit.app` 打开 texmf.cnf
4. 检查文件中是否有 `OSFONTDIR` 变量
   1. 若无，则在文件最后新增一行，内容为：OSFONTDIR = ~/Library/Fonts//:/Library/Fonts//:/System/Library/Fonts//
   2. 若有，则确保其中包含 ~/Library/Fonts 这个目录

## 安装 zhfzfonts.tex

打开 Terminal.app，依次执行下列命令：

```Bash
ls -l /usr/local/texlive/texmf-local # 确认目录存在（如果不存在，说明你没有将 macTeX 安装在默认位置，请自行调整）
mkdir -p /usr/local/texlive/texmf-local/tex/generic/zhmetrics/ # 新建目录
cd /usr/local/texlive/texmf-local/tex/generic/zhmetrics/ # 进入刚才新建的目录
wget https://liam.page/attachment/attachment/LaTeX-useful-tools/zhfzfonts.tex # 下载 `zhfzfonts.tex`
texhash # 刷新 ls-R 数据库，可能需要 `root` 权限
```

## 试用 CJK

至此，你可以如常使用 CJK 宏包支持中文，只需要在导言区额外新增一行即可：\AtBeginDvi{\input{zhfzfonts}}。

```latex
\documentclass{article}
\usepackage{CJK}  % CJKutf8
\AtBeginDvi{\input{zhfzfonts}}
\begin{document}
\begin{CJK*}{UTF8}{song}
中文。
\clearpage
\end{CJK*}
\end{document}
```

你可以使用 PDFLaTeX 编译，也可以使用 LaTeX - DVIPDFMx 编译。得到结果如下图所示。

注意，CJK 支持 GBK，也支持 UTF-8。因此，你需要将文档编码保存为与 CJK 环境相同的编码格式。

## Reference

<https://liam.page/2020/04/17/using-CJK-on-macTeX-step-by-step/>
