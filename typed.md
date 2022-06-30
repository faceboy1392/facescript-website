# Typed Aspen

> note this isnt an alternate version of aspen, its simply a different idea of what i might do with the language, if i choose to try and make it statically typed

also this isnt meant to be proper documentation, its really just me writing down ideas

also markdown code blocks are using ts for syntax highlighting because i said so and this is my website and i can do what i want

also now that i think of it this seems a lot like a rip off of typescript syntax

## Values & variables
```ts
var my_bool: bool = true
var my_num: int = 10
var my_float: float = 1.2
var my_double: double = 2.49
var my_char: char = 'A'
var my_string: string = "mawn lower"

const my_const: bool = false

{
    global my_global_variable = "yes"
}

println(my_global_variable) // "yes"
```

## Conditionals
```ts
var today: string = "friday"

if today == "friday" {
    println("yay")
} else {

}
```

## object
```c
struct Humanoid {
    name: string,
    age: int,
    height: float,
    number_of_eyeballs: int
}

class Car {}
```