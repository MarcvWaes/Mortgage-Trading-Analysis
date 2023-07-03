# Mortgage-Trading-Analysis

# Performed the following challenges:
- Data check
- Explore Data
- Analyze and Visualize data
- Dashboarding
- Communicate insights

# Performed DAX calculations:
- Loan to Value Ratio
  - Loan to Value Ratio = DIVIDE(sum(loan_data[loan_amount]),SUM(loan_data[property_value]),0)
- Monthly Income
  - Monthly Income = DIVIDE(SUM(loan_data[income_thousands]), 12)*1000
- Debt to Income Ratio
  - Debt to Income Ratio = DIVIDE(SUM(loan_data[recurring_monthly_debt]), [Monthly Income],0)
- Trade Status
  - Trade Status = IF(
  - ISBLANK(loan_status[file_in_audit]),
  - "Closed - Needs Audit",
  - IF (ISBLANK(loan_status[file_audit_complete]),
  - "Closed - In Audit", 
  - IF(ISBLANK(loan_status[file_sent_to_custodian]), 
  - "Closed - Audit Complete",
  - IF(ISBLANK(loan_status[file_at_custodian]), 
  - "Closed - File Sent to Custodian",
  - "Closed - Ready to Trade")))) 
- Payment Period
  - Payment Period = loan_balance[payment_periods_made]+1
- Amortization Amount
  - Amortization Amount = PPMT(loan_balance[interest_rate]/12, loan_balance[Payment Period], loan_balance[loan_term], loan_balance[current_balance],0,0)
- Scheduled Principal Balance
  - Scheduled Principal Balance = 
  - loan_balance[current_balance]
  - + IF(loan_balance[next_payment_due_date]
  - < loan_balance[Scheduled Next Payment Data], 
  - loan_balance[Amortization Amount],0)
- Scheduled Next Payment Date
  - Scheduled Next Payment Data = DATE(2021, 11, 1)
- Benchmark Test
  - Benchmark Test = IF(loan_data[max_price.Price] > loan_data[umbs_price], "True", "False")
- Trade Amount
  - Trade Amount = RELATED(loan_balance[Scheduled Principal Balance]) * [max_price.Price] / 100
- Trade Premium
  - Trade Premium = RELATED(loan_balance[Scheduled Principal Balance]) * loan_data[max_price.Price] / 100 - RELATED(loan_balance[Scheduled Principal Balance])
- WA Price
  - WA Price = DIVIDE(SUMX(loan_data, loan_data[max_price.Price]*RELATED(loan_balance[Scheduled Principal Balance])), SUM(loan_balance[Scheduled Principal Balance]), 0)
- Total Loan Revenue
  - Total Loan Revenue = SUMX(loan_data, loan_data[Trade Premium]+loan_data[origition_charges])
- Loan Gross Profit
  - Loan Gross Profit = SUMX(loan_data, [Total Loan Revenue] - loan_data[lender_credits])
- Loan Profit Margin
  - Loan Profit Margin = DIVIDE(loan_data[Loan Gross Profit], SUMX(loan_balance, loan_balance[Scheduled Principal Balance]),0)
- Target Profit
  - Target Profit Margin = DIVIDE(SUMX(loan_data, loan_data[target_profit]), SUMX(loan_data, loan_data[loan_amount]), 0)

# Dashboards:
- Loan Status
![0h3ds3s1 qkv](https://github.com/MarcvWaes/Mortgage-Trading-Analysis/assets/120553175/1d0268c2-1b36-49a3-9c95-196b4b63a219)

- Loan Balances
![mzszgeql xbe](https://github.com/MarcvWaes/Mortgage-Trading-Analysis/assets/120553175/696d2ce1-2793-4655-9840-081d7b347150)

- Trade Analysis
![awct3ful bs2](https://github.com/MarcvWaes/Mortgage-Trading-Analysis/assets/120553175/3c102ee1-4ac9-4526-a95f-1a62cebfde09)

- Trade Execution
![iiik2ciy r3d](https://github.com/MarcvWaes/Mortgage-Trading-Analysis/assets/120553175/0c93471d-ac55-4bd6-a6c9-ca990aa0378e)

- Profit Analysis
![1qd4spnz d54](https://github.com/MarcvWaes/Mortgage-Trading-Analysis/assets/120553175/3a20a576-883c-4b20-be75-091fff5c6735)

 
