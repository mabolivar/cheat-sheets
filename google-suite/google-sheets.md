
### Format pivot table output as value (%)

To format the table output as `value (%)`, it is necessary to 
1. Create a calculated field
2. Count/sum the desired value 
3. Create a separate pivot table using the same filters in order to get to total values for the desired variable. 
4. Use the `GETPIVOTDATA(.)` to get the `Grand total` value from the second table.
5. Format the data using the `TEXT(.)` function.

```
=CONCATENATE(
	COUNTA(id), 
	" (",
	TEXT(
		COUNTA(id)/GETPIVOTDATA(Metrics!$F$1,Metrics!$F$1),
		"0%"
	),
	")"
)
```

## Sum only working days

EXAMPLE

```
WORKDAY("20/07/1969"; 4; A1:A10)
```

ABOUT

Calculates the date after a number of working days from a specified start date.

---

start_date

The date from which to begin counting.

num_days

The number of working days to advance from start_date. If negative, counts backwards.

holidays - [optional]

A range or array constant containing the dates to consider holidays.

