
# 📊 Banking Loan Analytics Project (Python)

## 📌 Project Overview

This project analyzes a banking loan dataset to derive **key performance indicators (KPIs)** and **business insights** that support data-driven lending decisions. Using **Python**, the analysis evaluates loan applications, funding performance, borrower behavior, and repayment trends through structured metrics and visualizations.

The objective is to help stakeholders monitor **loan portfolio health**, identify **risk patterns**, and understand **lending trends across time, geography, and borrower profiles**.

## 🛠️ Tools & Technologies

* **Python**
* **Pandas & NumPy** – Data cleaning & KPI calculations
* **Matplotlib / Seaborn / Plotly** – Data visualization
* **Google Colab** – Analysis & reporting


## 🎯 Key KPIs Analysis

### 1️⃣ Total Loan Applications

Calculates total loan applications and Month-to-Date (MTD) loan applications.

```python
Total_loan_applications = df['id'].count()
print("Total loan applications are ",Total_loan_applications )
```
Ans: Total loan applications are  38576


### MTD Loan Applications

```python
last_issue_date = df['issue_date'].max()
last_year = last_issue_date.year
last_month = last_issue_date.month
mtd_date = df[(df['issue_date'].dt.year == last_year) & (df['issue_date'].dt.month == last_month)]
mtd_loan_applications = mtd_date['id'].count()
print(f"MTD_Loan_applications for ({last_issue_date.strftime("%B %Y")}): {mtd_loan_applications} ")

```
Ans: MTD_Loan_applications for (December 2021): 4314

### 2️⃣ Total Funded Amount

Measures total loan amount disbursed and MTD funded amount.

```python
Total_funded_amount = df['loan_amount'].sum()
Total_funded_amount_millions = Total_funded_amount/1000000
print("Total funded amount is ${:.2f}M". format(Total_funded_amount_millions))
```
Ans: Total funded amount is $435.76M

```python
last_issue_date = df['issue_date'].max()
last_year = last_issue_date.year
last_month = last_issue_date.month

mtd_date = df[(df["issue_date"].dt.year == last_year) & (df["issue_date"].dt.month == last_month)]
mtd_funded_amount = mtd_date["loan_amount"].sum()
mtd_funded_amount_millions = mtd_funded_amount/1000000
print(f"MTD Funded amount for ({last_issue_date.strftime("%B %Y")}): ${mtd_funded_amount_millions:.2f}M")
```
Ans: MTD Funded amount for (December 2021): $53.98M

### 3️⃣ Total Amount Received

Tracks total repayments received and MTD received amount.

```python
Total_amt_received = df["total_payment"].sum()
Total_amt_received_millions = Total_amt_received/1000000
print("Total amount received is ${:.2f}M".format(Total_amt_received_millions))
```
Ans: Total amount received is $473.07M

```python
last_date = df['issue_date'].max()
last_year = last_date.year
last_month = last_date.month
mtd_date = df[(df['issue_date'].dt.year == last_year) & (df['issue_date'].dt.month == last_month )]
mtd_amount_received = mtd_date["total_payment"].sum()
mtd_amount_received_millions = mtd_amount_received/1000000
print(f" Total MTD Amount received for {last_date.strftime("%B %Y")}: ${mtd_amount_received_millions:.2f}M")
```
Ans: Total MTD Amount received for December 2021: $58.07M

### 4️⃣ Average Interest Rate

Calculates average interest rate across the loan portfolio.

```python
avg_interest_rate  = df["int_rate"].mean()*100
print(f"Average interest rate is {avg_interest_rate:.2f}%")
```
Ans: Average interest rate is 12.05%

### 5️⃣ Average Debt-to-Income Ratio (DTI)

Evaluates borrower financial health.

```python
Average_DTI = df['dti'].mean()*100
print(f"Average DTI is {Average_DTI:.2f}")
```
Ans: Average DTI is 13.33

## ✅ Good Loan vs Bad Loan Analysis

### 🟢 Good Loan Metrics

Loans marked as **Fully Paid** or **Current**.

