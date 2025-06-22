# Charity-Pledge-Report-Analysis-using-Alteryx
Charity Pledge Report Analysis
This is a data analysis project focused on understanding charitable giving patterns through pledge data. While this analysis could have been performed using tools like Excel or Python, I chose to use Alteryx due to its intuitive, no-code/low-code interface and powerful data preparation capabilities.
Alteryx made the entire data cleaning, transformation, and analysis process more efficient and streamlined. I thoroughly enjoyed working on this project and leveraging Alteryx to extract meaningful insights from raw data.

Problem Statement:
As part of a non-profit organization focused on facilitating charitable giving, we received a System Pledge Report detailing pledges made to various charities. However, this report lacked contextual information about the charities themselves.
To gain actionable insights, we were tasked with integrating the pledge data with a master Charity Information dataset. The objective was to identify:
1.	The charity category with the highest total pledge amount.
2.	The charity that received the highest number of individual credit card donations.
3.	The charity with the highest total pledge amount in the state of New York (employee state) under the "Public" category.

Data Preparation and Cleaning
1. System Pledge Report
•	Input & Connection: Imported into Alteryx and connected using the Input Data tool.
•	Data Cleansing:
o	Used the Data Cleansing Tool to assess column quality using Red, Yellow, and Green indicators.
o	Applied the Filter Tool to trim extra spaces, especially in the “Market” column.
o	Standardized casing in the "Employee Work State" column to ensure consistency (e.g., NY vs ny).
•	Select Tool:
o	Validated and adjusted column data types as appropriate.
o	Identified incorrect date formatting and corrected it using the DateTime Tool. The new column was renamed, and the old one was removed.
•	Formula Tool:
o	Created a conditional formula to handle missing values in the "Gift Type" column. Any null values were interpreted as "Online" donations using:
if [Gift Type] = Null then "Online" else [Gift Type] endif
2. Charity Information
•	Address Splitting:
o	The full address field was separated using the Text to Columns Tool, where "+" was the delimiter.
•	Select Tool:
o	Data types were reviewed and corrected as necessary.
•	Multi-Row Formula Tool:
o	Used to populate missing values in the "Charity Country" and "Charity State" columns with the last known value from the preceding row. This was achieved using:
if IsNull([Charity State]) then [Row-1:Charity State] else [Charity State] endif
•	Data Cleaning:
o	Standardized address text using Title Case formatting.
•	Unique Tool:
o	Ensured that each Charity EIN (Employer Identification Number) was unique before merging datasets.

Data Integration and Analysis
•	Union Tool:
o	Merged the System Pledge Report and Charity Information datasets using the EIN as the common key.
•	Summary Tool:
o	Aggregated pledge amounts and counts to support the analysis for all three questions.
•	Filter Tool:
o	Applied filters to narrow down data for specific conditions:
	For Question 3, filtered "Employee Work State" to only include “NY”.
	Used additional filters and sorting tools to identify top results.

Findings (Summary Tool Outputs)
1.	Charity Category with the Largest Total Pledge Amount:
Determined by summing pledge amounts grouped by charity category and sorting in descending order.
2.	Charity with the Highest Number of Credit Card Individual Donations:
Identified by counting individual donations where the gift type was “Credit Card”, then grouped by charity and sorted by count.
3.	Charity with Highest Total Pledge in NY (Public Category):
Filtered for "Employee Work State = NY" and "Charity Category = Public", then grouped by charity and sorted by total pledge amount.
