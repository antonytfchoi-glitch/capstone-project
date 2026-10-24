# Antony Choi capstone-project in Real Estate
Problem Statement

HDB resale prices vary widely across towns, flat types and lease ages. Buyers, sellers and policymakers find it hard to judge fair value and affordability, and to see how location and lease decay affect prices. This analysis uses HDB resale transactions to identify what drives resale prices and how the market has changed over time. The aim is to support better valuation, affordability assessment and housing planning.

<img width="364" height="83" alt="image" src="https://github.com/user-attachments/assets/2c0cd451-c4b6-44af-ba0b-6a33cf6fc68a" />

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

Outliers
By the 1.5×IQR rule within each flat type, 12,587 price outliers (about 2%) are flagged, mostly 4 ROOM (5,774) and 5 ROOM (4,358).
The high end is genuine: the largest price-per-sqm values are 4 ROOM flats in Central Area at around $15,000/sqm in 2022 to 2023.
The 199 prices under $60,000 are almost all 1 ROOM flats (190) from the early 2000s. They are real, not errors.
Treatment: do not delete these. Use log(price), analyse by flat type and town, and use robust statistics such as the median.

Formatting and type issues
month is a text string, so convert it to a date and derive year and month.
block is text. 18% of values contain letters (for example “104A”), so do not convert it to a number.
street_name uses standard abbreviations (AVE, ST, RD, NTH, CTRL, BT). They are consistent within the data, but expect to adjust them if you geocode.
Stored prices are all positive; 137 prices are not whole dollars, which is fine.

Data dictionary vs. actual data
The dictionary lists street_lat, street_lon, town_lat and town_lon, but none of these columns exist in the four files. Any map or distance analysis needs geocoding or an external lookup.
The dictionary gives the unit of remaining_lease as years, but the column is actually an integer or text depending on the file (issue 2).
The dictionary describes one table, but the data comes as four files with different columns and date definitions.

Limitations in report
Prices are nominal, not inflation-adjusted. The yearly average rises from about $258K in 2000 to $572K in 2023, so adjust before comparing across years.
Coverage ends in January 2024, and 2024 has only 411 rows, so exclude it from annual comparisons. The zip is dated 2026, so the data is not current.
There is no unit-level identifier, so repeat sales of the same flat cannot be tracked.
Yearly volume dips in 2013 to 2014 (about 16,000 transactions vs. 23,000 in 2012). Treat this as a real market change, not missing data. Cooling measures are a likely cause, but the data cannot confirm it.
Early-year transaction counts vary by town because new towns such as Punggol (first sales in 2005) were still being built. Account for this in town-level trends.

Usage Example (Python & Pandas)
Load: read and combine all four CSVs in the data folder.
Prepare: convert month to a date, then add year, price_per_sqm and remaining_lease_years. The last one is derived for every row, because the files before 2015 have no remaining lease column.
Quick checks: drop the duplicate rows, then exclude terrace houses and the partial 2024 data. That leaves 626,673 rows, and the summary statistics are printed.
First analyses: median price by year, price by flat type, and the top 10 towns by price per sqm in 2023.
Chart: median price over time for each flat type.

<img width="1350" height="750" alt="image" src="https://github.com/user-attachments/assets/fa90b08e-4363-456d-b0fc-c29be9628774" />

<img width="1350" height="750" alt="image" src="https://github.com/user-attachments/assets/9284604e-69e8-4d8b-9b98-
db0f63622232" />

<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/b1fea87f-a4be-444a-b702-e61c70a4137a" />

<img width="1350" height="750" alt="image" src="https://github.com/user-attachments/assets/1b755c87-e06f-46b8-a575-e22c8ca5ac1a" />

<img width="1350" height="750" alt="image" src="https://github.com/user-attachments/assets/af5f1485-fd3f-4e91-8c00-b39217e6f82b" />





