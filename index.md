# Aspen
thats what im calling this language, aspen

this is an early version, im also tryna design a better static typed version with less bad design

## Values
---
```rb
# Comments

#/
multiline comments (even tho the syntax highlighting shows this text as not a comment it still is a comment)
/#

# String
'Hello'
"Hi"

# Bool
true
false

# Number
123
3.14
-29
# No distinction between integers and floats, they are all double precision floating point integers behind the scenes

# Null
null
```

## Variables
---
```rb
var my_var = "Hello"
var other_var = "World"

# Prints with newline
println( my_var )

# Prints without newline
print( other_var )
```

## Math
---
```rb
# Basic numeric math
println( 5 + 3 )
println( 23 % 7 )
# Exponentiation
println( 5 ** 3 )
# String concatenation also exists
println( "Hello " + "world" )
# And string multiplication
println( "get out of my head " * 10 )
```

### Math libary
```rb
# Just like an import statement, it includes that module (in this case a standard library module) in the script
uses Math

# Examples of some functions, using a module makes its contents available in the global scope
println( abs(-8) )
println( sqrt(25) )
println( pi )
```

## Operators
---
```rb
println( true or false ) # true
println( true and false ) # false
println( not true ) # false
println( false || true ) # true
println( true && true ) # false
println( !false ) # true
println( 1 + 2 ) # 3
println( 3 - 4 ) # -1
println( 3 * 6 ) # 18
println( 20 / 4 ) # 5
println( 15 % 4 ) # 3
println( 2 ** 4 ) # 16
println( ~5.6 ) # 6, squiggly ~ rounds a number to the nearest integer
println( 5 > 3 ) # true
println( 4 < -3 ) # false
println( 5 >= 5 ) # true
println( 5 <= 6 )# true
println( 3.4 ~= 3.2 ) # true, rounds the two numbers to the nearest integer and then checks equality
println( true ? "yes" : "no" ) # "yes"

# also <=> like what ruby has

# & | ^ ~ << >>` bitwise operators will also exist

# Now here is a tricky one
# (lists shown in a little more detail later and functions in functions.md)
var my_list = [1, 2, 3]
my_list.=reverse

# .= as used here is basically shorthand for my_list = my_list.reverse
```

## Conditionals
---
```rb
if true println( "beans" )
println( "goodbye world" ) if false

if 5 == 5 {
    println( "bruh" )
} else if 3 == 4 {
    println( "ok" )
} else {
    println( "huh" )
}

println( 5 + 5 != 248 ? "hello" : "world" )

# Switch statement stuff, "test"s against multiple "case"s
var weekday_number = some_function_that_returns_a_number_between_0_and_6_representing_the_current_day_of_the_week()

# Single statement cases
test weekday_number {
    case 0: print( "Sunday" )
    case 1: print( "Monday" )
    case 2: print( "Tuesday" )
    case 3: print( "Wednesday" )
    case 4: print( "Thursday" )
    case 5: print( "Friday" )
    case 6: print( "Saturday" )
    default: print( "Invalid day" )
}


var username = login() # a function that doesnt exist but just pretend it does for the sake of this example

# Multi statement cases
test username {
    case "Bob" {
        open_desktop()
        start_apps()
    }
    case "Admin" {
        open_desktop()
        start_apps()
        open_admin_panel()
    }
    default {
        logout()
    }
}
```

## Loops
---
```rb
# Simple while loops
while humans_exist {
    dominate(world)
}

# Simple for loops
for (var i = 0; i < 100; i++) {
    println( "hello your virus has computer" )
}

for i in 1..100 {
    print( "AAA" )
}

# Another way to loop, uses a callback
repeat 100 (i) -> print( "bruh " )
```

## Functions
---
```rb
fun cool_fact() {
    println( "Bees have 5 eyes" )
}

cool_fact() # println(s the thing

# Short-hand syntax
fun cube(num) -> num ** 3

println( cube(3) ) # 27

# Named parameters
fun greet(:first_name, :last_name) {
    # Template strings
    println( "Hello #{first_name + last_name}" )
}

# Named arguments can be passed in any order, these do the same thing
greet(first_name: "Bob", last_name: "Fitzgerald")
greet(last_name: "Fitzgerald", first_name: "Bob")

