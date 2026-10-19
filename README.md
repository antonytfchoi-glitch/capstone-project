# Antony Choi capstone-project in Real Estate
Problem Statement

HDB resale prices vary widely across towns, flat types and lease ages. Buyers, sellers and policymakers find it hard to judge fair value and affordability, and to see how location and lease decay affect prices. This analysis uses HDB resale transactions to identify what drives resale prices and how the market has changed over time. The aim is to support better valuation, affordability assessment and housing planning.

Research Objectives

1.Quantify how flat type, floor area, storey range and flat model affect resale price.
2.Measure how remaining lease and lease commencement year affect price, to estimate lease depreciation.
3.Compare resale prices and price per square metre across towns to identify high-value and affordable areas.
4.Analyse long-term price trends and seasonality in transaction volume from 2000 to the latest data.
5.Build a predictive model of resale price and identify which features contribute most to it.

<img width="271" height="500" alt="image" src="https://github.com/user-attachments/assets/8c5b170d-d941-4caa-ae9d-621f8020a15e" />

<img width="397" height="143" alt="image" src="https://github.com/user-attachments/assets/a3145ac3-fe5d-4c31-95b6-e4c98f2d48f5" />

Duplicates
There are 1,066 exact duplicate rows (0.17%), spread across the 2000 to 2012 file (513), 2017 onwards (349), 2012 to 2014 (248) and 2015 to 2016 (24).
Another 68 groups are identical except for remaining_lease, which differs by one month. Those look like separate sales.
There is no transaction or unit ID, so identical rows may be genuine separate sales. Two identical flats in one block can sell for the same price in the same month.
Treatment: flag the duplicates (is_dup) and run the main analysis both with and without them. Do not drop them silently.
