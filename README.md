# Movie Dataset Correlation Analysis

## Description

This project is an exploratory data analysis of a movies dataset, written in Python in a Jupyter notebook. It cleans the data, fixes column types, extracts the release year from a text field, and then uses correlation analysis to find which features are most closely related to a film's gross earnings. The results are shown as scatter plots, a regression plot and correlation heatmaps.

The central question is: what drives a movie's gross revenue? The notebook looks at budget, votes, score, runtime and the production company.

## Notebook

`Movie_Dataset_Correlation_Analysis.ipynb`

## Dataset

The analysis uses `movies.csv`, with one row per movie. The columns used or referenced in the notebook include:

| Column | Meaning |
| --- | --- |
| name | Movie title |
| rating | Age rating |
| genre | Main genre |
| year | Release year as listed in the file |
| released | Release date with country, for example `June 13, 1980 (United States)` |
| score | Audience score |
| votes | Number of votes |
| director, writer, star | Key people involved |
| country | Country of origin |
| budget | Production budget |
| gross | Gross earnings |
| company | Production company |
| runtime | Length in minutes |

Update the file path in the data loading cell to match where `movies.csv` is stored on your machine.

## Requirements

Python 3.12 or 3.13 is recommended. The notebook installs its own dependencies in the first cell:

```
%pip install pandas numpy seaborn matplotlib openpyxl
```

Libraries used: pandas, numpy, seaborn, matplotlib (including pyplot and mlab) and openpyxl.

## How to Run

1. Install JupyterLab in a virtual environment and launch it from the project folder with `jupyter lab`.
2. Open `Movie_Dataset_Correlation_Analysis.ipynb`.
3. Edit the path in the `pd.read_csv` cell so it points to your copy of `movies.csv`.
4. Run the cells from top to bottom.

## Workflow

**1. Setup.** The libraries are imported, the `ggplot` plot style is applied, and the default figure size is set to 12 by 8.

**2. Loading and inspecting.** The data is read with `pd.read_csv` and previewed with `df.head()`. The percentage of missing values in each column is printed, and `df.dtypes` is used to check the data types.

**3. Cleaning.** Rows with missing `budget` or `gross` values are dropped, and both columns are converted to `int64`. Dropping the missing rows first is what makes the integer conversion possible, because integer columns cannot hold missing values.

**4. Year correction.** A new column, `year_corrected`, is built from the `released` text. The string is split at the opening bracket to remove the country, then split at the comma to keep only the year.

**5. Sorting and duplicates.** The data is sorted by `gross` in descending order, the display limit for rows is removed, and the unique production companies are listed.

**6. Budget versus gross.** A matplotlib scatter plot and a seaborn regression plot (`sns.regplot`) show how budget relates to gross earnings.

**7. Correlation of numeric features.** The Pearson correlation matrix is calculated with `df.corr(numeric_only=True, method='pearson')` and drawn as an annotated seaborn heatmap.

**8. Including text columns.** Text columns such as company are converted to numeric category codes with `astype('category').cat.codes`, and the correlation matrix and heatmap are produced again so that categorical features can be compared as well.

**9. Strongest relationships.** The correlation matrix is unstacked into pairs, sorted, and filtered to show pairs with a correlation above 0.5.

## Findings

The conclusions recorded in the notebook are:

1. Budget and gross earnings show a high correlation.
2. Votes and budget have the highest correlation with gross earnings.
3. The production company has no meaningful correlation with gross earnings.

## Limitations

1. Correlation does not show causation. A larger budget may go with higher earnings without causing them.
2. Rows with a missing budget or gross value were removed, which may bias the results toward films with better record keeping.
3. Budget and gross are not adjusted for inflation, so films from different decades are not directly comparable.
4. The category codes used for text columns are arbitrary numbers, so the correlations involving them should be read with caution. A near zero value for company mainly shows that the numbering has no order, not that company never matters.
5. The `year_corrected` column is stored as text, so it is not included in numeric correlations unless it is converted first.

## Possible Extensions

1. Convert `year_corrected` to a number and include it in the correlations.
2. Adjust budget and gross for inflation.
3. Compare correlations by genre or decade.
4. Build a regression model to predict gross earnings.

## Acknowledgements

This project follows the approach taught in the "Data Analyst Portfolio Project | Correlation in Python" video by Alex The Analyst: https://youtu.be/iPYVYBtUTyE

The dataset is the Movies dataset published on Kaggle by danielgrijalvas: https://www.kaggle.com/datasets/danielgrijalvas/movies

I worked through the project myself in JupyterLab, adapted the code to run on current versions of pandas and Python, and wrote this README, including the findings and limitations sections.

## Author

Benjamin Joseph
