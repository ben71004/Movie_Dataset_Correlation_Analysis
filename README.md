# Movie Industry Correlation Analysis

## Description

An exploratory data analysis project in Python that investigates which factors are related to a movie's financial success. Using a dataset of movies, the notebook cleans the data, fixes column types, extracts release years, and then measures how numeric features such as budget, votes, score, runtime and gross revenue relate to each other. The results are shown as a correlation matrix and a heatmap.

The project is a practical walkthrough of a standard data analysis workflow: load, inspect, clean, transform, and visualize.

## Goals

1. Load and inspect the movies dataset.
2. Find and handle missing values.
3. Convert columns to appropriate data types (for example, budget and gross to integers).
4. Extract a clean release year from the text `released` column.
5. Measure correlations between numeric variables.
6. Visualize the correlations with a heatmap and draw conclusions.

## Dataset

The analysis uses `movies.csv`, which contains one row per movie. Typical columns include:

| Column | Meaning |
| --- | --- |
| name | Movie title |
| rating | Age rating (for example PG, R) |
| genre | Main genre |
| year | Release year |
| released | Full release date with country |
| score | Audience rating score |
| votes | Number of votes |
| director, writer, star | Key people involved |
| country | Country of origin |
| budget | Production budget |
| gross | Worldwide gross revenue |
| company | Production company |
| runtime | Length in minutes |

Place `movies.csv` in the same folder as the notebook, or update the file path in the loading cell.

## Requirements

- Python 3.12 or 3.13 (very new Python versions may lack prebuilt packages for Jupyter dependencies on Windows)
- JupyterLab
- pandas
- numpy
- seaborn
- matplotlib
- openpyxl (only needed if you read Excel files)

## Setup

```bash
# create and activate a virtual environment (Windows)
py -3.13 -m venv jupyter-env
jupyter-env\Scripts\activate

# install the libraries
pip install jupyterlab pandas numpy seaborn matplotlib openpyxl

# launch Jupyter from the project folder
jupyter lab
```

## Usage

1. Open the notebook in JupyterLab.
2. Make sure `movies.csv` is in the project folder.
3. Run the cells from top to bottom.

## Method

**Loading.** The data is read with `pd.read_csv`.

**Missing values.** Missing values are counted with `df.isna().sum()`. Columns such as budget contain blanks, so they are stored as floats. They are either dropped, filled, or converted with the nullable `Int64` type before casting to integers.

**Data types.** Numeric columns are converted to integers so they behave correctly in calculations and charts.

**Year extraction.** The year is pulled from the `released` text (for example, `June 13, 1980 (United States)`) using string operations or a regular expression, then converted to a number.

**Correlation.** Correlation is calculated only on numeric columns:

```python
df.corr(numeric_only=True)
```

**Visualization.** The matrix is plotted as a heatmap:

```python
plt.figure(figsize=(8, 6))
sns.heatmap(df.corr(numeric_only=True), annot=True, cmap='coolwarm')
plt.show()
```

## Findings

Fill in after running the analysis. Typical points to cover:

- Which variable correlates most strongly with gross revenue (budget and votes are common candidates).
- Whether score is strongly related to revenue.
- Any weak or surprising relationships.

## Limitations

- Correlation does not imply causation.
- Rows with missing budget or gross values may be removed, which can bias results.
- Budgets and revenues are not adjusted for inflation, so older and newer films are not directly comparable.
- Text columns such as company or genre are not included in the numeric correlation unless they are encoded first, and the codes are arbitrary.

## Possible Extensions

- Encode categorical columns (genre, rating, company) and include them in the analysis.
- Adjust budget and gross for inflation.
- Compare correlations across decades or genres.
- Build a simple regression model to predict gross revenue.

## Author

Replace with your name and contact details.
