# Data Directory

## Two Data Files

This folder contains two versions of the Angrist & Evans (1998) Census extract:

- **`census80_slim.csv.gz`** — Contains 20 key variables. Used by the original notebooks `02` and `03`. It is faster to load and easier to work with.
- **`census80_full.csv.gz`** — Contains all 85 original variables from the raw extract. Used by the corrected notebook `04`, because the authors' sample restrictions need variables the slim file omits (children's ages in quarters, the mother's birth year and quarter, Census allocation flags, and marriage timing). `04` loads only the 25 columns it needs.

## Data Processing

The original data was sourced as a `.sas7bdat` file, a binary format used by SAS, which is common in academic economics research. It was loaded into Python using `pandas.read_sas()` (927,267 rows × 85 columns, about 2.9 GB in memory). Downcasting numeric columns barely helped, because most columns loaded as byte strings; keeping only needed columns and converting low-cardinality columns to categorical dtype reduced memory to about 0.6 GB. The data were then saved as `.csv.gz` files. CSV does not preserve dtypes, and the byte-string values were written as literal `b'...'` text, so each notebook strips that wrapper and converts values back to numbers when loading. The `.csv.gz` format is a standard CSV compressed with gzip, which reduces file size significantly while remaining natively readable by pandas with no extra steps (`pd.read_csv("file.csv.gz")` works out of the box).

## Accessing the Original Data

The original raw file can be downloaded directly from the Angrist Data Archive hosted by MIT Economics:

**https://economics.mit.edu/people/faculty/josh-angrist/angrist-data-archive**

Download the file associated with Angrist & Evans (1998) and place it in this folder as `m_d_806.sas7bdat` to reproduce the processing steps in `01_Data_Cleaning.ipynb`.
