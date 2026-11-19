# 1_attempt.md — First-draft note and calculations

**Student:** Iyad Rahim

**ERP:** 36103

> Note on the attempt snapshot: this is an attempt before AI

## Planned method

1. Use the Week 2 cleaned file and keep the city groups separate.

2. For every item-city pair, calculate the mean and median of the available prices.

3. Sort each group by date and calculate the percentage change from its first valid price to its last valid price:

   $$
   \frac{\text{last valid price} - \text{first valid price}}{\text{first valid price}}\times 100
   $$

4. For the flagged-value comparison, use Sweetener D in City 1. Compare the corrected value of 157.5 with the original flagged value of 9,999.

5. Do not fill the missing Pulse C, City 2 value with an invented number. For its percentage change, use the first available observation and state that it starts one week later.

## Initial interpretation

The mean and median are close in most groups, which suggests that the centre of these teaching observations is not being pulled far apart by extreme values after cleaning. They are not the same statistic: the mean uses every value and is affected more by extreme observations, while the median is the middle value after sorting.

The first-to-last percentage change describes the endpoints only. It does not show every movement during the weeks in between and should not be described as a steady increase.

## Data note

The Week 2 cleaned file contains 96 rows. One price remains missing for Pulse C in City 2 on 1 January 2026. The two suspicious source values were corrected in Week 2: 1,250 for Staple A, City 2, and 9,999 for Sweetener D, City 1. The original flagged value 9,999 is used only for the sensitivity comparison below.