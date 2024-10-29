**INPUT**

Raw CSV exports from TOMI are saved to /TOMI Extracts/ folder on internal Sharepoint.

PowerBI looks up these files and appends them as part of the **Performance No Fraud** query.

**CALENDAR**

PowerBI then generates a **Calendar** query using the following code, down to a resolution of 15 minutes.

= let StartDate = #datetime(2023, 01, 01, 00, 00, 00), // Earliest date from Performance No Fraud 
EndDate = #datetime(2024, 11, 01, 00, 00, 00), // Latest date from Performance No Fraud 
NumOf15Mins = Duration.TotalDays(EndDate - StartDate) *24 *4, // Calculate number of 15 min intervals across date range 
Generatedate = List.DateTimes(StartDate, NumOf15Mins, #duration(0, 0, 15, 0)), // Generate dates at 15 min intervals 
#"Converted to Table" = Table.FromList(Generatedate, Splitter.SplitByNothing(), null, null, ExtraValues.Error), 
#"Renamed Columns" = Table.RenameColumns(#"Converted to Table",{{"Column1", "DateTime"}})

Additional columns are then added to show just [date], [year], [month], [day], [DayName] & [time].

**HOLIDAYS**
_Bank Holidays_

A separate scrape then occurs to look at https://www.gov.uk/bank-holidays and extract the tables relating to Scotland for Past bank holidays in 2023 and 2024, as well as future bank holidays in 2024, 2025 and 2026. Scotland Bank Holidays were chosen due to the additional bank holiday observed in Scotland, and due to the customer share in Scotland **percentage to be clarified**
This scrape extracts the data as 5 separate tables split by year and temporal position, before being appended into one new query called **Bank Holidays**. The underlying queries are then hidden from the report.

--Get list from Adam of other dates that are likely to be one off holidays

**EXCLUSIONS**

_Other Exclusions_

--Extract a list of P1 and P2 incidents - Most likely to be customer impacting  - **Incidents** Query _to be created_

--Manual cleanse based on visual inspection?

_Uniting the excludes_

The **Calendar** query then has a custom column called [Bank Holiday] that looks at whether the [date] column is found in the **Bank Holidays** query, and if so, returns 1. A new column called [KnownRepeatables] is added to the **Calendar** query which will return "Yes" if the [BankHolidays] columnn, _or any of the other variables that will be later added_, are above 1. 
The **Calendar** query then has a custom column called [Incidents] that looks at whether the [date] column is found in the **Incidents** query, and if so, returns 1. A new column called [Exclude] is added to the **Calendar** query which will return "Yes" if the [Incidents] columnn, _or any of the other variables that will be later added_, are above 

**EXPORT**

Finally, the **Performance No Fraud** query also has a column called [DS] added, which looks up whether the [Exclude] variable is set to "Yes" in the corresponding 15 minute interval within the **Calendar** query. If this is found, then the [DS] column returns _**blank()**_, otherwise it returns the value of [Calls Offered]. 

A table from the **Performance No Fraud** query can then be created with [DateTime] and [DS]. This is then ready to be exported as a CSV and imported into the Python script for Forecasting - this is the Input data.

A separate table from the **Calendar** query can also be created, with [DateTime] showing only dates where [KnownVariables] is set to "Yes". This can also be exported to CSV and imported into the Python script - this is the Holidays data.

**ANALYSIS**

The PowerBI report will also allow for basic analysis of the underlying data going in. A chart showing both the raw imported data charting calls offered vs datetime
![image](https://github.com/user-attachments/assets/27688782-fbd8-45d0-9daf-604f0fa9f980)
