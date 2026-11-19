# Assignment 13: Two Averages, One Argument

This notebook uses the Week 2 cleaned teaching file. The data are illustrative, not actual PBS observations. It calculates mean, median and first-to-last percentage change by item and city, then checks the effect of the flagged Sweetener D value.

```
import pandas as pd
import numpy as np

df = pd.read_csv("week2_cleaned_prices.csv")
df["date"] = pd.to_datetime(df["date"])
df["price"] = pd.to_numeric(df["price"], errors="coerce")

print("Rows:", len(df))
print("Missing prices:", df["price"].isna().sum())
print("Items:", sorted(df["item"].dropna().unique()))
print("Cities:", sorted(df["city"].dropna().unique()))

```

## Mean, median and first-to-last percentage change

```
rows = []
for (item, city), group in df.groupby(["item", "city"]):
    group = group.sort_values("date")
    valid = group.dropna(subset=["price"])
    first = valid.iloc[0]
    last = valid.iloc[-1]
    change = (last["price"] - first["price"]) / first["price"] * 100
    rows.append({
        "item": item,
        "city": city,
        "valid_observations": len(valid),
        "mean": valid["price"].mean(),
        "median": valid["price"].median(),
        "first_valid_date": first["date"].date(),
        "first_valid_price": first["price"],
        "last_valid_date": last["date"].date(),
        "last_valid_price": last["price"],
        "first_to_last_change_pct": change
    })

summary = pd.DataFrame(rows).sort_values(["item", "city"])
summary.round(2)

```

The percentage change uses the first and last **valid** observations in each item-city group. Pulse C in City 2 has no value on 1 January, so its first valid observation is 8 January. The percentage change is therefore based on 8 January to 19 March.

## Pooled item averages across the two cities (additional view)

```
pooled = df.groupby("item")["price"].agg(
    valid_observations="count",
    mean="mean",
    median="median"
).reset_index()
pooled.round(2)

```

## Sensitivity check: flagged value in Sweetener D, City 1

```
flag_group = df[(df["item"] == "Sweetener D") & (df["city"] == "City 1")].copy()
corrected = flag_group["price"].dropna()

# The Week 2 cleaning record shows the original source value as 9,999
# and the corrected working value as 157.5 for 22 January 2026.
flag_index = flag_group.index[
    flag_group["price_original"].astype(str).str.replace(",", "", regex=False).eq("9999")
][0]

with_original_flag = corrected.copy()
with_original_flag.loc[flag_index] = 9999.0

comparison = pd.DataFrame([
    {"version": "Week 2 corrected value", "mean": corrected.mean(), "median": corrected.median()},
    {"version": "Original 9,999 value used", "mean": with_original_flag.mean(), "median": with_original_flag.median()}
])
comparison.round(2)

```

The extreme source value greatly increases the mean, but has a much smaller effect on the median. This is evidence that the mean is not automatically the best measure of a typical price when an extreme value may be present. The flagged source value should be checked against the surrounding observations and the Week 2 cleaning decision, not accepted only because it appears in the raw file.