```python
good_loans = df[df['loan_status'].isin(["Fully Paid" , "Current"])]

total_loan_applications = df['id'].count()

total_good_loans = good_loans['id'].count()
good_loans_percentage = (total_good_loans/total_loan_applications)*100

total_good_loan_funded_amt = good_loans["loan_amount"].sum()
total_good_loan_funded_amt_millions = good_loans["loan_amount"].sum()/1000000

total_good_loan_received_amount = good_loans['total_payment'].sum()
total_good_loan_received_amount_millions = good_loans['total_payment'].sum()/1000000

print("Total loan applications are ",total_loan_applications)
print("Total good loan applications are ",(total_good_loans))
print("Total good loans percentage is: {:.2f}% ".format(good_loans_percentage))
print("Total funded amount for good loans(in Millions) is ${:.2f}M".format(total_good_loan_funded_amt_millions))
print("Total received amount from good loans(in Millions) is ${:.2f}M".format(total_good_loan_received_amount_millions))
```
Ans: Total loan applications are  38576 <br>
Total good loan applications are  33243 <br>
Total good loans percentage is: 86.18% <br>
Total funded amount for good loans(in Millions) is $370.22M <br>
Total received amount from good loans(in Millions) is $435.79M

### 🔴 Bad Loan Metrics

Loans marked as **Charged off** .

```python
Total_loan_applications = df['id'].count()

bad_loans = df[df['loan_status'].isin(['Charged Off'])]

Total_bad_loans = bad_loans['id'].count()
Total_bad_loans_percentage = (Total_bad_loans/Total_loan_applications)*100

Bad_loan_funded_amt = bad_loans['loan_amount'].sum()
Bad_loan_funded_amt_millions = Bad_loan_funded_amt/1000000

Bad_loan_received_amt = bad_loans['total_payment'].sum()
Bad_loan_received_amt_millions = Bad_loan_received_amt/1000000

print("Total loan applications are ",Total_loan_applications)
print("Number of bad loan applications as ",Total_bad_loans )
print("Bad loan applications percentage is {:.2f}%".format(Total_bad_loans_percentage))
print("Total funded amount for bad loans(in Millions) is ${:.2f}M".format(Bad_loan_funded_amt_millions))
print("Total received amount from bad loans(in Millions) is ${:.2f}M".format(Bad_loan_received_amt_millions))
```
Ans: 
Total loan applications are  38576 <br>
Number of bad loan applications as  5333 <br>
Bad loan applications percentage is 13.82% <br>
Total funded amount for bad loans(in Millions) is $65.53M <br>
Total received amount from bad loans(in Millions) is $37.28M <br>


## 📈 Visual Analysis & Business Insights

### 📅 1 Monthly Trends by Issue Date

Identifies seasonality and long-term trends.
### 1.a Total Funded Amount by issue date
```python
monthly_funded = (
    df.sort_values('issue_date')
    .assign(month_name = lambda X: X['issue_date'].dt.strftime("%b %Y"))
    .groupby('month_name', sort = False)['loan_amount'].sum()
    .div(1000000)
    .reset_index(name = "loan_amount_millions")
)


plt.figure(figsize = (12,6))
plt.plot(monthly_funded['month_name'], monthly_funded['loan_amount_millions'], marker = 'o', color = 'blue', linewidth = 1)

for i, row in monthly_funded.iterrows():
  plt.text(
      i,
      row['loan_amount_millions']+0.2, f"${row['loan_amount_millions']:.2f}M",
           ha = 'center', va = 'bottom', fontsize = 10, rotation = 0, color = 'red'
           )

plt.title("Monthly Funded Amount(in Millions)", fontsize = 15)
plt.xlabel("Month")
plt.ylabel("Funded Amount($ in Millions)")
plt.xticks(rotation = 45)
plt.grid(True, linestyle = '--', alpha = 0.6)
plt.tight_layout()
plt.show()
```
📊 **Visualization**

![Total Funded Amount by issue date](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/1.a%20Monthly%20Funded%20Amount.png)

