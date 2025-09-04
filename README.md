## Navigate to the folder where the .qmd file is located.
For example, in Windows PowerShell:

cd "C:\Users\Administrator\Downloads"（(replace with the actual location of the .qmd file on your computer)）

quarto render "24034306ChengShan.qmd" --to pdf

This will generate:

24034306ChengShan.pdf (formatted coursework submission)


## Note:



1.bibliography: ChenShandata/bio.bib

2.csl: ChenShandata/harvard-cite-them-right.csl


Quarto will automatically create a folder named ChenShandata in your project directory (if it does not already exist) and download the necessary files there.

This ensures that your bibliography (bio.bib) and CSL style file (harvard-cite-them-right.csl) are correctly located for PDF rendering.


## Library Installation and Environment Setup

This code checks and ensures that all required Python libraries for the project are installed. If requirements.txt is missing, it automatically downloads it from GitHub. Any missing libraries are installed via pip, and the current Python environment path is displayed. This ensures that the project can run smoothly on different machines without manually managing dependencies.


## Data Download and Loading

This code automatically creates a project-specific folder (ChenShandata) on your computer to store required files. It downloads key data and resources from GitHub if they are missing:

1.final_data.csv (main dataset)

2.bio.bib (bibliography)

3.harvard-cite-them-right.csl (citation style)

4.neighbourhoods.geojson (spatial boundaries)

After downloading, it loads the CSV into a pandas DataFrame and stops execution if the data is missing or empty. This ensures reproducibility and that all required files are locally available without manual intervention.

Key points to emphasize:

A local folder ChenShandata will be automatically created.

Missing files are downloaded from GitHub, so you don’t need to manually fetch them.

Execution halts if final_data.csv is not available, preventing downstream errors.

Handles different file types correctly (GeoJSON as bytes, text files as UTF-8).


## MikTeX "security risk" Warning

When running Quarto/XeLaTeX on Windows with administrator privileges, MikTeX may show:

xelatex: security risk: running with elevated privileges
miktex-dvipdfmx: security risk: running with elevated privileges


This is a warning, not an error.

The PDF is still generated successfully.

To avoid the warning, run Quarto as a normal user instead of with administrator rights.

## PDF rendered successfully
C:\Users\Administrator>quarto render "24034306ChengShan.qmd" --to pdf

Starting python3 kernel...Done

Executing '24034306ChengShan.quarto_ipynb'
  Cell 1/8: ''...Done
  Cell 2/8: ''...Done
  Cell 3/8: ''...Done
  Cell 4/8: ''...Done
  Cell 5/8: ''...Done
  Cell 6/8: ''...Done
  Cell 7/8: ''...Done
  Cell 8/8: ''...Done

pandoc
  to: latex
  output-file: 24034306ChengShan.tex
  standalone: true
  pdf-engine: xelatex
  variables:
    graphics: true
    tables: true
  default-image-extension: pdf
  toc: false
  number-sections: false

metadata
  documentclass: scrartcl
  classoption:
    - DIV=11
    - numbers=noendperiod
  papersize: a4
  header-includes:
    - \KOMAoption{captions}{tableheading}
  block-headings: true
  bibliography:
    - ChenShandata/bio.bib
  csl: ChenShandata/harvard-cite-them-right.csl
  title: Professionalisation of Airbnb:regulatory challenge or growth opportunity?
  jupyter:
    jupytext:
      text_representation:
        extension: .qmd
        format_name: quarto
        format_version: '1.0'
        jupytext_version: 1.15.2
    kernelspec:
      display_name: Python 3 (ipykernel)
      language: python
      name: python3
  mainfont: Times New Roman
  sansfont: Arial
  monofont: Courier New
  geometry:
    - top=25mm
    - left=40mm
    - right=30mm
    - bottom=25mm
    - heightrounded
  colorlinks: true


Rendering PDF
running xelatex - 1
  xelatex: security risk: running with elevated privileges
  This is XeTeX, Version 3.141592653-2.6-0.999997 (MiKTeX 25.3) (preloaded format=xelatex.fmt)
   restricted \write18 enabled.
  entering extended mode
  miktex-dvipdfmx: security risk: running with elevated privileges

running xelatex - 2
  xelatex: security risk: running with elevated privileges
  This is XeTeX, Version 3.141592653-2.6-0.999997 (MiKTeX 25.3) (preloaded format=xelatex.fmt)
   restricted \write18 enabled.
  entering extended mode
  miktex-dvipdfmx: security risk: running with elevated privileges


Output created: 24034306ChengShan.pdf
