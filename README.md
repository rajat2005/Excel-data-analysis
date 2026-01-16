# Netflix Movies & TV Shows - Data Cleaning & Exploratory Analysis

![Netflix Logo](https://upload.wikimedia.org/wikipedia/commons/thumb/0/08/Netflix_2015_logo.svg/320px-Netflix_2015_logo.svg.png)
*(Add your own visualizations/screenshots here later if you want)*

## Project Overview

This project performs **data cleaning** and basic preparation on the popular **Netflix Movies and TV Shows** dataset (commonly found on Kaggle). The goal was to transform the raw, messy dataset into a clean, analysis-ready version using **Microsoft Excel**.

Main focus areas:
- Handling missing values (especially in `director`, `cast`, `country`)
- Standardizing text fields (remove extra spaces, fix capitalization inconsistencies)
- Validating & converting date formats to **YYYY-MM-DD**
- Ensuring numeric columns contain only valid numbers
- Reducing spelling variations & inconsistencies in categorical columns

This cleaned dataset is now suitable for further **EDA**, visualization (in Excel, Power BI, Tableau, Python, etc.), or building simple dashboards/recommendation insights.

## Dataset Source

- **Original Dataset**: Netflix Movies and TV Shows  
- **Kaggle Link**: [https://www.kaggle.com/datasets/shivamb/netflix-shows](https://www.kaggle.com/datasets/shivamb/netflix-shows)  
- **Rows**: ~8,800 titles (movies + TV shows)  
- **License**: CC0: Public Domain  
- **Last major update in original**: ~2019–2021 period (depending on version)

## Original Columns (typical structure)

| Column        | Description                                      | Data Type (original) | Common Issues                     |
|---------------|--------------------------------------------------|----------------------|------------------------------------|
| show_id       | Unique ID for each title                         | Text                 | —                                 |
| type          | Movie or TV Show                                 | Text                 | Minor case/spelling variations    |
| title         | Title of the movie/TV show                       | Text                 | Extra spaces, inconsistent case   |
| director      | Director(s) — comma separated                    | Text                 | ~30% missing                      |
| cast          | Actors/actresses — comma separated               | Text                 | Many missing, long strings        |
| country       | Country/countries where produced                 | Text                 | Missing, comma-separated, typos   |
| date_added    | Date added to Netflix                            | Text                 | Mixed formats (e.g. "January 15, 2019") |
| release_year  | Year of release                                  | Number/Text          | Rare typos/symbols                |
| rating        | Age rating (TV-MA, PG-13, etc.)                  | Text                 | Typos, extra spaces (" TV-14 ")   |
| duration      | Duration (e.g. "142 min", "2 Seasons")           | Text                 | —                                 |
| listed_in     | Genres/categories — comma separated              | Text                 | Extra spaces                      |
| description   | Short plot summary                               | Text                 | —                                 |

## What I Did – Step-by-Step Cleaning in Excel

1. **Preserve Original Data**  
   - Created duplicate sheet named "Cleaned_Data"  
   - Worked only on new columns (e.g., `Clean_Director`, `Clean_Date_Added`) to avoid overwriting originals

2. **Handled Missing Values**  
   - `director`, `cast`, `country`: replaced blanks/NaN with **"Unknown"** (most common & safe approach for analysis)  
   - Used formula: `=IF(ISBLANK(A2),"Unknown",A2)` or similar

3. **Text Standardization** (TRIM, PROPER, UPPER, etc.)  
   - Removed leading/trailing/extra spaces → `TRIM()`  
   - Fixed inconsistent capitalization → `PROPER(TRIM())` for names (director, cast, title)  
   - UPPER for categorical codes when needed (e.g., rating)  
   - Combined heavy cleaning: `=PROPER(TRIM(CLEAN(A2)))`

4. **Date Column Validation & Standardization** (`date_added`)  
   - Converted messy text dates ("September 25, 2021", "October 2020") to proper Excel dates  
   - Standardized format → **yyyy-mm-dd** using DATEVALUE + SUBSTITUTE + TRIM  
   - Handled partial dates & errors with IFERROR or helper columns

5. **Numeric Validation** (`release_year`)  
   - Removed dots, text, or symbols → forced pure numeric values  
   - Used: `=IFERROR(--TRIM(SUBSTITUTE(A2,".","")),"Check")`  
   - Applied Data Validation: whole numbers 1900–2030

6. **Categorical Cleaning**  
   - `type`: standardized to "Movie" / "TV Show" (fixed case/spelling)  
   - `rating`: TRIM + UPPER + manual Find & Replace for typos ("UR" → "NR", extra spaces)  
   - `country` & `listed_in`: TRIM + PROPER, reduced comma-spacing issues

7. **Final Steps**  
   - Copy-pasted cleaned values (Paste Special → Values)  
   - Removed/hid original messy columns (optional)  
   - Added basic Data Validation dropdowns for `type` & `rating`  
   - Checked for duplicates & inconsistencies using Conditional Formatting

## Files in This Repository

- `netflix_titles_original.csv` — Raw dataset (or link to Kaggle)  
- `netflix_cleaned.xlsx` — Excel file with original + cleaned sheets  
- `README.md` — this file

## Tools Used

- Microsoft Excel (TRIM, PROPER, UPPER, DATEVALUE, SUBSTITUTE, IFERROR, Text to Columns, Data Validation, Conditional Formatting)  
- (Optional next steps: Power Query for advanced transformations)

## Next Possible Steps

- Create pivot tables & charts in Excel (top directors, content by year/country, movie vs TV ratio)  
- Export clean CSV → analyze in Python (pandas, seaborn/matplotlib) or Power BI  
- Build simple content-based recommender using `description` or `listed_in`

## Author

- **Rajat** (Gurugram, India)  
- Purpose: Data Analyst portfolio / practice project

Last updated: January 2026

Feel free to fork, use, or improve! 🍿
