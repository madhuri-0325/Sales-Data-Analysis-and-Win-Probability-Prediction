# Sales-Data-Analysis-and-Win-Probability-Prediction
## Project Overview
This project involves a comprehensive analysis of B2B sales data to identify key performance drivers and predict deal win probability. The analysis covers revenue distribution, win rates across various dimensions (industry, region, product, lead source), sales cycle dynamics, and time-based trends. A Logistic Regression model is then developed to predict deal outcomes and understand the factors influencing win probability.

## Approach

The analysis was conducted in several stages:

### 1. Data Loading and Initial Exploration
- Loaded the `skygeni_sales_data.csv` dataset into a pandas DataFrame.
- Performed initial data inspection using `df.info()` to check data types and non-null counts.
- Checked for duplicate rows using `df.duplicated().sum()`.
- Converted `created_date` and `closed_date` columns to datetime objects.
- Generated descriptive statistics for all columns, including categorical features, using `df.describe(include='all').T`.

### 2. Revenue Analysis
- Calculated the total revenue from 'Won' deals.
- Visualized the distribution of deal amounts for 'Won' deals using a histogram to understand revenue concentration.

### 3. Win Rate Analysis
- Calculated the overall win rate for all deals.
- Analyzed win rates by different categorical features: `industry`, `region`, `product_type`, and `lead_source`.
- Investigated revenue and average deal size by industry, region, product, and lead source to identify top-performing segments.

### 4. Sales Cycle Analysis
- Examined the correlation between `deal_amount` and `sales_cycle_days` to determine if larger deals require longer sales cycles.
- Visualized this relationship using a scatter plot.

### 5. Time-Based Analysis
- Analyzed the monthly revenue trend based on `closed_date` to observe growth patterns and seasonality.
- Compared the average `deal_amount` for 'Won' versus 'Lost' deals to understand if deal size impacts outcome.

### 6. Win Probability Prediction (Logistic Regression Model)
- **Business Problem**: To identify which deals are more likely to close and why.
- **Goal**: Build a model that predicts win probability and identifies key drivers.
- **Data Preparation**:
    - Created a binary target variable `won_flag` (1 for 'Won', 0 for 'Lost').
    - Selected meaningful features: `deal_amount`, `sales_cycle_days`, `industry`, `region`, `product_type`, `lead_source`.
    - Applied one-hot encoding to categorical features to prepare them for the model.
    - Split the data into training and testing sets (80% train, 20% test).
- **Model Training and Evaluation**:
    - Trained a Logistic Regression model on the training data.
    - Evaluated the model using a classification report and ROC-AUC score on the test set.
- **Interpretation**:
    - Extracted and interpreted the coefficients of the Logistic Regression model to understand feature importance.
    - Created a `win_probability` column and a `win_segment` (High, Medium, Low) based on predicted probabilities.
    - Plotted the Precision-Recall curve to further assess model performance.

## Key Decisions

- **Feature Selection for Model**: Only variables available *before* a deal is closed (`deal_amount`, `sales_cycle_days`, `industry`, `region`, `product_type`, `lead_source`) were used to avoid data leakage and ensure real-world usability. Fields like `closed_date` or `deal_stage` were excluded as they could indirectly reveal the outcome.
- **Model Choice**: Logistic Regression was chosen as the baseline model due to its simplicity, interpretability, and suitability for binary classification. It allows for clear understanding of how each feature influences win probability through its coefficients.
- **Handling Categorical Variables**: One-hot encoding was used for categorical features to convert them into a numerical format suitable for logistic regression, with `drop_first=True` to avoid multicollinearity.
- **Interpretation of Model Limitations**: Despite the model build, the low ROC-AUC score and flat Precision-Recall curve indicated that the chosen structured features do not strongly determine win probability. This led to the conclusion that unobserved variables (e.g., sales rep skill, pricing strategy, competitive dynamics) likely play a more significant role.

## How to Run the Project

### Prerequisites
- Python 3.x
- Jupyter Notebook or Google Colab
- Required Python libraries: `pandas`, `numpy`, `seaborn`, `matplotlib`, `scikit-learn`

### Installation
If you don't have the libraries installed, you can install them using pip install pandas numpy seaborn matplotlib scikit-learn


### Steps to Run
Clone the repository:
git clone <repository_url>
cd <repository_name>
#### Download the dataset: Ensure skygeni_sales_data.csv is in the same directory as the notebook.
#### Open the notebook: Launch Jupyter Notebook or Google Colab and open the .ipynb file.
#### Run all cells: Execute all cells in the notebook sequentially. The analysis and model building steps will be performed, and outputs (plots, tables, model metrics) will be displayed.

## Summary of Findings & Model Insights
The initial exploratory analysis revealed a right-skewed revenue distribution, suggesting a few high-value deals significantly impact total revenue. Win rates were found to be relatively consistent across industries, regions, products, and lead sources, hovering around 45%. India, Ecommerce, and Inbound leads showed high deal volumes and revenue contributions. There was no strong correlation between deal size and sales cycle duration.

The Logistic Regression model, while interpretable, showed limited predictive power (ROC-AUC ~0.49). This suggests that the available structured data features are not strong drivers of deal win probability, implying that other, uncaptured factors are more influential in determining deal outcomes. Therefore, the model cannot reliably predict win probability based on the current feature set, and further data collection or a different modeling approach might be required for better prediction. ```
