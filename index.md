# Facescript

# NEW NAME IDEA
## "Aspen", not currently taken by any programming language

## Values
---
```rb
# Comments

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
```py
# Can use either `=` or R-style `<-`
my_var = "Hello"
other_var = "World"

# Prints with newline
echo my_var

# Prints without newline
print other_var
```

## Math
---
```py
# Basic numeric math
echo 5 + 3
echo 23 % 7
# Exponentiation
echo 5 ** 3
# String concatenation also exists
echo "Hello " + "world"
# And string multiplication
echo "get out of my head " * 10
```

### Math libary
```rb
# Just like an import statement, it includes that module (in this case a standard library module) in the script
uses Math

# Examples of some functions, using a module makes its contents available in the global scope
echo abs(-8)
echo sqrt(25)
echo pi
```

## Operators
---
```rb
echo true or false # true
echo true and false # false
echo not true # false
echo false || true # true
echo true && true # false
echo !false # true
echo 1 + 2 # 3
echo 3 - 4 # -1
echo 3 * 6 # 18
echo 20 / 4 # 5
echo 15 % 4 # 3
echo 2 ** 4 # 16
echo 5 > 3 # true
echo 4 < -3 # false
echo 5 >= 5 # true
echo 5 <= 6 # true
echo 3.4 ~= 3.2 # true, rounds the two numbers to the nearest integer and then checks equality
echo true ? "yes" : "no" # "yes"

# `& | ^ ~ << >>` bitwise operators will also exist
```

## Conditionals
---
```rb
if true echo "beans"
echo "goodbye world" if false

# These two do the same thig, can use do-end or { }
if 5 == 5 do
    echo "bruh"
else if 3 == 4 do
    echo "ok"
else do
    echo "huh"
end

if 5 == 5 {
    echo "bruh"
} else if 3 == 4 {
    echo "ok"
} else {
    echo "huh"
}

echo 5 + 5 != 248 ? "hello" : "world"

# Switch statement stuff, "test"s against multiple "case"s
weekday_number = some_function_that_returns_a_number_between_0_and_6_representing_the_current_day_of_the_week()

# Single statement cases
test weekday_number {
    case 0: print "Sunday"
    case 1: print "Monday"
    case 2: print "Tuesday"
    case 3: print "Wednesday"
    case 4: print "Thursday"
    case 5: print "Friday"
    case 6: print "Saturday"
}

username = login()

# Multi statement cases
test username {
    case "Bob"
        open_desktop()
        start_apps()
    end
    case "Admin"
        open_desktop()
        start_apps()
        open_admin_panel()
    end
    default
        logout()
    end
}
```

## Loops
---
```rb
# Simple while loops
while humans_exist do
    dominate(world)
end

# Simple for loops
for (i = 0; i < 100; i++) do
    echo "hello your virus has computer"
end

for i in 1..100 do
    print "AAA"
end

# Another way to loop, uses a callback
repeat 100 (i) -> print "bruh "
```

## Functions
---
```rb
fun cool_fact() {
    echo "Bees have 5 eyes" 
}

cool_fact() # echos the thing

# Short-hand syntax
fun cube(num) -> num ** 3

echo cube(3) # 27

# Named parameters
fun greet(:first_name, :last_name) {
    # Template strings
    echo "Hello #{first_name + last_name}"
}

# Named arguments can be passed in any order, these do the same thing
greet(first_name: "Bob", last_name: "Fitzgerald")
greet(last_name: "Fitzgerald", first_name: "Bob")

# Callbacks
fun call_function(callback, arg) -> callback(arg)
call_function((arg) -> { echo arg }, "Hello world")

# Callback syntax: "(" args?+ ")" -> ("{" code+ "}") | expression
```

## Data structures
---
```rb
# List
letters = ["A", "B", "C"]
echo letters[1] # "B"

# Dictionary
employees = [jim: "Software Engineer", bob: "Manager", eric: "Coffee Coordinator"]
echo employees.jim # "Software Engineer"
echo employees.bob # "Manager"

# Prints "A B C "
for letter in letters do
    print "#{letter} "
end
```

## Classes
---
```rb
# Simplest class, a data class. Defined in a single line, and given paramters similar to that of functions. Paramter names become the names of the instance's equivalent fields
data class Human (name, age, occupation)

tom = new Human("Tom", 26, "Unemployed")
echo tom.name # "Tom"
echo tom.occupation # "Unemployed"

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
        print "Vroom vroom! "
        echo "Used #{miles / this.mpg} gallons of fuel."
    }

    # Class function, only available on the class itself
    @contact_dealership() {
        echo "We'll be right with you. Please hold..."
    }
}

epic_super_car = new Car("Honda Civic", 1482, 3)
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
        if not @check_existing(username) do
            this.username = username
            this.password = password
            @user_count++
            @users.add(this)
        else echo "That username already exists!"
    }

    @check_existing(username) -> @users.find({ username: username }) != null

    # A superclass method that will try to log into a specific user. If the login is successful, it returns the instance of that user.
    @login(username, password) {
        # Find the user by the username. Method will return null if it doesn't exist.
        user = @users.find({ username: username })

        if not user do
            echo "That user doesn't exist"
            return
        end

        # Check if the password is correct. Has to call the method on that user instance since password is a private field. If the password is correct, return the user.
        if user.test_password(password) return this
        else echo "Incorrect password"
    }

    # Check if a password is correct.
    test_password(password) -> password == this.password

    get username() -> "@#{this.username}"
    set username(new_name) {
        # Sets the username if that username is not already in use.
        if not @users.find({ username: new_name }) do
            this.username = new_name
        else echo "That username already exists!"
    }
}

bob = new User('epicbob39', 'thefitnessgrampacertest')
anonymous = new User('xX_HackerFace64_Xx', 'password1')

user = User.login('xX_HackerFace64_Xx', 'password1')
other_user = User.login('epicbob39', 'bruh') # "Incorrect password"
```

## Custom Operators
---
A custom operator can be anything that isn't already used in the language's grammar. For example, you can't define `*` as an operator, but something like `*!` is fine, since that on its own is not valid syntax by default.
```rb
# A custom binary operator (two operands) using `$` as its symbol that just returns the hypotenuse (a squared plus b squared)
# The body simply acts like a function body. A not-null return statement is required
define ((arg1) $ (arg2)) {
    return arg1**2 + arg2**2
}

echo 3 $ 5 # 34
echo 2 $ 3 * 3 # 39. Acts like ((2 $ 3) * 3), since custom operators will have the same precedence as function calls
```

## 