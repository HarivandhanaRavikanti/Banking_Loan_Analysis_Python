
# 📊 Banking Loan Analytics Project (Python)

## 📌 Project Overview

This project analyzes a banking loan dataset to derive **key performance indicators (KPIs)** and **business insights** that support data-driven lending decisions. Using **Python**, the analysis evaluates loan applications, funding performance, borrower behavior, and repayment trends through structured metrics and visualizations.

The objective is to help stakeholders monitor **loan portfolio health**, identify **risk patterns**, and understand **lending trends across time, geography, and borrower profiles**.

---

## 🛠️ Tools & Technologies

* **Python**
* **Pandas & NumPy** – Data cleaning & KPI calculations
* **Matplotlib / Seaborn / Plotly** – Data visualization
* **Google Colab** – Analysis & reporting

---

## 🎯 Key KPIs Analysis

### 1️⃣ Total Loan Applications

Calculates total loan applications and Month-to-Date (MTD) loan applications.

```python
Total_Loan_Applications = df['id'].count()

last_issue_date = df['issue_date'].max()
mtd_loan_applications = df[
    (df['issue_date'].dt.year == last_issue_date.year) &
    (df['issue_date'].dt.month == last_issue_date.month)
]['id'].count()
```

📊 **Visualization**
![Total Loan Applications](total_loan_applications.png)

---

### 2️⃣ Total Funded Amount

Measures total loan amount disbursed and MTD funded amount.

```python
Total_funded_amount = df['loan_amount'].sum() / 1_000_000

mtd_funded_amount = df[
    (df['issue_date'].dt.year == last_issue_date.year) &
    (df['issue_date'].dt.month == last_issue_date.month)
]['loan_amount'].sum() / 1_000_000
```

📊 **Visualization**
![Total Funded Amount](total_funded_amount.png)

---

### 3️⃣ Total Amount Received

Tracks total repayments received and MTD received amount.

```python
Total_amt_received = df['total_payment'].sum() / 1_000_000

mtd_amount_received = df[
    (df['issue_date'].dt.year == last_issue_date.year) &
    (df['issue_date'].dt.month == last_issue_date.month)
]['total_payment'].sum() / 1_000_000
```

📊 **Visualization**
![Total Amount Received](total_amount_received.png)

---

### 4️⃣ Average Interest Rate

Calculates average interest rate across the loan portfolio.

```python
avg_interest_rate = df['int_rate'].mean() * 100
```

---

### 5️⃣ Average Debt-to-Income Ratio (DTI)

Evaluates borrower financial health.

```python
Average_DTI = df['dti'].mean() * 100
```

---

## ✅ Good Loan vs Bad Loan Analysis

### 🟢 Good Loan Metrics

Loans marked as **Fully Paid** or **Current**.

```python
good_loans = df[df['loan_status'].isin(['Fully Paid', 'Current'])]

good_loan_percentage = (
    good_loans['id'].count() / df['id'].count()
) * 100
```

📊 **Visualization**
![Good Loans](good_loans.png)

---

### 🔴 Bad Loan Metrics

Loans marked as **Charged Off**.

```python
bad_loans = df[df['loan_status'] == 'Charged Off']

bad_loan_percentage = (
    bad_loans['id'].count() / df['id'].count()
) * 100
```

📊 **Visualization**
![Bad Loans](bad_loans.png)

---

## 📈 Visual Analysis & Business Insights

### 📅 Monthly Trends by Issue Date

Identifies seasonality and long-term trends.

```python
monthly_funded = (
    df.assign(month=df['issue_date'].dt.strftime('%b %Y'))
      .groupby('month')['loan_amount']
      .sum() / 1_000_000
)
```

📊 **Visualization**
![Monthly Trends](monthly_trends.png)

---

### 🌍 Regional Analysis by State

Shows geographic distribution of lending.

```python
state_funding = df.groupby('address_state')['loan_amount'].sum() / 1000
```

📊 **Visualization**
![Regional Analysis](regional_analysis.png)

---

### ⏳ Loan Term Analysis

Distribution of loans by term length.

```python
termwise_funded_amount = df.groupby('term')['loan_amount'].sum() / 1_000_000
```

📊 **Visualization**
![Loan Term Distribution](loan_term.png)

---

### 🧑‍💼 Employment Length Analysis

Impact of employment history on loan metrics.

```python
emp_lengthwise_funded = df.groupby('emp_length')['loan_amount'].sum() / 1_000_000
```

📊 **Visualization**
![Employment Length Analysis](employment_length.png)

---

### 🎯 Loan Purpose Breakdown

Primary reasons borrowers seek loans.

```python
loan_purpose = df.groupby('purpose')['loan_amount'].sum() / 1_000_000
```

📊 **Visualization**
![Loan Purpose Analysis](loan_purpose.png)

---

### 🏠 Home Ownership Analysis

Impact of home ownership on lending.

```python
home_ownership_funded = (
    df.groupby('home_ownership')['loan_amount']
      .sum() / 1_000_000
)
```

📊 **Visualization**
![Home Ownership Analysis](home_ownership.png)

---

## 🚀 Key Takeaways

* Provides a **complete view of loan portfolio performance**
* Clearly distinguishes **Good vs Bad loan risk**
* Identifies **seasonality, regional trends, and borrower behavior**
* Demonstrates practical **Python-based banking analytics**


---


