---
path: '/2022/3/pandoc-markdown-to-pdf-using-html5-engine-20220331235600'
title: 'pandoc markdown to pdf using html5 engine'
date: '20220331235600'
category: 'markdown'
tags: ['pandoc', 'markdown', 'latex']
---

# pandoc markdown to pdf using html5 engine
Converting markdown to a PDF is a nightmare, espeically when interfacing with
LaTeX. This has proven to be a truly terrible experience, it is likely much easier
to just write plain old LaTeX.

I was able to (finally) convert the file to a PDF, but it looked much worse off than
than anything I could have put together in LaTeX.

**Requirements:**
* Ubuntu

**Resources:**
* [Blog post on fancier markdown](https://blog.stolle.email/2020/04/05/convert-markdown-files-to-pdf-in-ubuntu/)
* [Blog post on colors and unknown characters](https://jdhao.github.io/2019/05/30/markdown2pdf_pandoc/#issues-and-techniques)

## Steps

If you don't have any lists or tables:
```
sudo apt install texlive-latex-base texlive-fonts-recommended texlive-fonts-extra texlive-latex-extra pandoc
pandoc -t latex -o test.pdf test.md
```

If you do have lists or tables:
```
sudo apt install wkhtmltopdf pandoc
pandoc -t html5 -V papersize=a4 -o test.pdf test.md
```

## Tips
* If you want linebreaks in your lists use a `\` at the end of each item or just put
a newline between them.
* Anything you don't want concatenated into a wrapped line should have the above as well,
this gets needlessly verbose.
* If you want to have a table it must be in a code block, they look gross too

```
| my table |
|----------|
| something|
```

