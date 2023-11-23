# Why jupytex?
This is a python package for rendering LaTeX in Jupyter notebook with native 
rendering capabilities. Jupyter uses MathJax to render LaTeX inside of 
Markdown cells, which is fine for most use cases; however, this does not 
provide the full set of tools that LaTeX has to offer (e.g. tikzpictures,
complex figures). What we want is the ability to write content using Jupyter
for dynamic content while not sacrificing the beauty of native LaTeX.

# How Does it Work?
This is a custom ipython [magic plugin](https://ipython.readthedocs.io/en/stable/config/custommagics.html)
which allows users to create a new code cell, placing `%%tex` at the top and 
then put all of their LaTeX source code afterwards. Running the cell compiles
the code into `.svg` format which is displayed following the cell.

Jupytex uses `pdflatex` to compile your cell's code into PDF format, then
`pdfcrop` to crop the content, and `pdf2svg` to convert the PDF to `.svg`
format. Then this is displayed using the IPython module. The compilation is
fast, and has the upside of your LaTeX not needing to be rendered with
Javascript when viewed on the web. 

The `.svg` format is great because it doesn't lose any definition upon
zooming in on the compiled LaTeX and you can highlight text with your cursor,
which you cannot do with normal image formats like PNG/JPEG.

To load the module in ipython use: `get_ipython().register_magic_function(tex, 'cell')`

# Current Limitations
Because jupytex presents the compiled LaTeX in `.svg` format, it assumes
a standard page layout. Currently `texify()` crops to content; although there
are slight things that are off about the margins. The goal is to fix this in
the next release!

# Tests directory
Currently this directory contains screenshots but no automated tests. Some 
ideas for testing could be to use selenium for screenshotting and comparing 
images with known working versions.

# Example Runs
![](./tests/magic.png)
![](./tests/tikz.png)
![](./tests/algorithm.png)
![](./tests/matrix.png)
