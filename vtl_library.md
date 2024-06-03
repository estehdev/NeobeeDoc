# VTL Library
&nbsp;

&nbsp;

## Time Library
Prefix for methods in this custom class: `library_date`

&nbsp;

### year()
Returns current year in four-digit format (yyyy).

#### Example
vtl: `$library_date.year()`

response: 2024

&nbsp;

### today()
Returns current date in format: yyyyMMdd.

#### Example
vtl: `$library_date.today()`

response: 20240603

&nbsp;

### now()
Returns current date and time in format: yyyy-MM-dd HH:mm:ss.

#### Example
vtl: `$library_date.now()`

response: 2024-06-03 13:09:13

&nbsp;

### dateSubDay()
Returns date and time in format: yyyy-MM-dd HH:mm:ss that is the result of subtracting given number of days from given date.

#### Example
vtl: `$library_date.dateSubDay('2023-05-31 12:34:56', 2)`

response: 2023-05-29 12:34:56

&nbsp;

### dateAddDay()
Returns date and time in format: yyyy-MM-dd HH:mm:ss that is the result of adding given number of days to given date.

#### Example
vtl: `$library_date.dateAddDay('2023-05-31 12:34:56', 2)`

response: 2023-06-02 12:34:56

&nbsp;

### daySub()
Returns date in format: yyyyMMdd that is the result of subtracting given number of days from given date.

#### Example
vtl: `$library_date.daySub('20230531', 2)`

response: 20230529

&nbsp;

### dayAdd()
Returns date in format: yyyyMMdd that is the result of adding given number of days to given date.

#### Example
vtl: `$library_date.dayAdd('20230531', 2)`

response: 20230602

&nbsp;




&nbsp;

&nbsp;

## Library

Prefix for methods in this custom class: `library`

### printObject()



-----
> [!TIP]
> Additional examples of vtl expressions can be found [here](vtl_examples.md) 
