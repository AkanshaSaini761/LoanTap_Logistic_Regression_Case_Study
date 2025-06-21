# 💳 LoanTap Personal Loan Creditworthiness Case Study

## 🏢 About LoanTap
**LoanTap** is an innovative online lending platform offering customized loan products tailored for millennials. Their portfolio includes:
- Personal Loan
- EMI Free Loan
- Personal Overdraft
- Advance Salary Loan

This case study focuses on the **Personal Loan** underwriting process.

## 🎯 Objective
To determine **creditworthiness** of individual borrowers using **logistic regression**.  
The goal is to help LoanTap:
- Minimize defaults (NPA risk)
- Optimize approvals for reliable borrowers
- Understand key factors driving loan defaults

## 📁 Dataset Overview

**Source:** [LoanTapData.csv](https://drive.google.com/file/d/1xzH4sDLFE-7WkX2MlRbv3d8NEE7cSa8i/view?usp=drive_link)

| Column Name              | Description |
|--------------------------|-------------|
| `loan_amnt`              | Loan amount requested by the borrower (can reflect adjustments made by credit department) |
| `term`                   | Loan duration in months (typically 36 or 60) |
| `int_rate`               | Interest rate on the loan |
| `installment`            | Monthly EMI the borrower will pay if loan is approved |
| `grade`                  | LoanTap-assigned loan grade (credit quality indicator) |
| `sub_grade`              | More granular subgrade under the assigned loan grade |
| `emp_title`              | Borrower’s job title at time of application |
| `emp_length`             | Borrower’s employment length in years (0 to 10, where 10 = 10+ years) |
| `home_ownership`         | Borrower’s home ownership status (e.g., Rent, Own, Mortgage) |
| `annual_inc`             | Borrower’s self-reported annual income |
| `verification_status`    | Indicates whether income is verified by LoanTap |
| `issue_d`                | Month and year the loan was funded |
| `loan_status`            | **Target variable** indicating current loan status |
| `purpose`                | Purpose category selected by borrower (e.g., debt consolidation, education) |
| `title`                  | Free-form loan title entered by the borrower |
| `dti`                    | Debt-to-Income ratio (excluding mortgage and current requested loan) |
| `earliest_cr_line`       | Date of borrower's earliest reported credit line |
| `open_acc`               | Number of currently open credit lines |
| `pub_rec`                | Number of derogatory public records (e.g., bankruptcies, liens) |
| `revol_bal`              | Total revolving credit balance |
| `revol_util`             | Percentage of revolving credit used (credit utilization) |
| `total_acc`              | Total number of credit lines in borrower's credit file |
| `initial_list_status`    | Initial listing status of the loan (`W` or `F`) |
| `application_type`       | Whether the application is individual or joint |
| `mort_acc`               | Number of mortgage accounts held by the borrower |
| `pub_rec_bankruptcies`   | Number of public record bankruptcies |
| `Address`                | Address of the borrower (used for location-based analysis, if needed) |

## 🔍 Analysis Goals

- Explore relationship between **`loan_status`** and **predictors**
- Clean and preprocess features (**missing, outliers, transformations**)
- Engineer risk-related binary flags (e.g., **public records, bankruptcy**)
- Use **logistic regression** to build a classification model
- Analyze results using **precision-recall tradeoff**

### 📊 Exploratory Analysis

- Univariate & Bivariate analysis
- Outlier handling using IQR
- Missing value treatment
- Correlation heatmaps
- Income, grade, purpose vs. default rate

### ⚙️ Feature Engineering

- Created flags:
  - `pub_rec_flag`, `mort_acc_flag`, `bankruptcy_flag`
- Extracted ZIP code from address
- Encoded categorical variables (One-hot encoding)
- Scaled numerical features using `StandardScaler`

### 📈 Model Building

- Model: **Logistic Regression**
- Libraries used: `sklearn`, `statsmodels`
- Train/Test split: 80/20

#### 🧪 Evaluation Metrics

- Classification Report (Precision, Recall, F1-score)
- ROC AUC Score
- Precision-Recall Curve
- Confusion Matrix

## 📊 Key Insights

- **80%** of customers repaid fully; **20%** defaulted
- **Loan Amount ↔ Installment** correlation = **0.95**
- **Grade A1** has highest repayment reliability; **G5** shows highest default
- **Mortgage** is the most common home ownership status (~50%)
- **Top job titles**: Manager, Teacher (stable income profiles)
- **Longer loan terms (60 months)** are linked to higher defaults
- **Debt Consolidation** and **Credit Card** loans dominate among defaulters
- **Zip codes like 11650, 86630, 93700** have **100% default rates**
- **Post-SMOTE Recall ↑ from 46% to 81%**, **Precision ↓ from 94% to 48%**
- **Accuracy ↓ from 89% to 79%** after SMOTE (tradeoff handled via F1-score)
- **Weighted F1-score = 0.88**, balancing precision and recall


## 📈 Tradeoff Analysis

> Balancing precision and recall is critical in financial decision-making.

- **High Precision**: Minimizes false positives → avoids lending to defaulters  
- **High Recall**: Minimizes false negatives → ensures defaulters are caught  
- **SMOTE** was used to increase recall while accepting some drop in precision  
- ROC-AUC and PR Curves used for evaluating threshold adjustments

## 📋 Questionnaire Highlights

1. **% Fully Paid Loans**: ~80%  
2. **LoanAmt vs Installment**: Strong correlation (0.95)  
3. **Most Common Home Ownership**: Mortgage  
4. **Grade A borrowers repay better**: ✅ True (93% repayment)  
5. **Top Job Titles**: Manager, Teacher  
6. **Most important metric for banks**: **Precision**  
7. **Gap in Precision & Recall**: Affects profitability and risk directly  
8. **Top Predictive Features**: Zip code, grade, application_type, income, loan_amnt  
9. **Location Matters?** ✅ Yes (ZIP code affects outcome)

## ✅ Recommendations

1. **Enhance Data Balance**  
   Use SMOTE or similar techniques to ensure fair learning from defaulters and non-defaulters

2. **Prioritize Risk Indicators**  
   Features like `grade`, `zip_code`, `dti`, `revol_util`, and `purpose` strongly affect outcomes

3. **Advanced Modeling**  
   Try ensemble models like **Random Forest**, **Gradient Boosting**, or **Neural Nets** for deeper insights

4. **Adaptive Thresholds**  
   Tune classification thresholds dynamically to meet business goals (risk-tolerant vs growth-oriented)

5. **Ongoing Model Monitoring**  
   Set up validation and performance pipelines to adapt to changing credit behavior trends


## 🛠 Tools & Libraries Used

- **Python**: `Pandas`, `NumPy`, `Matplotlib`, `Seaborn`
- **Modeling**: `scikit-learn`, `statsmodels`
- **Preprocessing**: `StandardScaler`, `OneHotEncoder`, `SMOTE` (imbalanced-learn)
- **Evaluation**: ROC AUC, Precision-Recall Curve, Classification Report
- **Environment**: Jupyter Notebook


## 📄 Output Report

All analysis, preprocessing steps, and model results are detailed in the PDF file:  
📎 [`LoanTap_case_study_akansha_saini.pdf`](https://github.com/AkanshaSaini761/LoanTap_Logistic_Regression_Case_Study/blob/main/LoanTap_case_study_akansha_saini.pdf)