### 1.a For Area chart Funded Amount:
```python
monthly_funded = (
    df.sort_values('issue_date')
    .assign(month_name = lambda X: X['issue_date'].dt.strftime("%b %Y"))
    .groupby('month_name', sort = False)['loan_amount'].sum()
    .div(1000000)
    .reset_index(name = "loan_amount_millions")
)


plt.figure(figsize = (12,6))
plt.plot(monthly_funded['month_name'], monthly_funded['loan_amount_millions'], marker = 'o', color = 'blue', linewidth = 1)
plt.fill_between(monthly_funded['month_name'], monthly_funded['loan_amount_millions'], color = 'blue', alpha =0.2)

for i, row in monthly_funded.iterrows():
  plt.text(
      i,
      row['loan_amount_millions']+0.2, f"${row['loan_amount_millions']:.2f}M",
           ha = 'center', va = 'bottom', fontsize = 10, rotation = 0, color = 'blue', alpha = 1
           )

plt.title("Monthly Funded Amount(in Millions)", fontsize = 15)
plt.xlabel("Month")
plt.ylabel("Funded Amount($ in Millions)")
plt.xticks(rotation = 45)
plt.grid(True, linestyle = '--', alpha = 0.6)
plt.tight_layout()
plt.show()
```
### 1.b Total Received Amount by issue date
```python
monthly_received= (
    df.sort_values('issue_date')
    .assign(month_name= lambda x: x['issue_date'].dt.strftime("%b %Y"))
    .groupby("month_name", sort = False)['total_payment'].sum()
    .div(1000000)
    .reset_index(name = "total_received_millions")
)

plt.figure(figsize=(12,6))
plt.plot(monthly_received['month_name'], monthly_received['total_received_millions'],marker = 'o', color = 'red', linewidth = 1)

for i,row in monthly_received.iterrows():
  plt.text(i, row['total_received_millions']+0.2, f"${row['total_received_millions']:.2f}M",
           ha = "center", va = 'bottom', fontsize = 10, color = "black", alpha = 1, rotation = 0 )

plt.title("Total Amount Received (in Millions)", fontsize = 15, color = "black")
plt.xlabel("Month")
plt.ylabel("Total received Amount(in millions)")
plt.xticks(rotation=45)
plt.grid(True, linestyle = '--', alpha = 0.6)
plt.tight_layout()
plt.show()

```

📊 **Visualization**

![Total Amount Received by issue Date](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/1.b%20Total%20Amount%20received.png)

### 1.c Total Loan Applications by issue date
```python
monthly_applications= (
    df.sort_values('issue_date')
    .assign(month_name= lambda x: x['issue_date'].dt.strftime("%b %Y"))
    .groupby("month_name", sort = False)['id'].count()
    .reset_index(name = "total_loan_applications")
)

plt.figure(figsize=(12,6))
plt.plot(monthly_applications['month_name'], monthly_applications['total_loan_applications'],marker = 'o', color = 'darkgreen', linewidth = 1)

for i,row in monthly_applications.iterrows():
  plt.text(i, row['total_loan_applications']+0.2, f"{row['total_loan_applications']}",
           ha = "center", va = 'bottom', fontsize = 10, color = "black", alpha = 1, rotation = 0 )

plt.title("Total Loan Applications", fontsize = 15, color = "black")
plt.xlabel("Month")
plt.ylabel("Loans Applied")
plt.xticks(rotation=45)
plt.grid(True, linestyle = '--',color = "black", alpha = 0.2)
plt.tight_layout()
plt.show()
```

📊 **Visualization**

![Total Loan Applications by issue date](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/1.c%20Total%20Loan%20Applications.png)


### 🌍 2 Regional Analysis by State

### 2.a Total Funded Amount by State
```python
state_funding = df.groupby('address_state')['loan_amount'].sum().sort_values(ascending = True)
state_funding_thousands = state_funding / 1000

plt.figure(figsize = (14,8))
bars = plt.barh(state_funding_thousands.index, state_funding_thousands.values, color = 'blue', alpha = 0.3)

for bar in bars:
  width =bar.get_width()
  plt.text(width + 10, bar.get_y() + bar.get_height() /2, f'{width:,.0f}k', va = 'center',fontsize = 8)


plt.title('Total Funded Amount by state (in Thousands)')
plt.xlabel('Funded Amount(in Thousands)')
plt.ylabel('State')
plt.tight_layout()
plt.show()

```

📊 **Visualization**

![Total Funded Amount by State](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/2.a%20Total%20Funed%20Amount%20by%20state.png)

