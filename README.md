
## ⚠️ Critical Note: QMD File Available for Direct Execution
Run the first code block to install the required libraries. If it doesn’t work, you can directly run the following command in Jupyter Notebook or IPython to install all necessary packages:

```{python}
#| echo: False
!pip install pandas==2.2.3 numpy==1.26.4 matplotlib==3.9.2 seaborn==0.13.2 wordcloud==1.9.4 geopandas==1.0.1 scikit-learn==1.6.1 requests==2.32.3 tqdm==4.67.1
```
or
```{python}
#| echo: False
import sys

# Install core libraries with fixed versions (including geopandas)
!{sys.executable} -m pip install \
    pandas==2.2.3 \
    numpy==1.26.4 \
    matplotlib==3.9.2 \
    seaborn==0.13.2 \
    wordcloud==1.9.4 \
    geopandas==1.0.1 \
    scikit-learn==1.6.1 \
    requests==2.32.3 \
    tqdm==4.67.1

```

If library installation fails: The final version of my QMD file is available on GitHub: 24034306ChengShan.qmd
. You can use this file to run the analysis directly without needing to re-install packages manually.

The QMD file includes a Python setup block that automatically installs any missing packages globally:

Check for requirements.txt — if missing, it downloads it from GitHub.

Install missing libraries globally — all required packages are installed system-wide using pip install -r requirements.txt, ensuring that every user on the system can access them without separate user-level installs.

Show current Python executable — confirms which Python environment is being used.

Key modules: importlib (check installed packages), subprocess (run pip globally), sys, Pathlib, requests.

This guarantees that the QMD can be executed directly without manual package management and avoids issues caused by missing dependencies.
## 0. Library Installation 
```{python}
#| echo: False
!pip install pandas==2.2.3 numpy==1.26.4 matplotlib==3.9.2 seaborn==0.13.2 wordcloud==1.9.4 geopandas==1.0.1 scikit-learn==1.6.1 requests==2.32.3 tqdm==4.67.1
```

```{python}
#| echo: False
import importlib
import subprocess
import sys
from pathlib import Path
import requests

# ----------------------------
# Step 1: Ensure requirements.txt exists
# ----------------------------
req_file = Path("requirements.txt")
if not req_file.exists():
    url = "https://raw.githubusercontent.com/shanchengnb/resit/main/requirements.txt"
    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()
        req_file.write_text(response.text, encoding="utf-8")
        print(f"✔ requirements.txt downloaded from GitHub to {req_file.resolve()}")
    except Exception as e:
        print(f"⚠️ Failed to download requirements.txt: {e}")
        print("👉 Please manually download it from https://github.com/shanchengnb/resit and place it in the project root.")
        raise SystemExit("❌ Cannot proceed without requirements.txt")

# ----------------------------
# Step 2: Install missing libraries
# ----------------------------
def check_and_install_requirements(req_path):
    """Check and install any missing packages listed in requirements.txt."""
    if not req_path.exists():
        raise FileNotFoundError(f"{req_path} does not exist.")

    # Parse required packages
    with req_path.open("r", encoding="utf-8") as f:
        lines = f.readlines()
    req_packages = [line.strip().split("==")[0] for line in lines if line.strip() and not line.startswith("#")]

    # Check missing packages
    missing = []
    for pkg in req_packages:
        try:
            importlib.import_module(pkg)
        except ImportError:
            missing.append(pkg)

    if missing:
        print("⚠️ Installing missing packages globally:")
        for pkg in missing:
            print("   -", pkg)
        try:
            subprocess.check_call([sys.executable, "-m", "pip", "install", "-r", str(req_path)])
            print("\n✅ Missing packages installed successfully.")
        except subprocess.CalledProcessError as e:
            print(f"❌ Failed to install packages: {e}")
            raise
    else:
        print("✅ All required packages are already installed.")

# Run the check
check_and_install_requirements(req_file)

# ----------------------------
# Step 3: Show current Python executable
# ----------------------------
print(f"📝 Current Python executable: {sys.executable}")


```


## Navigate to the folder where the .qmd file is located.
For example, in Windows PowerShell:

cd "C:\Users\Administrator\Downloads"（(replace with the actual location of the .qmd file on your computer)）

quarto render "24034306ChengShan.qmd" --to pdf

This will generate:

24034306ChengShan.pdf (formatted coursework submission)

## ⚠️ Python Library Installation Notes

This project uses a requirements.txt file to ensure all required Python packages are available for reproducibility.

Installation Process in QMD

Ensure requirements.txt exists

The code downloads it automatically from GitHub if missing.

If the download fails, place it manually in the project root.

Check and install missing libraries

The script imports each package from requirements.txt and detects missing ones.

Missing packages are installed using:

python -m pip install --user -r requirements.txt


The --user flag installs packages in your user site-packages to avoid needing admin/root privileges.

Python executable check

After installation, sys.executable confirms the Python environment being used.

Important Notes

Local environments (Windows/macOS, Anaconda/VS Code)

Use --user to avoid permission issues.

Safe and recommended when you cannot install packages system-wide.

Docker / Instructor evaluation environment

Typically the Python user in Docker is root, so --user is not needed.

You can install packages globally using:

python -m pip install -r requirements.txt


In Docker, if a package already exists, it will not be reinstalled unless explicitly upgraded.

Version discrepancies

The current script installs missing packages only; it does not upgrade packages if a different version is present.

For fully reproducible results, ensure the Docker image contains all required packages at the correct versions.

## Font Information

This project was rendered in a local environment (without Docker). For aesthetic and cross-platform compatibility, the following fonts are used:


mainfont: "Times New Roman"

sansfont: "Arial"

monofont: "Courier New"

Times New Roman: Used for body text; classic, clear, and widely supported.

Arial: Used for sans-serif text, such as headings or chart labels.

Courier New: Used for monospaced text, such as code blocks or terminal outputs.

If these fonts are not installed on the teacher’s computer, they can be downloaded and installed manually (from system defaults or official sources like Microsoft or Google) to ensure consistent PDF formatting.

##  Important Notice: CSV File Encoding

The final_data.csv file in this project is already UTF-8 encoded. You can use it directly after downloading.

Do not re-save the CSV file in Excel or WPS, because the default save may convert it to GBK/ANSI encoding, which will cause Python to raise an error:

UnicodeDecodeError: 'utf-8' codec can't decode byte 0xa1 in position 147

✅ Solution: Safely Load the CSV

Use the following Python code to automatically handle both UTF-8 and GBK encoded CSV files:

import pandas as pd

from pathlib import Path

csv_path = Path("ChenShandata/final_data.csv")

try:
    df = pd.read_csv(csv_path, encoding="utf-8")
    print("✅ CSV loaded successfully with UTF-8 encoding")

    
except UnicodeDecodeError:   
    df = pd.read_csv(csv_path, encoding="gbk")
    print("✅ CSV loaded successfully with GBK encoding")


This way, even if the CSV file is accidentally re-saved as GBK, it will still load correctly without errors.

💡 Best Practices

Keep the original downloaded CSV file unchanged — do not modify or re-save it.


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
