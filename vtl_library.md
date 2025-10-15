# VTL Library
&nbsp;

> [!TIP]
> Additional examples of vtl expressions can be found [here](vtl_examples.md).

&nbsp;

## Time Library
Prefix for methods in this custom class: `library_date`

&nbsp;

### year()
Returns current year (in local timezone) in four-digit (yyyy) format.

#### Example
vtl: `$library_date.year()`

response: "2024"

&nbsp;

### today()
Returns current date (in local timezone) in yyyyMMdd format.

#### Example
vtl: `$library_date.today()`

response: "20240603"

&nbsp;

### now()
Returns current time in GMT in yyyy-MM-dd HH:mm:ss format.

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

### dateAddHours(Object object, Object add)
Adds a specified number of hours (add) to the passed date (object).

#### Example
vtl: $library_date.dateAddHours('2023-05-31 12:34:56', 5)

response: "2023-05-31 17:34:56"
&nbsp;


### dateSubHours(Object object, Object add)
Subtracts the specified number of hours (sub) from the passed date (object).

#### Example
vtl: $library_date.dateSubHours('2023-05-31 12:34:56', 3)

response: "2023-05-31 09:34:56"
&nbsp;

### dateAddMinutes(Object object, Object add)
Adds a specified number of minutes (add) to the passed date (object).

#### Example
vtl: $library_date.dateAddMinutes('2023-05-31 12:34:56', 10)

response: "2023-05-31 12:44:56"
&nbsp;


### dateSubMinutes(Object object, Object sub)
Subtracts the specified number of minutes (sub) from the passed date (object).

#### Example
vtl: $library_date.dateSubHours('2023-05-31 12:34:56', 10)

response: "2023-05-31 12:24:56"
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

### formatDay(Object date)
Returns given yyyyMMdd format date in medium date format for the serbian language and Republika Srbija country.

#### Example
vtl: `$library_date.formatDay('20230531')`

response: "31.05.2023."

&nbsp;


### formatDay(Object date, String requestedLanguage, String requestedCountry)
Returns given yyyyMMdd format date in medium date format for the requested language and requested country.

#### Example
vtl: `$library_date.formatDay('20230531', 'sr', 'RS')`

response: "31.05.2023."

&nbsp;

### formatDate(Object date)
Returns given yyyy-MM-dd HH:mm:ss format date in medium date-time format for the serbian language and Republika Srbija country.

#### Example
vtl: `$library_date.formatDate('2023-05-31 12:34:56')`

response: "31.05.2023. 12:34."

&nbsp;


### formatDate(Object date, String requestedLanguage, String requestedCountry)
Returns given yyyy-MM-dd HH:mm:ss format date in medium date-time format for the requested language and requested country.

#### Example
vtl: `$library_date.formatDate('2023-05-31 12:34:56', 'sr', 'RS')`

response: "31.05.2023. 12:34."

&nbsp;

&nbsp;

### daysBetween(Object day1, Object day2)
Returns number of days between two days.

#### Example
vtl: `$library_date.daysBetween(20250701, 20250901)`

response: "62"

&nbsp;

&nbsp;


## Library

Prefix for methods in this custom class: `library`

&nbsp;

### printObject(Object input)
If object is instance of java Map, it return JsonObject.toString(). If object is java List, it returns JsonArray.toString(). If object is java String, it returns String with escaped values using Json String rules.

#### Example
vtl: `$library.printObject('folder/file')`

response: "folder\\/file"

&nbsp;

### escapeJson(String input)
Returns String with escaped values using Json String rules.

#### Example
vtl: `$library.escapeJson('folder/file')`

response: "folder\\/file"

&nbsp;

### escQuery(Object input)
Returns url encoded value of given object to be used in url query parameters.

#### Example
vtl: `$library.escQuery('folder/file')`

response: "folder%2Ffile"

&nbsp;

### escPath(Object input)
Returns url encoded value of given object to be used in url path parameters.

#### Example
vtl: `$library.escPath('folder/file')`

response: "folder%2ffile"

&nbsp;

### quote(Object input)
If object is instance of String, returns given value between double quotes. Else, returns object.toString

#### Example
vtl: `$library.quote('input')`

response: "\"input\""

&nbsp;

### formatNumber(Object input)
Returns formated decimal number that is the result of division by 100 of given input for the serbian language and Republika Srbija country.

#### Example
vtl: `$library.formatNumber('1234')`

response: "12,34"

&nbsp;

### formatNumber(Object input, String requestedLanguage, String requestedCountry)
Returns formated decimal number that is the result of division by 100 of given input for the requested language and requested country.

#### Example
vtl: `$library.formatNumber('1234','sr','Rs')`

response: "12,34"

&nbsp;

### unescapeJson(String input)
Returns String with any Json literals unescaped.

#### Example
vtl: `$library.unescapeJson('folder\\/file')`

