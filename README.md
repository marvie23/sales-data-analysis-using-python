# Sales-Data-Analysis-using-python
This project explores and analyzes retail sales data using Python. It identifies business insights, sales patterns, and profitability across products and regions.
#  Sales Data Analysis

This project explores and analyzes retail sales data using Python. It identifies business insights, sales patterns, and profitability across products and regions.

---

##  Dataset Description

The dataset includes the following fields:

- `Order ID`
- `Order Date`
- `Category`, `Sub-Category`
- `Amount`, `Profit`, `Quantity`
- `State`, `City`
- `PaymentMode`
- `CustomerName`

---

##  Business Questions Answered

1. Which product categories generate the highest revenue?
2. What is the average sales per transaction by state?
3. What is the trend of total monthly sales?
4. What are the top 5 products by quantity and revenue?
5. What days of the week generate the most revenue?
6. Which products sell in the lowest quantities?
7. Which products yield high sales but low profit margins?

---

##  Tools & Libraries Used

```bash
python
pandas
matplotlib
seaborn
```

##  Key Insights

###  1. Revenue by Category
```python
data.groupby('Category')['Amount'].sum().sort_values(ascending=False)
```
> Electronics generated the highest total revenue.

---

###  2. Average Sales by State
```python
data.groupby('State')['Amount'].mean().sort_values(ascending=False).head(10)
```
> States like **California** and **New York** have the highest average sales per order.

---

###  3. Monthly Sales Trend
```python
monthly_sales = data.groupby('Year-Month')['Amount'].sum()
monthly_sales.plot(kind='line', marker='o')
```
> Sales show seasonal peaks — indicating influence from holidays or promotions.

---

###  4. Top-Selling Products
```python
# By Quantity
data.groupby('Sub-Category')['Quantity'].sum().sort_values(ascending=False).head(5)

# By Revenue
data.groupby('Sub-Category')['Amount'].sum().sort_values(ascending=False).head(5)
```
> High quantity: Phones, Chairs  
> High revenue: Laptops, Printers

---

### 🔹 . Sales by Day of the Week
```python
data['Order Date'] = pd.to_datetime(data['Order Date'])
data['DayOfWeek'] = data['Order Date'].dt.day_name()
data.groupby('DayOfWeek')['Amount'].sum().sort_values(ascending=False)
```
> Peak sales occur on **Friday** and **Saturday**

---

###  6. Low-Selling Products
```python
data.groupby('Sub-Category')['Quantity'].mean().sort_values().head(10)
```
> Some products like Scanners or Copiers are sold in very low quantities.

---

###  7. Profit Margin by Product
```python
profit_margin = data.groupby('Sub-Category')[['Amount', 'Profit']].sum()
profit_margin['Margin %'] = (profit_margin['Profit'] / profit_margin['Amount']) * 100
profit_margin.sort_values(by='Margin %')
```
> Products like **Printers** have low profit margins despite high revenue.

---

##  Recommendations

- Promote high-margin best-sellers more heavily.
- Investigate low-margin, high-revenue products for cost optimization.
- Optimize inventory for slow-moving products.
- Focus marketing on high-performing states and weekend shoppers.
