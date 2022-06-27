# Aspen Built-in Functions & Standard Library Stuff
> NOTE: very very very work in progress, a lot of things will be missing

## Native functions, built into the compiler
---
```rb
# type conversion
echo str(5) # '5'
echo str(true) # 'true'

echo num('20') # 20
echo num('2.1') # 2.1

# int() rounds to the nearest integer if it has decimals
echo int(5.2) # 5
echo int('19.4') # 19

# since there isn't any type distinction between ints or floats, there is no float() function. All numbers are just double precision floating point numbers behind the scenes

echo type('hello') # 'string'
# type() can return 'number', 'string', 'boolean', 'null' 'nan', 'function', 'list', 'table', 'class', or 'class instance'

# Some math functions may also be implemented natively, not sure
```

> `parse_num()` and `parse_int()` will also exist, I don't know the specifics of what I want them to be capable of but the difference between them and the num() and int() functions is that the num() and int() functions are for converting between types mostly, while these two are for parsing more advanced strings into numbers. For example, `parse_num('2489E+2')` will return whatever the heck that number is.

> `eval()` may be tricky, especially defining the scope of things properly. Hopefully I can implement it in such a way that it can be used relatively safely. Being able to execute without allowing native functions, setting an execution time limit, passing specific functions or arguments into it, etc.

## Methods on primitive values
---
```rb
# btw everything will have a .to_str() method 

my_bool = true
my_number = 123.456
my_string = 'hello, world?'

my_bool.to_num() # 1 or 0

my_number.to_fixed(1)

my_string[2]
my_string[-4]

my_string.uppercase()
my_string.lowercase()
my_string.capitalize()

my_string.split(' ')
my_string.match(/mayonnaise/)

my_string.pad_start(20, ' ') # if the string is shorter than the specified length, it adds the second argument to the beginning of the string until it reaches the desired length
my_string.pad_end(30, '.')

# these also would support regex
my_string.replace('hello', 'goodbye')
my_string.replace_all('l', '1')

my_string.starts_with('hello')
my_string.ends_width('world?')

# like javascript trim but should also accept an argument for what character it should try to trim, defaults to trimming whitespace
my_string.trim()
my_string.trim_start()
my_string.trim_end()

# NOTE: also need fancy functions for things like unicode codes and weird things with like modifier characters and whatever

# strings should also have all the same functions as arrays (except flat, and also divide should return a string array, not an array of subarrays)
```

## List and Table methods
---
### List
```rb
users = ['jon', 'eric', 'katrina', 'sam']

users[2] # 'katrina'
# accepts negative index
users[-1] # 'sam'

users.add('bob') # adds item to the end of the list
users.push('Xx_HackerBoyAnonymous1239_xX') # pushes it to the front of the list
users.remove('eric') # removes any matching items
users.pop() # removes and returns the last item
users.pop_first() # .pop() but removes and returns the item at the beginning of the list
users.size # length
users.first # first item in the list
users.last # last item in the list
users.last_index # size - 1
users.reverse
users.concat(['batman', 'lava boy'])
users.index_of('katrina') # returns the index of the first item to have a matching value
users.fill('bruh') # just replaces all items with that
users.fill('mr electric', 10) # fills the first 10 items of the list with that value, grows list to 10 if its too small
users.has('mr electric') # if the list includes that value
users.flat() # like javascript array.flat()

users.slice(1, 3)
users.divide(4) # divides the array into 4 quarters and returns an array containing sub arrays of the 4 quarters
users.to_str()
users.join(', ')

# array iterators also would exist, like .each() to run a callback for each item, .map() to run a callback to modify each item, .find(), .sort(), .filter(), and other stuff would also exist, etc
```
---
### Table
```rb
inventory = { banana: 15, burger: 4, mawn_lower: 47 }

inventory.mayonnaise = 7

# also the compiler will give you a warning if you try to manually assign a value to a key starting with an underscore, it wont stop you from running the code but it will warn you

inventory._keys # list of keys
inventory._values # list of values
inventory._pairs # something like [['banana', 15], ['burger', 4], ...]
```

## Time

> Very work in progress, has no timezone support or anything which isnt great, and there are still a lot of functions i need to add, so just dont pay any attention to how useless this is so far
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

now.sinceUnixEpoch # all the above unit properties exist on here as well (except unix timestamp) but they count the number of that unit that has elapsed since the unix epoch

# these just change the `hours` property to be out of 12 or 24. Converting back to 24 will internally use the `morning` or `afternoon` properties to figure things out.
now.as_12h_format()
now.as_24h_format()
now.to_iso_string()
# '2019-01-25T02:00:00.000Z'
# ISO 8601 string thing, also ignore the fact that it is using a completely different time, idk how to convert to ISO 8601, ill figure it out

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