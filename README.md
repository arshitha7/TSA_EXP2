# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
# Name : ARSHITHA MS
# Reg no : 212223240015
## Date: 28.04.2026

### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
1.Import necessary libraries (NumPy, Matplotlib)
2.Load the dataset
3.Calculate the linear trend values using least square method
4.Calculate the polynomial trend values using least square method
5.End the program

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data=pd.read_csv('customer.csv')

data.head()

income = data['Income'].tolist()
idd = data['id'].tolist()
```
A - LINEAR TREND ESTIMATION
```
X = [i - income[len(income) // 2] for i in income]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, idd)]

n = len(income)
b = (n * sum(xy) - sum(idd) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(idd) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]
```
B- POLYNOMIAL TREND ESTIMATION
```
x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, idd)]

coeff = [[len(X), sum(X), sum(x2)],
         [sum(X), sum(x2), sum(x3)],
         [sum(x2), sum(x3), sum(x4)]]

Y = [sum(idd), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)

solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution
poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]
```
PLOT
```
print(f"Linear Trend: y={a:.2f} + {b:.2f}x")
print(f"\nPolynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")

plt.figure(figsize=(8,5))
plt.plot(data['Income'], color='blue', marker='o', label='Volume')
plt.plot(data['Linear Trend'], color='black', linestyle='--', label='Linear Trend')
plt.title("Silver Data Price - Linear Trend Estimation")
plt.xlabel("EmployeeID")
plt.ylabel("Income")
plt.legend()
plt.grid(True)
plt.show()

plt.figure(figsize=(8,5))
plt.plot(data['Income'], color='blue', label='Income')
plt.plot(data['Polynomial Trend'], color='red', linestyle='--',label='Polynomial Trend')
plt.title("Salary Data - Polynomial Trend Estimation")
plt.xlabel("EmployeeID")
plt.ylabel("Income")
plt.legend()
plt.grid(True)
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="695" height="468" alt="download" src="https://github.com/user-attachments/assets/330ff127-c1ed-4a8b-bf7f-ac6488b0b775" />

B- POLYNOMIAL TREND ESTIMATION
<img width="695" height="468" alt="download" src="https://github.com/user-attachments/assets/fb0d3b9a-c747-4a3b-a82c-4e935571c307" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
