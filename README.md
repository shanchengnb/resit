## Navigate to the folder where the .qmd file is located.
For example, in Windows PowerShell:

cd "C:\Users\Administrator\Downloads"（(replace with the actual location of the .qmd file on your computer)）

quarto render "24034306ChengShan.qmd" --to pdf


This will generate:

24034306ChengShan.pdf (formatted coursework submission)

## MikTeX "security risk" Warning

When running Quarto/XeLaTeX on Windows with administrator privileges, MikTeX may show:

xelatex: security risk: running with elevated privileges
miktex-dvipdfmx: security risk: running with elevated privileges


This is a warning, not an error.

The PDF is still generated successfully.

To avoid the warning, run Quarto as a normal user instead of with administrator rights.