### 2.b Total Received Amount by State
```python
received_amount_bystate = df.groupby('address_state')['total_payment'].sum().sort_values(ascending = True)
received_amount_bystate_thousands = received_amount_bystate / 1000

plt.figure(figsize = (14,8))
bars = plt.barh(received_amount_bystate_thousands.index, received_amount_bystate_thousands.values, color = "red", alpha = 0.4)

for bar in bars:
  width = bar.get_width()
  plt.text(width+10, bar.get_y()+ bar.get_height()/2, f'{width:,.0f}K',va = 'center', color = "black", alpha = 1)

plt.title('Total Amount Received by state (in Thousands)')
plt.xlabel('Received Amount(in Thousands)')
plt.ylabel('State')
plt.tight_layout()
plt.show()
```

📊 **Visualization**

![Total Received Amount by State](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/2.b%20Total%20Received%20Amount%20by%20State.png)

### 2.c Total Loan Applications by State
```python
otal_loan_applications_bystate = df.groupby('address_state')['id'].count().sort_values(ascending = True)

plt.figure(figsize = (14,8))
bars = plt.barh(total_loan_applications_bystate.index, total_loan_applications_bystate.values, color = "green", alpha = 0.6)

for bar in bars:
  width = bar.get_width()
  plt.text(width+10, bar.get_y()+bar.get_height()/2, width, va = 'center', color = 'black', alpha = 1 )

plt.title('Total Loan Applications by state')
plt.xlabel('No of Loan Applications')
plt.ylabel('State')
plt.tight_layout()
plt.show()
```

📊 **Visualization**

![Total Loan Applications by State](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/2.c%20Total%20Loan%20Applications%20by%20state.png)


### ⏳3 Loan Term Analysis

Distribution of loans by term length.

### 3.a Total Funded Amount by Loan term
```python
termwise_funded_amount = df.groupby('term')['loan_amount'].sum()
termwise_funded_amount_millions = termwise_funded_amount/1000000

plt.figure(figsize = (5,5))
plt.pie(termwise_funded_amount_millions, labels = termwise_funded_amount_millions.index,
        autopct = lambda p: f'{p:.2f}% \n {p* sum(termwise_funded_amount_millions)/100 :.2f}M',
        startangle = 90, wedgeprops ={'width': 0.4}
        )

plt.gca().add_artist(
    plt.Circle((0, 0), 0.70, color='white'))

plt.title('Termwise Funded Amount(in Millions)')
plt.show()
```

📊 **Visualization**

![Total Funded Amount by Loan term](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/3.a%20Term%20Wise%20Funded%20Amount.png)

### 3.b Total Received Amount by State
```python
Termwise_received_amount = df.groupby('term')['total_payment'].sum()
Termwise_received_amount_millions = Termwise_received_amount/1000000

plt.figure(figsize = (4,4))
plt.pie(Termwise_received_amount_millions,labels = Termwise_received_amount_millions.index,
        colors = ['green', 'blue'],
        autopct = lambda p: f'{p:.2f}% \n {p*sum(Termwise_received_amount_millions)/100:.2f}M',
        startangle = 90, wedgeprops = {'width':0.4},
        )

plt.gca().add_artist( plt.Circle((0,0), 0.70, color = "White"))
plt.title('Termwise Received Amount')
plt.show
```

📊 **Visualization**

![Total Received Amount by State](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/3.b%20Termwise%20Received%20Amount.png)

### 3.c Total Loan Applications by state
```python
Termwise_loan_applications = df.groupby('term')['id'].count()

plt.figure(figsize = (4,4))
plt.pie(Termwise_loan_applications,labels = Termwise_loan_applications.index,
        colors = ['blue', 'lightgreen'],
        autopct = lambda p: f'{p:.2f}% \n {p*sum(Termwise_loan_applications)/100:.0f}',
        startangle = 90, wedgeprops = {'width':0.4},
        )

plt.gca().add_artist( plt.Circle((0,0), 0.70, color = "White"))
plt.title('Termwise Total Loan Applications')
plt.show()
```

📊 **Visualization**

![Total Loan Applications by state](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/3.c%20Term%20wise%20Total%20Loan%20Applications.png)


### 🧑‍💼 4 Employment Length Analysis

Impact of employment history on loan metrics.

