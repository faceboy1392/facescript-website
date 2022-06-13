# Aspen Built-in Functions & Standard Library Stuff

## Native functions
---
```rb
# type conversion
echo str(5) # '5'
echo str(true) # 'true'

echo num('20') # 20
echo num('2.1') # 2.1

# int() rounds to the nearest integer
echo int(5.2) # 5
echo int('19.4') # 19

# since there isn't any type distinction between ints or floats, there is no float() function


echo type('hello') # 'string'
# type() can return 'number', 'string', 'boolean', 'null' 'nan', 'function', 'list', 'table', 'class', or 'class instance'

# Some math functions may also be implemented natively, not sure
```

> `parse_num()` and `parse_int()` will also exist, I don't know the specifics of what I want them to be capable of but the difference between them and the num() and int() functions is that the num() and int() functions are for converting between types mostly, while these two are for parsing more advanced strings into numbers. For example, `parse_num('2489E+2')` will return whatever the heck that number is.

> `eval` may be tricky, especially defining the scope of things properly. Hopefully I can implement it in such a way that it can be used relatively safely. Being able to execute without allowing native functions, setting an execution time limit, passing specific functions or arguments into it, etc.a

## Time
---
```rb
# Ways of using the Time class

Time.now()
Time.today() # 1:00:00 AM, beginning of the current day
Time.yesterday()
Time.tomorrow()

Time.nearestMinute() # Rounds to the nearest minute
Time.nearestHour() # Rounds to the nearest hour

now = Time.now()

echo now # calls now.to_string()
# 13/06/2022 10:41:32 EST
# DD/MM/YYYY hh:mm:ss <timezone>

now.day
now.month
now.year
now.hours # 24 hour format
now.minutes
now.seconds
now.milliseconds
now.week # week of the year out of 52
now.weekday # what weekday it is, either 'monday, 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', or 'sunday'
now.unix # unix timestamp

# these just change the `hours` property to be out of 12 or 24. Converting back to 24 will internally use the `morning` or `afternoon` properties to figure things out.
now.as_12_hour_format()
now.as_24_hour_format()
now.to_iso_string()
# '2019-01-25T02:00:00.000Z'
# ISO 8601 string thing, also ignore the fact that it is using a completely different time, idk how to convert to ISO 8601

# bools
now.is_morning
now.is_afternoon
now.is_leap_year


# time math
now = now.add({ hours: 5 })
now = now.subtract({ hours: 3, minutes: 30 })

# something kinda similar to that dayjs thing
echo now.format('DD/MM/YYY hh:mm:ss')
```