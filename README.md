# EDA-Travel: Travel Package Customer Analysis

Exploratory data analysis of 4,888 travel-agency customer records to find who buys a travel package (`ProdTaken`).
The notebook cleans the data, explores it with charts, and prepares features for a future prediction model.
Overall, 18.8% of contacted customers (920 of 4,888) bought a package.

## Project Files

| File | Description |
|---|---|
| `Travel.csv` | Raw dataset: 4,888 rows × 20 columns |
| `EDA-Travel.ipynb` | Notebook: cleaning, EDA, feature engineering, encoding. Findings are in its comments; there is no separate report |
| `README.md` | This file |

## Dataset

Source and data dictionary are not documented in the repo. Descriptions are inferred from column names.

| Column(s) | Description |
|---|---|
| `CustomerID` | Unique ID (200000–204887) |
| `ProdTaken` | Target: 1 = package bought, 0 = not |
| `Age`, `MonthlyIncome` | Age (18–61) and monthly income (1,000–98,678) |
| `Gender`, `MaritalStatus`, `Occupation`, `Designation` | Demographics; designation is Executive, Manager, Senior Manager, AVP or VP |
| `CityTier`, `TypeofContact` | City tier (1–3); Self Enquiry or Company Invited |
| `ProductPitched` | Basic, Deluxe, Standard, Super Deluxe, King |
| `DurationOfPitch`, `NumberOfFollowups`, `PitchSatisfactionScore` | Pitch length (unit undocumented), follow-ups (1–6), satisfaction (1–5) |
| `PreferredPropertyStar` | Preferred hotel star rating (3–5) |
| `NumberOfTrips` | Number of trips taken (time period not documented) |
| `NumberOfPersonVisiting`, `NumberOfChildrenVisiting` | Travel party size and children count |
| `Passport`, `OwnCar` | Binary flags (1 = yes) |

## Approach

1. **Understand:** load 4,888 × 20 table; 7 integer, 7 float, 6 text columns; check nulls and category values.
2. **Clean:** fix `Fe Male` → `Female`; drop `CustomerID`; drop every row with a missing value (4,888 → 4,128).
3. **Analyse:** count plots and histograms; marital status vs purchase; violin, swarm and 3D plots; correlation heatmap.
4. **Engineer:** add `TotalVisiting` (persons + children); 80/20 train/test split (`random_state=1`); one-hot encode and standardise.
5. **Report:** observations kept as notebook comments; the numbers below were recomputed from `Travel.csv`.

## Key Insights

Conversion rates use all 4,888 rows (blanks in a field excluded for that field). These are associations, not causes.

| Factor | Converts best | Converts worst |
|---|---|---|
| Passport | Holders: 34.7% (n=1,422) | None: 12.3% (n=3,466) |
| Package pitched | Basic: 30.0% (n=1,842) | Super Deluxe 5.8%, King 8.7%, Deluxe 11.8% |
| Marital status | Single: 33.2% (n=916) | Divorced 13.1%, Married 13.9% |
| Age band | 18–29: 32.0% (n=916) | 40–49: 13.7%, 30–39: 16.5% |
| Income quartile | Lowest (≤20,346): 26.4% | Highest (>25,571): 12.4% |
| Follow-ups | 6: 39.7% (n=136), 5: 24.9% | 1–2: 10.5–11.4% |
| City tier | Tier 3: 23.6%, Tier 2: 23.2% | Tier 1: 16.3% |
| Preferred star | 5-star: 26.2% | 3-star: 16.1% |

- Passport holders are 29% of customers but 54% of buyers. Basic is 60% of buyers.
- Executives (Basic) with a passport convert at 56.7% (n=568). Singles under 30 convert at 53.9% (n=256).
- Little or no signal: `OwnCar` (18.5% vs 19.4%) and `PitchSatisfactionScore` (15.0–21.6%, not monotonic).

## Tech Stack

- Python 3 (notebook metadata: 3.11.7) in Jupyter
- pandas, NumPy for cleaning; Matplotlib, Seaborn for charts (incl. 3D scatter)
- scikit-learn: `train_test_split`, `OneHotEncoder`, `StandardScaler`, `ColumnTransformer`

## How to Use

1. Keep `Travel.csv` next to the notebook (it is read by relative path).
2. Install packages (no requirements file; taken from the notebook imports): `pip install pandas numpy matplotlib seaborn scikit-learn jupyter`
3. Run `jupyter notebook EDA-Travel.ipynb` and choose **Run All**, or open the notebook on GitHub to read the saved outputs.