### 4.a Total Funded Amount by Employment length
```python
emp_lengthwise_funded_amount = df.groupby('emp_length')['loan_amount'].sum().sort_values(ascending = True)
emp_lengthwise_funded_amount_Millions = emp_lengthwise_funded_amount/1000000

plt.figure(figsize = (10,6))
bars = plt.barh(emp_lengthwise_funded_amount_Millions.index,
                emp_lengthwise_funded_amount_Millions.values, color = 'red', alpha = 0.7)
for bar in bars:
  width = bar.get_width()
  plt.text(width+0.5, bar.get_y()+bar.get_height()/2, f'{width:,.0f}M', va = 'center', fontsize = 9)

plt.title("Employment Lengthwise Funded Amount(in Millions)")
plt.xlabel("Funded Amount(in Millions)")
plt.ylabel("Employment Length")
plt.tight_layout()
plt.show()
```

📊 **Visualization**


![Total Funded Amount by Employment length](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/4.a%20Employment%20length%20wise%20Funded%20Amount.png)

### 4.b Total Received Amount by employment length
```python
emp_lengthwise_received_amount = df.groupby('emp_length')['total_payment'].sum().sort_values(ascending = True)
emp_lengthwise_received_amount_Millions = emp_lengthwise_received_amount/1000000

plt.figure(figsize = (10,6))
bars = plt.barh(emp_lengthwise_received_amount_Millions.index,
                emp_lengthwise_received_amount_Millions.values, color = 'blue', alpha = 0.7)
for bar in bars:
  width = bar.get_width()
  plt.text(width+0.5, bar.get_y()+bar.get_height()/2, f'{width:,.0f}M', va = 'center', fontsize = 9)

plt.title("Employment Lengthwise received Amount(in Millions)")
plt.xlabel("Received Amount(in Millions)")
plt.ylabel("Employment Length")
plt.tight_layout()
plt.show()
```

📊 **Visualization**


![Total Received Amount by employment length](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/4.b%20Employment%20length%20wise%20Received%20Amount.png)

### 4.c Total Loan Applications
```python
emp_lengthwise_total_applications = df.groupby('emp_length')['id'].count().sort_values(ascending = True)

plt.figure(figsize = (10,6))
bars = plt.barh(emp_lengthwise_total_applications.index,
                emp_lengthwise_total_applications.values, color = 'orange', alpha = 0.7)
for bar in bars:
  width = bar.get_width()
  plt.text(width+0.5, bar.get_y()+bar.get_height()/2, f'{width:,.0f}', va = 'center', fontsize = 9)

plt.title("Employment Lengthwise Total Loan Applications")
plt.xlabel("Total Loan Applications")
plt.ylabel("Employment Length")
plt.tight_layout()
plt.show()
```

📊 **Visualization**

![Total Loan Applications](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/4.c%20Employment%20lengthwise%20Total%20loan%20Applications.png)

### 🎯5 Loan Purpose Breakdown

Primary reasons borrowers seek loans.

### 5.a Total Funded Amount by Purpose
```python
Loan_purpose_Funded_amount = df.groupby('purpose')['loan_amount'].sum().sort_values(ascending = True)
Loan_purpose_Funded_amount_Millions = Loan_purpose_Funded_amount/1000000

plt.figure(figsize = (12,6))
bars = plt.barh(Loan_purpose_Funded_amount_Millions.index,
                Loan_purpose_Funded_amount_Millions.values, color = "purple", alpha = 0.6)
for bar in bars:
  width = bar.get_width()
  plt.text(width+0.5, bar.get_y()+bar.get_height()/2, f'{width:.2f}M',va = 'center', fontsize =9)

plt.title("Total Funded Amount by Loan Purpose")
plt.xlabel("Total Funded Amount(in Millions)")
plt.ylabel("Loan Purpose")
plt.tight_layout()
plt.show()
```

📊 **Visualization**

![Total Funded Amount by Purpose](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/5.a%20Total%20Funded%20Amount%20by%20Purpose.png)

### 5.b Total Received Amount by purpose
```python
Loan_purpose_received_amount = df.groupby('purpose')['total_payment'].sum().sort_values(ascending = True)
Loan_purpose_received_amount_Millions = Loan_purpose_Funded_amount/1000000

plt.figure(figsize = (12,6))
bars = plt.barh(Loan_purpose_received_amount_Millions.index,
                Loan_purpose_received_amount_Millions.values, color = "green", alpha = 0.8)
for bar in bars:
  width = bar.get_width()
  plt.text(width+0.5, bar.get_y()+bar.get_height()/2, f'{width:.2f}M',va = 'center', fontsize =9)

plt.title("Total Received Amount by Loan Purpose")
plt.xlabel("Total Received Amount(in Millions)")
plt.ylabel("Loan Purpose")
plt.tight_layout()
plt.show()
```
📊 **Visualization**

