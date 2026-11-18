# PowerBi-Basic-to-Advance
A repo for PowerBI Tutorials, covering from basic to advance of it. 


# Time Intelligence
> It's the DAX Function that calculate or cumulate data over period. 
The main two constrain for Time Intelligence is:
- The Table needs to declaire as Date Table.
- Then using Table's Date column we can use time intelligence functionality.

## TOTALYTD()
Gives the total aggregrated value from the start date to current date as per current filter context. 
```
Sales YTD = TOTALYTD([Total Sale], Calender[date])
```
TOTALYTD([Total Sale], Calender[date]) is actuall a short-cut of CALCULATE([Total Sale], DATESYTD(Calender[Date]))

**DATESYTD()** gives all the dates till last date in current filter context. 

## SAMEPERIODLASTYEAR()
This dax function takes the current date filter, and based on the context goes exactly one year back.
```
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR(Calender[date]))
```
SAMEPERIODLASTYEAR(Calender[date]) is equivalent as DATEADD(Calender[date], -1, YEAR)
DATEADD() gives the dates of 1 year back. In the same way it works for MONTH, QUATER, DAYS. If we want 2 year back data then we can pass -2. 

## YoY % 
Used to describe Growth % over the time. 

```
YoY % = 
var _cur = [Total Sales]
var _ly = [Sales LY]
RETURN
  DIVIDE(_cur - _ly, _ly)
```

*EXERCISE*
Calculate Sales YTD LY, MoM % 


## Rolling AVG
MoM % Fluctuates a lot. For better storytelling we use the Rolling AVG of 3 or 5 months.
```
Sales 3M Rolling AVG =
var _end = MAX(Calender[Date])
var _dates = DATESINPERIOD(Calender[Date], -3, MONTHS)
RETURN
  CALCULATE(AVERAGEX(VALUES(Calender[Year-Month]), [Total Sales]), _dates)
```
