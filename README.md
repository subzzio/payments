# Create README.md file
readme_content = """# Task 13: Digital Payment Analytics - Personal UPI Data Analysis

## 1. Problem Statement
Analyze personal UPI transaction data to understand spending patterns, identify saving opportunities, and gain insights into financial behavior. This project creates a comprehensive analytics dashboard to track income, expenses, and savings.

## 2. Dataset Description
- **Source:** Personal UPI transaction history
- **Time Period:** 2023 - 2024
- **Records:** {:,} transactions
- **Features:** Date, Category, Withdrawal, Deposit, Balance, Reference Number

## 3. Key Insights
### Financial Overview
- **Total Income:** Rs {:,}
- **Total Expenses:** Rs {:,}
- **Net Savings:** Rs {:,}
- **Savings Rate:** {:.2f}%

### Top Spending Categories
{}

### Monthly Averages
- **Average Monthly Expense:** Rs {:,}
- **Average Daily Spend:** Rs {:,}
- **Final Balance:** Rs {:,}

## 4. Dashboard Screenshots

### Page 1: Executive Overview
![Executive Overview](images/page-1_db.png)

### Page 2: Transaction Dashboard (Main)
![Transaction Dashboard](images/page-2_db.png)

### Page 2.2: Category Analysis
![Category Analysis](images/page-2.2_db.png)

### Page 3: Financial Health (Main)
![Financial Health](images/page-3_db.png)

### Page 3.2: Detailed Health
![Detailed Health](images/page-3.2_db.png)

## 5. Key Recommendations
- **Reduce {0} spending** - Highest expense category
- **Increase savings rate** to 20% (currently {1:.2f}%)
- **Track daily spending** to avoid overspending
- **Create monthly budget** for each category

## 6. Tools Used
- **Python:** Pandas, NumPy, Matplotlib, Seaborn, Plotly
- **Jupyter Notebook** for analysis
- **Power BI** for dashboard creation

## 7. Project Structure
TASK_13_Digital_Payment_Analytics/
├── data/ # Raw and cleaned datasets
├── notebook/ # Jupyter analysis notebook
├── dashboard/ # Power BI dashboard file
├── images/ # Dashboard screenshots
├── reports/ # Financial insights report
├── README.md # Project documentation
└── requirements.txt # Python dependencies

text

## 8. How to Run This Project
1. Install dependencies: `pip install -r requirements.txt`
2. Run Jupyter Notebook and execute all cells
3. Open Power BI and import cleaned data
4. Explore the 5 dashboard pages

## 9. Future Scope
- Predictive analytics for spending patterns
- Automated monthly budget alerts
- Bank API integration for real-time tracking
- Mobile dashboard for expense tracking
"""

# Calculate values
top_cat = df[df['Withdrawal'] > 0].groupby('Category')['Withdrawal'].sum().sort_values(ascending=False)
top_cat_str = '\n'.join([f'   - **{cat}:** Rs {amt:,.2f}' for cat, amt in top_cat.head(5).items()])

# Write README.md
with open('../README.md', 'w', encoding='utf-8') as f:
    f.write(readme_content.format(
        len(df), total_income, total_expenses, net_savings, savings_rate,
        top_cat_str, avg_monthly_expense, avg_daily_spend, df['Balance'].iloc[-1],
        top_cat.index[0] if len(top_cat) > 0 else 'N/A',
        savings_rate,
        top_cat.index[1] if len(top_cat) > 1 else 'N/A'
    ))

print("✅ README.md created successfully!")