response: "folder/file"

&nbsp;

### escapeXml(String input)
Returns String with escaped values for characters using XML entities.

#### Example
vtl: `$library.escapeXml('folder & file')`

response: "folder \&amp; file"

&nbsp;

### parseJsonToMap(String input)
Returns Map<String, Object> parsed from input string which is json object toString().

#### Example
vtl: `$library.parseJsonToMap('{"key":"value"}')`

response: {key=value}

&nbsp;

&nbsp;


### parseJsonToList(String input)
Returns List parsed from input string which is json object toString().

#### Example
vtl: `$library.parseJsonToList('[{"key":"value"}]')`

response: [{key=value}]

&nbsp;

&nbsp;


### uuid()
Returns random generated UUID

#### Example
vtl: `$library.uuid()`

response: c2660907-b88d-46eb-86a3-8e9f4a4e75f4

&nbsp;

&nbsp;


### counter(String counterName)
Returns next number in counter(sequence) named counterName

#### Example
vtl: `$library.counter('Test1')`

response: 1 
*(every execution increments this result)*
&nbsp;

&nbsp;

### toMap(List<Map<String, Object>> list, String key)
Returns Map<String, Map<String, Object> where elemets of list are returned as Map. Key of map is property sent as parametar key.

#### Example
vtl: 
```
#set($list=[{'name' : 'Name A', 'code' : 'A1'}, {'name' : 'Name B', 'code' : 'B1'}])
#set ($map=$library.toMap($list, 'code'))
$map.get('A1')
```

response: {name=Name A, code=A1}

&nbsp;

&nbsp;

## Text Library

Prefix for methods in this custom class: `library_text`

&nbsp;

### removeHtml(String input)
Returns plain text String with all the html tags removed. 

#### Example
vtl: `$library_text.removeHtml('<p>example</p>')`

response: "example"

&nbsp;

### extractTextHtml(String input)
Return text from html. 

&nbsp;

### extractTitleHtml(String input)
Return title of html page

&nbsp;

### lpad(String input, String padChar, int length)
Left pad
#### Example
vtl: `$library_text.lpad('23','0',15)`

response: "000000000000023"

&nbsp;

### rpad(String input, String padChar, int length)
Right pad
#### Example
vtl: `$library_text.rpad('23','0',15)`

response: "230000000000000"

&nbsp;

### base64Encode(String input)
Return base64 encoded string
#### Example
vtl: `$library_text.base64Encode('Neki tekst')`

response: "TmVraSB0ZWtzdA=="

&nbsp;

### base64Decode(String input)
Return base64 encoded string
#### Example
vtl: `$library_text.base64Decode('TmVraSB0ZWtzdA==')`

response: "Neki tekst"

&nbsp;

### regexExtract(String inputText, String regex)
Extract text from inputText using regular expression

&nbsp;

### convertNumberToText(String amount, String currency, String script, String format, boolean joinWords, String formatHundreds)

Enables conversion of numeric values into text format, adapted to Serbian language (Cyrillic or Latin) and use in contract documentation.
The {convertNumberToText} method accepts:
- amount as a string (e.g. "2000.456")
- currency: "RSD", "EUR" or "USD"
- script: "SR" (Cyrillic) or "SR_LAT" (Latin)
- format:
  * DECIMALNUM: uses the format "и 00/100"
  * DECIMALTEXT: uses the text form of the decimal part, e.g. "и четрдесетшест пара"
    
(Optional)
- joinWords:
  * true -  all words of numbers are joined without spaces
  * false - all words of numbers are separated with spaces
- formatHundreds:
  * SERBIAN_SHORT - where for the value 500 it will print "petsto"
  * SERBIAN_LONG -  where for the value 500 it will print "petstotina"

The result is a string representing the amount in letters, concatenated without spaces (e.g. "Педесетпетхијадачетиристотина динара и шест пара"),
while currency and decimals are always separated by a space.

FLAG:
JOIN_WORDS = true → all words of numbers are joined without spaces.

Format_Hundreds: by default its value is "SERBIAN_LONG", if you do not send a parameter in the method, if you send it you have the option "SERBIAN_LONG (where for the value 500 it will print "petstotina") and "SERBIAN_SHORT"
(where for the value 500 it will print "petsto")

#### Example
vtl: `$library_text.convertNumberToText("2000.456", "RSD", "SR", "DECIMALTEXT")` default

#### Example
With explicit joinWords = true and formatHundreds = "SERBIAN_LONG" parameters
vtl: `$library_text.convertNumberToText("2000.456", "RSD", "SR", "DECIMALTEXT",true, "SERBIAN_LONG")` (true for parameter joinWords)
&nbsp;

response: "Двехиљаде динара и четрдесетшест пара"

&nbsp;

## Math Library

Prefix for methods in this custom class: `library_math`

&nbsp;