![Total Received Amount by purpose](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/5.B%20Total%20Received%20amount%20by%20purpose.png)

### 5.c Total Loan Applications by purpose
```python
Loan_purpose_Total_Applications = df.groupby('purpose')['id'].count().sort_values(ascending = False)

plt.figure(figsize = (12,6))
bars = plt.bar(Loan_purpose_Total_Applications.index,
                Loan_purpose_Total_Applications.values, color = "blue", alpha = 0.8)
for bar in bars:
  height = bar.get_height()
  plt.text(bar.get_x()+bar.get_width()/2, height+5,  f'{height:.0f}',
           va = 'bottom', ha = 'center', fontsize =9, color = "black")

plt.title("Total Loan Applications by Loan Purpose")
plt.xlabel("Total Loan Applications")
plt.ylabel("Loan Purpose")
plt.xticks(rotation = 45)
plt.tight_layout()
plt.show()
```

📊 **Visualization**

![Total Loan Applications by purpose](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/5.c%20Tota%20Loans%20by%20Purpose.png)


### 🏠 6 Home Ownership Analysis

Impact of home ownership on lending.

### 6.a Total Funded Amount by Home ownership
```python
Funded_amount_Ownership_Millions = (
    df.groupby('home_ownership')['loan_amount']
      .sum()
      .sort_values(ascending=True)
      .div(1_000_000)
      .reset_index(name='Funded_amount_Ownership_Millions')
)

fig = px.treemap(
    Funded_amount_Ownership_Millions, path = ['home_ownership'],
    values = 'Funded_amount_Ownership_Millions',
    color = 'Funded_amount_Ownership_Millions',
    color_continuous_scale = 'Blues',
    title = 'Total Funded Amount by Home Ownership(in Millions)'
)

fig.show()
```

📊 **Visualization**

![Total Funded Amount by Home ownership](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/6.a%20Funded%20Ampunt%20by%20Home%20ownership.png)

### 6.b Total Received Amount by Home Ownership
```python
received_amount_Ownership_Millions = (
    df.groupby('home_ownership')['total_payment']
      .sum()
      .div(1_000_000)
      .reset_index(name='received_amount_Ownership_Millions')
)

fig = px.treemap(
    received_amount_Ownership_Millions, path = ['home_ownership'],
    values = 'received_amount_Ownership_Millions',
    color = 'received_amount_Ownership_Millions',
    color_continuous_scale = 'Blues',
    title = 'Received Amount by Home Ownership(in Millions)'
)
fig.update_traces(
    texttemplate=
    "<b>%{label}</b><br>"
    "%{value:.2f}M<br>"
    "%{percentParent:.2f}%"
)

fig.show()
```

📊 **Visualization**

![Total Received Amount by Home Ownership](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/6.b%20Received%20Amount%20by%20Home%20ownership.png)

### 6.c Total Received Amount by Home ownership
```python
loan_applications_homwownership = df.groupby('home_ownership')['id'].count().sort_values(ascending=False)

plt.figure(figsize=(10,6))
bars = plt.bar(
    loan_applications_homwownership.index,
    loan_applications_homwownership.values,
    color='grey',
    alpha=1
)


for bar in bars:
    height = bar.get_height()
    plt.text(
        bar.get_x() + bar.get_width()/2,
        height + 0.2,
        f'{height}',
        ha='center',
        va='bottom',
        fontsize=10,
        color='black'
    )

plt.title("Total Loan Applications baed on Home Ownership", fontsize=14, fontweight = 'bold')
plt.xlabel("Home Ownership Type")
plt.ylabel("Number of Loan Applications")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

📊 **Visualization**

![Total Received Amount by Home ownership](https://github.com/HarivandhanaRavikanti/Banking_Loan_Analysis_Python/blob/main/6.c%20Total%20Loan%20applications%20by%20Home%20ownership.png)

## 🚀 Key Takeaways

* Provides a **complete view of loan portfolio performance**
* Clearly distinguishes **Good vs Bad loan risk**
* Identifies **seasonality, regional trends, and borrower behavior**
* Demonstrates practical **Python-based banking analytics**

