## Navigate to the folder where the .qmd file is located.
For example, in Windows PowerShell:

cd "C:\Users\Administrator\Downloads"（(replace with the actual location of the .qmd file on your computer)）

quarto render "24034306ChengShan.qmd" --to pdf

This will generate:

24034306ChengShan.pdf (formatted coursework submission)


## Note:

When you specify in your .qmd file:

bibliography: ChenShandata/bio.bib
csl: ChenShandata/harvard-cite-them-right.csl


Quarto will automatically create a folder named ChenShandata in your project directory (if it does not already exist) and save the necessary files there.

This ensures that your bibliography (bio.bib) and CSL style file (harvard-cite-them-right.csl) are correctly located for PDF rendering.


## Library Installation and Environment Setup

This code checks and ensures that all required Python libraries for the project are installed. If requirements.txt is missing, it automatically downloads it from GitHub. Any missing libraries are installed via pip, and the current Python environment path is displayed. This ensures that the project can run smoothly on different machines without manually managing dependencies.


## Data Download and Loading

This code automatically creates a project-specific folder (ChenShandata) on your computer to store required files. It downloads key data and resources from GitHub if they are missing:

final_data.csv (main dataset)

bio.bib (bibliography)

harvard-cite-them-right.csl (citation style)

neighbourhoods.geojson (spatial boundaries)

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
