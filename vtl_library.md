# VTL Library
&nbsp;

&nbsp;

## Time Library
Prefix for methods in this custom class: `library_date`

&nbsp;

### year()
Returns current year in four-digit (yyyy) format.

#### Example
vtl: `$library_date.year()`

response: "2024"

&nbsp;

### today()
Returns current date in yyyyMMdd format.

#### Example
vtl: `$library_date.today()`

response: "20240603"

&nbsp;

### now()
Returns current date in yyyy-MM-dd HH:mm:ss format.

#### Example
vtl: `$library_date.now()`

response: "2024-06-03 13:09:13"

&nbsp;

### dateSubDay(Object date, Object daysToSubtract)
Returns date in yyyy-MM-dd HH:mm:ss format that is the result of subtracting given number of days from given date.

#### Example
vtl: `$library_date.dateSubDay('2023-05-31 12:34:56', 2)`

response: "2023-05-29 12:34:56"

&nbsp;

### dateAddDay(Object date, Object daysToAdd)
Returns date in yyyy-MM-dd HH:mm:ss format that is the result of adding given number of days to given date.

#### Example
vtl: `$library_date.dateAddDay('2023-05-31 12:34:56', 2)`

response: "2023-06-02 12:34:56"

&nbsp;

### daySub(Object date, Object daysToSubtract)
Returns date in yyyyMMdd format that is the result of subtracting given number of days from given date.

#### Example
vtl: `$library_date.daySub('20230531', 2)`

response: "20230529"

&nbsp;

### dayAdd(Object date, Object daysToAdd)
Returns date in yyyyMMdd format that is the result of adding given number of days to given date.

#### Example
vtl: `$library_date.dayAdd('20230531', 2)`

response: "20230602"

&nbsp;

### convertToTimeZone(Object date, String requestedtimeZone)
Returns date in yyyy-MM-dd HH:mm:ss format for the given date and time in UTC and given time zone.

#### Example
vtl: `$library_date.convertToTimeZone('2023-05-31 12:34:56','Europe/Belgrade')`

response: "2023-05-31 14:34:56"

&nbsp;

### format(Object date, String requestedFormat)
Returns date in requested format for the given date in yyyy-MM-dd HH:mm:ss format.

#### Example
vtl: `$library_date.format('2023-05-31 12:34:56','yyMMdd')`

response: "230531"

&nbsp;




&nbsp;

&nbsp;

## Library

Prefix for methods in this custom class: `library`

### printObject()



-----
> [!TIP]
> Additional examples of vtl expressions can be found [here](vtl_examples.md) 
