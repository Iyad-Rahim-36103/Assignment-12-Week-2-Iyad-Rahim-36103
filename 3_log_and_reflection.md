# 3_log_reflection.md — Log, Audit, and Reflection

## 1. AI-Use Log

AI assistance was used to help draft an interpretation of the descriptive statistics and to challenge the claims in that interpretation. The calculations were independently recomputed in the notebook using the Week 2 cleaned file. Claims about the mean being always typical, the use of the original 9,999 value, and conclusions about actual PBS prices were rejected after checking the data and its labels.

The attempt snapshot in `1_attempt.md` is explicitly identified as attempt before AI. No personal or confidential data was entered into an AI tool.

## 2. AI-Generated Interpretation Audit

### AI-generated interpretation to audit

1. The mean is always the best measure of a typical price because it uses every observation.

2. The medians and means are close in the cleaned item-city groups, so the typical values are broadly similar in this dataset.

3. Sweetener D in City 1 increased by 19.80% from its first valid observation to its last valid observation.

4. Pulse C in City 2 increased by 2.40%, although its first available value is from 8 January because the 1 January price is missing.

5. The 9,999 source value should be used because it is the number originally recorded.

6. These results show that actual PBS prices rose across Pakistan during this period.

### Audit table

| Claim | Colour | Check performed | Verdict | 
| ----- | ----- | ----- | ----- | 
| 1\. Mean is always the best measure of typical price. | Red | Compared mean and median; tested the effect of the 9,999 source value. | Reject. The mean is sensitive to extreme values and is not always the best description of a typical observation. | 
| 2\. Means and medians are close in cleaned groups. | Green | Recomputed both statistics for all eight item-city groups. | Keep, with the qualification that this is the cleaned illustrative dataset. | 
| 3\. Sweetener D, City 1 changed by 19.80%. | Green | Recomputed $(178.5 - 149) / 149 \times 100$. | Keep. | 
| 4\. Pulse C, City 2 changed by 2.40% from its first available value. | Green | Recomputed $(213.5 - 208.5) / 208.5 \times 100$ and checked the missing first-week record. | Keep, and state the dates used. | 
| 5\. The original 9,999 should be used because it was recorded. | Red | Compared it with the paired city value, neighbouring weeks and the Week 2 correction note. | Reject. A recorded value is not automatically valid; 9,999 was flagged and corrected to 157.5 in Week 2. | 
| 6\. Results show actual PBS prices rose across Pakistan. | Red | Checked the data label and scope. | Reject. The file is illustrative teaching data, not actual PBS observations, and covers only two teaching cities. | 

### Recalculation: flagged-value effect

For Sweetener D, City 1, using the Week 2 corrected value of 157.5 gives a mean of **163.75** and a median of **163.75**. Replacing that one observation with the original flagged value of 9,999 gives a mean of **983.88** and a median of **165.75**. The mean changes dramatically, while the median moves only slightly. This is why the original extreme value should not be accepted without verification.

## 3. Confused Classmate Dialogue

**Student:** The mean is the total of all the prices divided by how many prices there are. It uses every observation.

**Classmate:** But why does that make it the typical price?

**Student:** It does not automatically make it typical. If one value is extremely high, it can pull the mean upward even when most prices are close together.

**Classmate:** But why would one value matter so much if there are eleven other prices?

**Student:** Because the mean includes the size of every value. In the Sweetener D, City 1 example, replacing 157.5 with 9,999 changes the mean from 163.75 to 983.88.

**Classmate:** But why doesn't the median change by the same amount?

**Student:** The median depends on the middle position after sorting, not on how large the highest value is. Here it changes from 163.75 to 165.75, which is much smaller.

**Classmate:** So should we always use the median then?

**Student:** Not always. The mean is useful when values are reasonably balanced and we want every observation to affect the result. The median is useful when the data are skewed or contain extreme values. Reporting both helps us see whether the centre is being pulled.

**Classmate:** So the mean isn't wrong, but calling it typical without checking can be wrong?

**Student:** Exactly. We need to look at the data and the context before choosing which average best describes them.

**End of excerpt:** The repeated “but why” questions stop once the distinction between the mean's sensitivity to magnitude and the median's reliance on the middle position is explained.

## 4. Referee's Note: What do the averages actually tell us?

**O:** The Week 2 cleaned teaching file contains 96 rows covering four items, two cities and twelve weekly dates.

**O:** The file is illustrative teaching data and is not actual PBS observations.

**O:** The calculations below keep City 1 and City 2 separate rather than treating the two markets as one series.

**O:** Across the item-city groups, mean prices range from about PKR 108.17 for Staple A in City 1 to PKR 327.83 for Oil B in City 2.

**O:** The medians are close to the means in these cleaned groups, with the largest visible distinction appearing where a flagged source value is considered.

**O:** From the first valid observation to the last valid observation, the percentage changes range from 2.40% for Pulse C in City 2 to 19.80% for Sweetener D in City 1.

**O:** Pulse C in City 2 has a missing value on 1 January, so its first available observation is 8 January rather than 1 January.

**O:** In the Sweetener D, City 1 series, the Week 2 cleaned value for 22 January is 157.5, while the source value recorded before correction was 9,999.

**E:** The closeness of the mean and median in the cleaned series may indicate that the corrected data do not contain a remaining extreme value that strongly pulls the mean away from the centre.

**E:** The higher percentage changes for Sweetener D may indicate a stronger increase over the period in this illustrative dataset, but the endpoint calculation does not prove that prices rose every week.

**E:** The city differences may reflect different local price levels, but this dataset alone cannot explain why the cities differ.

**C:** The data support saying that the recorded last price is higher than the first valid price in each item-city group shown.

**C:** The data do not support claiming that the same percentage change occurred in every week or that the pattern represents Pakistan's actual market.

**C:** The mean should not automatically be called the typical price without checking the distribution and possible outliers.

**C:** The median is less affected by a single extreme value, while the mean can be pulled sharply by it, so both should be reported when data quality is uncertain.

### Descriptive statistics by item and city

| Item | City | Mean (PKR) | Median (PKR) | First-to-last change | 
| ----- | ----- | ----- | ----- | ----- | 
| Oil B | City 1 | 321.83 | 321.00 | 15.44% | 
| Oil B | City 2 | 327.83 | 327.00 | 15.13% | 
| Pulse C | City 1 | 202.92 | 202.50 | 3.75% | 
| Pulse C | City 2 | 209.18 | 208.50 | 2.40% | 
| Staple A | City 1 | 108.17 | 107.75 | 13.37% | 
| Staple A | City 2 | 114.17 | 113.75 | 12.62% | 
| Sweetener D | City 1 | 163.75 | 163.75 | 19.80% | 
| Sweetener D | City 2 | 169.75 | 169.75 | 19.03% | 

### 

## 5. Reflection

My first draft could have made the mean sound like the typical price in every situation. That would have gone further than the data allow. The flagged-value comparison shows why: using 9,999 instead of the corrected 157.5 changes the mean from 163.75 to 983.88, while the median changes from 163.75 to 165.75.

I also had to be careful with the percentage change for Pulse C in City 2. The first date has a missing price, so the calculation starts with the first available value on 8 January. Finally, the results describe an illustrative teaching dataset only. They cannot be presented as actual PBS findings.