# Callbacks
fun call_function(callback, arg) -> callback(arg)
call_function((arg) -> { println( arg ) }, "Hello world")

# Callback syntax: "(" args?+ ")" -> ("{" code+ "}") | expression
```

## Data structures
---
```rb
# List
var letters = ["A", "B", "C"]
println( letters[1] ) # "B"

# Dictionary
var employees = [jim: "Software Engineer", bob: "Manager", eric: "Coffee Coordinator"]
println( employees.jim ) # "Software Engineer"
println( employees.bob ) # "Manager"

# Prints "A B C "
for letter in letters {
    print( "#{letter} " )
}
```

## Classes
---
```rb
# Simplest class, a data class. Defined in a single line, and given paramters similar to that of functions. Paramter names become the names of the instance's equivalent fields
# NOTE: im realizing now this seems a lot like a struct so i might just replace it with something like that, i dont know
data class Human (name, age, occupation)

tom = new Human("Tom", 26, "Unemployed")
println( tom.name ) # "Tom"
println( tom.occupation ) # "Unemployed"

# More complex classes (yes cars are more complex than people)
class Car {
    # Class variable. Doesn't exist on instances, only on the main class, but instances can access it internally. It is initialized once when the class itself is initialized
    # Not sure if I'll be able to implement this easily
    @cars_produced = 0

    init(model, year, mpg) {
        this.model = model
        this.year = year
        this.mpg = mpg
        @cars_produced++
    }

    drive(miles) {
        print( "Vroom vroom! " )
        println( "Used #{miles / this.mpg} gallons of fuel." )
    }

    # Class function, only available on the class itself
    @contact_dealership() {
        println( "We'll be right with you. Please hold..." )
    }
}

var epic_super_car = new Car("Honda Civic", 1482, 3)
epic_super_car.drive(12) # "Vroom vroom! Used 4 gallons of fuel."

Car.contact_dealership() # "We'll be right with you. Please hold..."
```
Fancier example here
```rb
# A class to represent user accounts
class User {
    @user_count = 0
    # Fields that cannot be accessed outside the class. Since @users is private, the @login method should be used to try to log into a specific account.
    private @users = []
    private password

    init(username, password) {
        if not @check_existing(username) {
            this.username = username
            this.password = password
            @user_count++
            @users.add(this)
        } else println( "That username already exists!" )
    }

    # this usage of .find() might change, not sure
    @check_existing(username) -> @users.find({ username: username }) != null

    # A superclass method that will try to log into a specific user. If the login is successful, it returns the instance of that user.
    @login(username, password) {
        # Find the user by the username. Method will return null if it doesn't exist.
        user = @users.find({ username: username })

        if not user {
            println( "That user doesn't exist" )
            return
        }

        # Check if the password is correct. Has to call the method on that user instance since password is a private field. If the password is correct, return the user.
        if user.test_password(password) return this
        else println( "Incorrect password" )
    }

    # Check if a password is correct.
    test_password(password) -> password == this.password

    get username() -> "@#{this.username}"
    set username(new_name) {
        # Sets the username if that username is not already in use.
        if not @users.find({ username: new_name }) {
            this.username = new_name
        } else println( "That username already exists!" )
    }
}

var bob = new User('epicbob39', 'thefitnessgrampacertest')
var anonymous = new User('xX_HackerFace64_Xx', 'password1')

# Logging in later
var user = User.login('xX_HackerFace64_Xx', 'password1')
var other_user = User.login('epicbob39', 'bruh') # "Incorrect password"
```

## Custom Operators (this might not actually be added, or maybe it will but not like this idk)
---
A custom operator can be anything that isn't already used in the language's grammar. For example, you can't define `*` as an operator, but something like `*!` is fine, since that on its own is not valid syntax by default.

> this probably wont be like this, im sure ill change it later, this is just a placeholder idea
```rb
# A custom binary operator (two operands) using `$` as its symbol that just returns the hypotenuse (a squared plus b squared)
# The body simply acts like a function body. A not-null return statement is required
define ((arg1) $ (arg2)) {
    return arg1**2 + arg2**2
}

println( 3 $ 5 ) # 34
println( 2 $ 3 * 3 ) # 39. Acts like ((2 $ 3) * 3), since custom operators will have the same precedence as function calls
```