### toNumber(Object num)
Converts num to BigDecimal

#### Example
vtl: `${library_math.toNumber('4.5555')}`

response: "4.5555"


### toMoney(Object num)
Converts num to decimal, multiplies it by 100 and returns it as int

#### Example
vtl: `${library_math.toMoney('4.5555')}`

response: "455"

### add(Object ... num)
Returns the sum of the numbers or null if they're invalid 

#### Example
vtl: `$library_math.add('5', 6, 7.5)`

response: "18.5"

&nbsp;

### sub(Object ... num)
Returns the difference of the numbers (subtracted in order) or null if they're invalid 

#### Example
vtl: `$library_math.sub(25, 6)`

response: "19"


vtl: `$library_math.sub(18.5, '10', 3)`

response: "5.5"


&nbsp;

### mul(Object ... num)
Returns the product of the numbers or null if they're invalid 

#### Example
vtl: `$library_math.mul(100000000, 10000000)`

response: "1000000000000000"

&nbsp;

### div(Object num1, Object num2)
Returns the quotient of the numbers or null if they're invalid or if denominator equals zero. If quotient have Non-terminating decimal expansion, it will be ronded to 4 decimals

#### Example
vtl: `$library_math.div(1000000000000000, 10000000)`

response: "100000000"

vtl: `$library_math.div(5,100)`

response: "0.05"   

vtl: `$library_math.div(20,7)`

response: "2.8571"   


### div(Object num1, Object num2, int precision)
Returns the quotient of the numbers or null if they're invalid or if denominator equals zero. If quotient is not whole number, result will be rounded at given precision. Rounding mode is HALF_DOWN

vtl: `$library_math.div(20.0, 7.0, 5)`

response: "2.85714" 

### div(Object num1, Object num2, int precision, String roundingMode)
Returns the quotient of the numbers or null if they're invalid or if denominator equals zero. If quotient is not whole number, result will be rounded at given precision with given rounding mode. Possilbe values for rounding modes are:
- CEILING - Rounding mode to round towards positive infinity.
- DOWN - Rounding mode to round towards zero.
- FLOOR - Rounding mode to round towards negative infinity.
- HALF_DOWN - Rounding mode to round towards "nearest neighbor" unless both neighbors are equidistant, in which case round down.
- HALF_EVEN - Rounding mode to round towards the "nearest neighbor" unless both neighbors are equidistant, in which case, round towards the even neighbor.
- HALF_UP - Rounding mode to round towards "nearest neighbor" unless both neighbors are equidistant, in which case round up.
- UNNECESSARY - Rounding mode to assert that the requested operation has an exact result, hence no rounding is necessary.
- UP - Rounding mode to round away from zero.

See https://docs.oracle.com/javase/8/docs/api/java/math/RoundingMode.html for more info

vtl: `$library_math.div(20.0, 7.0, 5, 'HALF_DOWN')`

response: "2.85714" 



### round(Object num)
Returns the number rounded to the nearest whole Integer or null if it's invalid

#### Example
vtl: `$library_math.round(3.141592653589793238462643383279502884197)`

response: "3"

&nbsp;

### round(Object num, Object precision)
Returns the value rounded to the specified number of decimal places using HALF_EVEN rounding mode or null if it's invalid 

#### Example
vtl: `$library_math.round(3.141592653589793238462643383279502884197, 2)`

response: "3.14"

&nbsp;


### round(Object num, Object precision, String roundingMode)
Returns the value rounded to the specified number of decimal places using provided roundingMode or null if it's invalid using provided roundingMode
See https://docs.oracle.com/javase/8/docs/api/java/math/RoundingMode.html for more info
#### Example
vtl: `${library_math.roundTo(4.5, 2, 'HALF_UP')})`

response: "5"

&nbsp;


### gt(Object o1, Object o2)
Returns true if numeric value of o1 is greater than o2

#### Example
vtl: `$library_math.gt(2, 3)`

response: "false"

&nbsp;

### ge(Object o1, Object o2)
Returns true if numeric value of o1 is greater than or equal to o2

#### Example
vtl: `$library_math.ge(2, 3)`

response: "false"

&nbsp;

### lt(Object o1, Object o2)
Returns true if numeric value of o1 is less than  o2

#### Example
vtl: `$library_math.lt(2, 3)`

response: "true"

### le(Object o1, Object o2)
Returns true if numeric value of o1 is less than or equal to o2

#### Example
vtl: `$library_math.le(2, 3)`

response: "true"

### eq(Object o1, Object o2)
Returns true if numeric value of o1 is equal to o2

#### Example
vtl: `$library_math.eq(2, 3)`

response: "false"

### ne(Object o1, Object o2)
Returns true if numeric value of o1 is not equal to o2

#### Example
vtl: `$library_math.ne(2, 3)`

response: "true"




&nbsp;

&nbsp;

