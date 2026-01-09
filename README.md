import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("Sample - Superstore.csv", encoding="latin1")

df["Order Date"] = pd.to_datetime(df["Order Date"])

df["MonthYear"] = df["Order Date"].dt.to_period("M")

monthly = df.groupby("MonthYear")["Sales"].sum().reset_index()

monthly["MonthYear"] = monthly["MonthYear"].astype(str)

best = monthly.loc[monthly["Sales"].idxmax()]

worst = monthly.loc[monthly["Sales"].idxmin()]

print("Monthly Sales")
print(monthly)

print("Best Month:", best["MonthYear"], best["Sales"])

print("Worst Month:", worst["MonthYear"], worst["Sales"])

plt.figure(figsize=(8,4))

plt.plot(monthly["MonthYear"], monthly["Sales"], marker="o")

plt.title("Monthly Sales Trend")

plt.xlabel("MonthYear")

plt.ylabel("Total Sales")

plt.xticks(rotation=45)

plt.tight_layout()

plt.show()

total_sales = monthly["Sales"].sum()

average_sales = monthly["Sales"].mean()

print("Total Sales:", total_sales)

print("Average Monthly Sales:", average_sales)

first = monthly.iloc[0]

last = monthly.iloc[-1]

print("First Month", first["MonthYear"], "Sales", first["Sales"])

print("Last Month", last["MonthYear"], "Sales", last["Sales"])
