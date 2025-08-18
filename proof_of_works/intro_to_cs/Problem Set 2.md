Each month, a credit card statement will come with the option for you to pay a minimum amount of your charge, usually 2% of the balance due. However, the credit card company earns money by charging interest on the balance that you don't pay. So even if you pay credit card payments on time, interest is still accruing on the outstanding balance.

Say you've made a $5,000 purchase on a credit card with an 18% annual interest rate and a 2% minimum monthly payment rate. If you only pay the minimum monthly amount for a year, how much is the remaining balance?

Unpaid balance for month 0:
$$
ub_{0} = b_{0} - p_{0}
$$
- $p_{0}$: your payment in month 0
- $b_{0}$: balance in month 0

At the beginning of month 1, the credit card company will charge you interest on your unpaid balance. So, the balance in month 1:
$$
b_{1} = ub_{0} + \frac{r}{12} \cdot ub_{0}
$$
- $r$: annual interest in decimal

Then, unpaid balance in month 1:
$$
ub_{1} = b_{1} - p_{1}
$$

## Problem 1

Given variables:
1. `balance` - the outstanding balance on the credit card
2. `annualInterestRate` - annual interest rate as a decimal
3. `monthlyPaymentRate` - minimum monthly payment rate as a decimal

Write a program to calculate the credit card balance after one year if a person only pays the minimum monthly payment required by the credit card company each month.

```python
balance = 5000
annual_interest_rate = 0.18
monthly_payment_rate = 0.02

for i in range(12):
	# Payment
	unpaid_balance = balance - balance * monthly_payment_rate
	# Interest
	balance = unpaid_balance + annual_interest_rate / 12 * unpaid_balance

print(f"Remaining balance: {round(balance, 2)}")
```

## Problem 2 & 3

Calculate the minimum **fixed** monthly payment needed in order pay off a credit card balance within 12 months.

1. `balance` - the outstanding balance on the credit card
2. `annualInterestRate` - annual interest rate as a decimal

Balance in this month:
$$
b = b' - p + (b' - p) \cdot r/12
$$
- $b'$: balance in the last month
- $p$: fixed payment

Or:
$$
b =(b' - p) \cdot t
$$
Where $t = 1 + \frac{r}{12}$ 

The upper bound of the payment is when the interest is calculated on the initial balance rather than the balance of each month.
$$
p_{upper} = b_{0} \cdot \left(1 + \frac{r}{12}\right)^{12} \cdot \frac{1}{12}
$$

The lower bound of the payment is when the interest is none.
$$
p_{lower} = \frac{b_{0}}{12}
$$

```python
balance = 4773 # initial balance
annual_interest_rate = 0.2
epsilon = 0.5
t = annual_interest / 12 + 1

high = balance * t ** 12 / 12
low = balance / 12

while True:
	b = balance
	payment = (high + low) / 2
	
	for _ in range(12):
		b = (b - payment) * t

	print(b, payment)

	if abs(b) < epsilon:
		break
	
	if b > 0:
		low = payment
	else:
		high = payment

print("Lowest Payment:", round(payment, 2))
```



