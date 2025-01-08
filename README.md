
WIP PLEASE COME BACK LATER


# Introduction 

[Luau](https://luau.org/) is an open source general purpose programming language that is developed and maintained by [Roblox](https://roblox.com). Luau is a superset of [Lua](https://www.lua.org/) and introduce many new features most notably typing! It is often used to develop experiences for [Roblox](https://roblox.com). This is guide is mainly written for folks who have some familiarity with programming and would like to start using Luau! If you are new to programming and would like to learn Luau for the purpose of writing your own Roblox game, we suggest you get started on the [creator docs site](https://create.roblox.com/docs)!

We aim to keep as much of this content as general as accessible as possible and many parts will explicity mention how to use Luau with Roblox. Sections that are entirely new to Luau are tagged with `Luau`. If you are skimming through the guide because you are already familiar with Lua, these are the sections you want to pay attention to!

This guide takes much inspiration (and some content) from the freely available online [Programming in Lua](https://www.lua.org/pil/) book as well as the resources on the [Luau website](https://luau.org/). Several sections currently link out to the Programming in Lua and you can easily infer the Luau types for the content in that guide after reading this one!

This guide was started as a Roblox Hack Week project. We aim to grow and evolve this guide over time and the current version should already be more than enough to really get you going with Luau!

# Additional Resources

- [Lua 5.1 manual](https://www.lua.org/manual/5.1/manual.html#5.4) (5.1 is the version where Luau diverged from Lua).
- [Luau lang website](https://luau.org/library)
- [Roblox Creator Docs site](https://create.roblox.com/docs)

# Getting Started

While Luau can be used as a standalone language, it is almost always embedded as a scripting language in another program such as Roblox. The easiest way to get started with writing and running Luau code is with the [Luau online interpreter](https://luau.org/demo). The next easiest way is...

## With Roblox

To get started with Luau in Roblox, go to the [Roblox Creator Hub](https://create.roblox.com/), log in/make an account, and download Roblox Studio. From the templates tab, create a new empty Baseplate project. Then in the explorer widget, write click under "workspace" and create a new script. To test your script, press the ▶️ button and you should see any output (from `print` commands which we will introduce later) in the Console widget.

The built in Roblox script editor will automatically run the Luau typechecker on your code and tell you if there are any errors

<TODO screenshot>

If you are using tools like LFS or Rojo to develop code in Visual Studio Code, you can use the community created [Luau Language Server](https://marketplace.visualstudio.com/items?itemName=JohnnyMorganz.luau-lsp) extension to get the same typechecking experience in your editor!

<TODO screenshot>

## Without Roblox

If for some reason you want to use Luau without Roblox (perhaps you are trying to embed Luau as a scripting language for your own project) you can download the interpreter on the [Luau Github page](https://github.com/luau-lang/luau) and run the code directly. You may also want to try the open source Luau runtime environment [Lune](https://github.com/lune-org/lune) to power up your program and make things a lot easier in general too! 

## Understanding the Roblox Luau Runtime Environment

If you are not using Luau with Roblox you can skip this section!

Roblox experiences are complex and multi-user and therefore there are a few things you should understand about *when* and *where* your Luau scripts run. Each Roblox experience has one or more clients (or players) connected to a server (called RCC). Scripts can run on either client or server. Roblox scripts can affect the game world, and by default, effects generated by server scripts automatically get replicated to all clients whereas effects on client scripts remain local. There are some exceptions to this rule that are beyond the scope of this guide!

Luau scripts are wrapped inside of `Instances` in the Roblox engine.

There are 3 types of script `Instances`

- Scripts: these run on the server only
- LocalScripts: these run on clients only
- ModuleScripts: these do not run by themselves

Anytime a `Script` or `LocalScript` instance is created (for example, when you launch the experience), the Roblox engine will run the code in the file. You can not control the order in which scripts run. These are the entry points into your Luau program.

`ModuleScripts` are reusable modules can be `require(...)`'d by other scripts. One major difference when developing on Roblox is that the Roblox runtime environment has a Datamodel rather than a filesystem. Therefore, instead of traversing the filesystem e.g. `require(helpers/myhelperscript.luau)` you need to traverse the Datamodel to find your module script e.g. `require(GetService("ReplicatedStorage").helpers.myhelperscript)`

TLDR to run Luau on Roblox, create a `Script` instance and hit the playtest button. Your script will run on the server and you will still be able to see its output on your local console.



# Getting Started

# Basic 💩

## Chunks 

<TODO>

## Variables

Variables are about what you'd expect in Luau. Variables can be assigned to with the `=` operator. 

Global variables do not need to be declared. You simple assign to them and they get created if they don't already exist or assigned to if they do.

```
myGlobalVar = "I created a global variable"
```

To remove a global variable, you simply assign `nil` to it

```
myGlobalVar = nil
```

In general, an object with a `nil` value  is equivalent to object not existing in Luau. You will see more of this in the tables section.

<sub>Global variables can be accessed via the `_G` table i.e. `_G["myGlobalVar"]` however if you ever find yourself wanting to do this please just stop.</sub>

Using global variables is discouraged by 9/10 software engineers so instead please avoid globals as much as possible!!

Local variables are variables that are scoped to the block or chunk in which they are declared. Local variables shadow any globals or locals in the parent scope. Local variables are declared with the `local` keyword. If you'd like to create a scope (block) for your local variables, you can use the `do` control expression

```
do
    local myLocalVariable = "I am a local variable"
    print(myLocalVariable)
    -- prints 
end
print(myLocalVariable) -- prints nil
```

All variables in Luau are typed either implicitly or explicitly. We'll go into this more in the typing section.

```
local myExplicitlyTypedNumber : number = 76
local myImplicitlyTypedNumber = 32
```


## Control

<TODO add stuff from https://luau.org/syntax>

## Expressions
This seciton covers relational and logical operators. String and table expressions are covered in later sections.
### Relational Expressions
### Logical Expressions

### Conditional Control
#### Conditional Expressions
In Luau, any value may be used as a condition. Conditionals (e.g. `if <condition>`) regard `false` and `nil` as false and everything else as true including `0` and the empty string `""`.
### Loops
#### numeric for 
#### generic for

you can make 
#### while
#### repeat
#### break



## Functions (basic)

## Adding Types (Luau)

The most important addition to Luau is the addition of types. Types add an additional level of correctness to you program! The addition of types to your pogram does not affect the way your pogram runs--instead, it allows the Luau type checker to statically analyze your code and help ensure everything is correct.


### Enabling the type checker

In Roblox, the Luau type checker is set to run in nonstrict mode by default. We recommend enabling strict mode by adding the `--!strict` directive to the top of your luau script. If you are using Luau outside of Roblox or with a third party tool like Rojo, there may be other configuration files you can use to globally set what mode of the typechecker

<details>
    <summary>Luau Typechecker Modes (not important)</summary>

    - --!nocheck,
        - do not run the typechecker
    - --!strict
        - (recommended) run the type checker in strict mode
    - --!nonstrict
        - (default) similar to strict mode, but is more relaxed in inferring types.
</details>


### Basic syntax

To declare the type of a variable, use the `:` symbol. For example, to declare a variable of type `number` (types are covered later) we can do the following:

`local myTypedNumber : number`

Variables in functions are type in the same way, and the return type is added at the end:

```
local function parrot(wordToSay : string, numberTimes : string) : string
    local output : string = ""
    for i = 1, numberTimes, 1 do
        output = output .. wordToSay
    end
    return output
end

```

Luau will also infer types for you.

```
local x = 5
print(typeof(x)) -- prints "number"
```

It is this author's opinion that you should avoid relying on type inference as much as possible!

<sub>NOTE There are some limitations in the current Luau type checker when it comes to type inference and type refinement. There is a new typechecker (to be released someday) that will solve many of these issues!</sub>

Types do not affect runtime in anyway

```
local myTypedNumber : number = 5
print(myTypedNumber) -- prints 5
myTypedNumber = "hello" -- this is a Luau type error and the program will still run just fine!
print(myTypedNumber) -- prints "hello"
```


### Why are Types Useful?

Types help ensure your programs correctness. For example consider the following function:

<TODO>

As your program grows in complexity, type errors like the above become increasingly complex and harder to track. Adding types to your pogram is a small investment that will greatly improve your engineering efficiency!

Types also make your code a lot more readablefor others. For example, types allow you to readily read what arguments a function takes and what output to expect from it:

<TODO>

### To learn more about types

The [Luau Typechecking](https://luau.org/typecheck) page is a great resource. Please check it out to learn more about advanced typing features!

# Primitive Types

The Luau comes with 10 primitive types: 

- `nil`
- `string`
- `number`
- `boolean`
- `table`
- `function`
- `thread`
- `userdata`
- `vector`
- `buffer`

The first 4 are the very basic types. The remaining types will be covered in other sections

## nil

The `nil` _type_ can also take the _value_ `nil`. The `nil` _value_ can still be a value of all other types (except the `never` type, more on that later). The `nil` type is special and is also rarely useful. Don't worry too much about it. 

## number

`number` is Luau's only built in number type. They are represented internal with real double precision floating point number. Luau's number should be sufficient for 99.99% percent of your needs!

Here are some examples of valid number expressions

`4`     `1.4723`     `4.57e-3`     `0.3e13`     `8e+22`

Luau supports the binary number operators 

- `+` addition
- `-` substraction
- `*` multiplication
- `/` division
- `^` exponentiation

and the unary operator

- `-` negation

with standard operator precedence.

## string

Luau strings represent a sequence of characters. They are immutable so if you want to change them you need to create a new string. Luau strings are eight-bit clean so they can hold any characters although if you are storing binary data, the `buffer` type may be more appropriate.

Luau strings can be concatenated with the `..` operator, and can be passed into the `print` function for debugging:

```
local cuteAnimal = "bunny 🐰"
print("I am a " .. cuteAnimal) // prints "I am a cute bunny 🐰" to the console
```

Luau string literals can be delimited with either doubel quotes `""` or single quotes `''`. These are the same except they allow for unespcaped single quotes or double quotes respectively.

The following special characters can be escaped:

- `\a`: bell  
- `\b`: back space  
- `\f`: form feed  
- `\n`: newline  
- `\r`: carriage return  
- `\t`: horizontal tab  
- `\v`: vertical tab  
- `\\`: backslash  
- `\"`: double quote  
- `\'`: single quote
- `\[`: left square bracket  
- `\]`: right square bracket  

Luau comes built in with very useful string manipulation functions in its standard library. You can see a list of methods available [here](https://luau.org/library#string-library). The Programming in Lua book has a [good section](https://www.lua.org/pil/20.html) on the `string` library if you are looking for more guidance.

## boolean

The Luau `boolean` type has two values: `true` and `false`, these are frequently used in conditional expressions however not all conditionals are booleans. Please see the Logical Expressions section for how to work with booleans.

# More on types

## The `typeof` function

You can determine the type of a variable with the `typeof` function

```
local x = 5
print(typeof(x)) -- prints "number"
```

This has various uses beyond telling you the type of a variable which we will cover soon!

## never, any, unknown types

`unknown` is the "top type", that is it’s a union of all types. An `unknown` typed variable can take on any value. 

```
local a: unknown = "hello world!"
local b: unknown = 5
local c: unknown = function() return 5 end
```

Unlike `any`, `unknown` will not allow itself to be used as a different type!

```
local function unknown(): unknown
    return if math.random() > 0.5 then "hello world!" else 5
end
```

```
local a: string = unknown() -- not ok
local b: number = unknown() -- not ok
```

In order to turn a variable of type `unknown` into a different type, you must apply type refinements on that variable.

```
local x = unknown()
if typeof(x) == "number" then
    -- x : number
end
```


<details>
  <summary>The never type (not important, just ignore me, seriosuly)</summary>


`never` is the bottom type, that is the sub type of all types. It is the "dual" of `unknown` that is, a value of type `never` must be assignable to a variable of any type. There is no such value in Luau. You might think that's `nil` and you would be right except that `nil` is not a valid value of the `never` type. `never` is occasionally useful, one such use case is when type refinements proves it impossible:

```
local x = unknown()
if typeof(x) == "number" and typeof(x) == "string" then
    -- x : never
end
```
</details>

`any` is just like `unknown`, except that it allows itself to be used as an arbitrary type without further checks or annotations. Essentially, it’s an opt-out from the type system entirely.

```
local x: any = 5
local y: string = x -- no type errors here!
```

`any` is useful when working with untyped code. Otherwise avoid it as much as possible and type your code! If your code is getting so complicated that you find yourself using the `any` type because you can't reasonably determine the types you are using that's often a sign you should simplify your code!



## union types

Types can be unioned with the `|` _type_ operator. For example

```
function gimmeStringOrNumber(x: string | number)
    if typeof(x) == "string" then
        print("You gave me a string: " .. x)
    else
        print("You gave me a number: " .. tostring(x))
    end
end

gimmeStringOrNumber("hello") -- prints "You gave me a string: hello"
gimmeStringOrNumber(5) -- prints "You gave me a number: 5"
gimmeStringOrNumber(true) -- not valid
```

Using symbols from math, we say `number` ⊆ `number | string` to indicate that  `number` is a subtype of `number | string`. We saw earlier that `X` ⊆ `unkown` for ALL types `X`.

The above is already very useful and this is not the only way to have subtypes. The subtyping relation will become much more relevant when we cover table types!

## type refinements

<TODO copy from website, add formal definiton for truthy>

Note. There are some limitations in the current Luau type checker when it comes to type inference and type refinement. There is a new typechecker (to be released someday) that will solve many of these issues!


## function types

Functions are first class objects in Luau and have their own type syntax. 

To declare a typed function e.g.

```
local function myTypedFunction(name : string, numApples : number) : string
    return arg1 .. " ate " .. tostring(numApples) .. " apples."
end
```

And to refer to a function as a typed value e.g.

```
local f : (string, number) -> string
f = myTypedFunction
```

### multiple return values

If your function returns multiple values you can use the following syntax e.g.

```
-- gimme has type `() -> (number, string)`
local function gimme() -> (number, string)  
    local things : {string} = {"apple", "orange", "xbox"} -- (the type of `things` is an indexed table type, we will cover it later)
    return (math.random(5), things[math.random(#things)])
end

local num, things = gimme()
```

### variadic args

<TODO you can do better than the one on the luau lang website>


### type inference on functions

Let’s start with something simple.

```
local function f(x) return x end

local a: number = f(1)     -- ok
local b: string = f("foo") -- ok
local c: string = f(true)  -- not ok
```

In strict mode, the inferred type of this function `f` is `<A>(A) -> A` (take a look at generics), whereas in nonstrict we infer `(any) -> any`. We know this is true because `f` can take anything and then return that. If we used `x` with another concrete type, then we would end up inferring that.

Further type inference on functions works (for the most part) like you would hope. 

```
local function greetingsHelper(name: string) : string
    return "Hello, " .. name
end

local function greetings(name)
    return greetingsHelper(name) -- infers type `(string) -> string` for the variable `name`
end

print(greetings("Alexander"))          -- ok
print(greetings({name = "Alexander"})) -- not ok
```

In general though, it is this author's opinion that it is better to always explicitly type your functions except perhaps in cases where your function is truly generic like in the simple example above.

## table types, table indexers and intersection types
This is SUPER DUPER important. This is covered in the table section!

## typecasting

You can force a value to be a certain type with the `::` symbol. This is called typecasting. You can only typecast if the value type shares a subtype with the type being casted too. Luau can not verify that the typecast will be valid during runtime. For this reason avoid typecasting as much as possible.

```
local a : string | number = 1
local b : number = a -- not ok
local c : number = a :: number -- ok
local d : string = a :: string -- ok, but d will not actually be a string
print(d) -- error! can't print a number! Don't typecast!
```

Typecasting is mainly useful when working with untyped Lua code or when you need to help along the typechecker with inference in some scenarios which will likely no longer be needed when the new typechecker is released. 


# Value + Reference + Immutable types

In Luau, variables are either value or reference types. The value of a variable is the actual data that the variable holds. The reference of a variable is the location in memory where the data is stored.

The following primitive types in Luau are value types:

- `nil`
- `number`
- `boolean`

The remaining primitives are reference types. Note that while `string` is a reference type, they behave like value types because they are immutable (more on this later).


```
local a = 5
local b = a
b = 6
print(a) -- prints 5
print(b) -- prints 6
```

In the above example, `a` is of type `number` which is a value type. The value of `a` is copied to `b` so changing `b` does not affect `a`. 

```
local a = {5}
local b = a
b[1] = 6
print(a[1]) -- prints 6
print(b[1]) -- prints 6
``` 

In the above example, `a` is a table type which is a reference type. The reference of `a` is copied to `b` so changing `b` does affect `a`.

In addition though, there are immutable references. Their contained values can never change. These behave like value types with respect to assignment (`=`). The `string` type is an example of an immutable reference type.

``` 
local a = "hello"
local b = a
b = "world"
print(a) -- prints "hello"
print(b) -- prints "world"
```

Note that all value types are also immutable. The only other immutable references in Luau are frozen tables. These are tables that have been made immutable with the `table.freeze` function. We will talk about them more in the table section. 


# Tables (Introduction)
Tables are the do-all data structure in Lua. While there are a few more options in Luau, tables remain super important so it's important to understand them well! 

## Basics
Tables are associative arrays (AKA dictionaries/maps) and can be indexed with strings, numbers, or any other Luau value except `nil`!

To create an empty table:

```
local myTable = {}
```

To set or modify values in a table:

```
myTable.name = "Alice"
myTable.age = 25
``` 

To create a table with some initial values:

```
local myTable = {name = "Alice", age = 25}
```

To access a value in a table:

```
print(myTable.name) -- prints "Alice"
print(myTable.age) -- prints 25
```

To explicitly define the type of the above table:

```
local myTable : {name: string, age: number} = {name = "Alice", age = 25}
```

To delete a key from a table:

```
myTable.name = nil
```

To check if a key exists in a table:

```
if myTable.name != nil then
    print("name exists")
else
    print("name does not exist")
end
```

## As Arrays

Luau contains a set of built in functions for using tables as arrays. The "array" portion of the table includes all the elements with continuous integer keys starting at 1. You can instantiate such an array with the following syntax:

```
local myArray = {"c", "o", "w"}
print(myArray[1] .. myArray[2] .. myArray[3]) -- prints "cow"
```

Luau comes with a [bunch of useful functions](https://luau.org/library#table-library) for manipulating tables as arrays. For example:

To add an element to the end of an array:

```
table.insert(myArray, "s")
print(myArray[1] .. myArray[2] .. myArray[3] .. myArray[4]) -- prints "cows"
```

To remove an element from an array:

```
table.remove(myArray, 4)
print(myArray[4]) -- prints nothing
```

Luau tables have no order however we can at least iterate over the array portion of a table in the expected order. To "sort" a table, we can use the `sort` function which sorts the values in the array portion of the table (changing their indices). 

```
local myArray = {"w", "o", "c"}
print(myArray[1] .. myArray[2] .. myArray[3]) -- prints "woc"
sort(myArray)
print(myArray[1] .. myArray[2] .. myArray[3]) -- prints "cow"
```

For more details on sort, see this [article](https://www.lua.org/pil/19.3.html) in the Programming in Lua book.

Using tables as arrays has one drawback. Tables can not hold `nil` values as this simply deletes the key so arrays can not hold `nil` values as this would break the continuous integer key requirement. To work around this, you can use the `getn` and `setn` functions. See [this article](https://www.lua.org/pil/19.1.html) in the Programming in Lua book for more information.


## Iterating over tables


In Lua, iterators were required to `for` loop over element in tables. To learn more about iterators, see the article on this topic in the [Programming in Lua](https://www.lua.org/pil/7.1.html) book. In Luau we can iterator over table key value pairs directly:

```
local myTable = {name = "Alice", age = 25}
for key, value in myTable do
    print(key, value)
end
-- prints "name Alice" followed by "age 25"
```

Iteration order goes through continous numeric keys starting at 1 first (i.e. 1...#myTable), and then through the remaining elements with no guarantee on order. This is the same behavior as iterating with `pairs`. Modifying table entries for any other keys besides the current one in the iterating results in undefined behavior.

To iterate over only the numeric keys of a table, you can use the `ipairs` function:

```
local myTable = {"a", "b", "c", cat = "meow"}
for i, value in ipairs(myTable) do
    print(i, value)
end
-- prints "1 a" followed by "2 b" followed by "3 c"
```

## Table Keys
In the above examples, we used built in Luau syntax that automatically defines literal numeric and string keys. However, you can use any Luau value as a key in a table including values contained in variables. The generic syntax for accessing a value in a table is `myTable[key]` where `key` is some luau value.

```
local myTable = {}
local key = "name"
myTable[key] = "Alice"
print(myTable[key]) -- prints "Alice"
print(myTable.name) -- prints "Alice"
myTable["age"] = 25
print(myTable["age"]) -- prints 25
print(myTable.age) -- prints 25
```

You can even use other tables as table keys

```
local someTable = {}
local someOtherTable = {}
local myTable = {}
myTable[someTable] = "hello"
myTable[someOtherTable] = "world"
print(myTable[someTable]) -- prints "hello"
print(myTable[someOtherTable]) -- prints "world"
``` 


You can also use this syntax when constructing tables
    
```
local nameKey = "name"
local ageKey = "age"
local myTable = {
    [nameKey] = "Alice",
    [ageKey] = 25
}
print(myTable.name, myTable.age) -- prints "Alice 25"
```

## As Objects
Tables are often used as objects in Lua. A common pattern is to create an explicitly typed table to representy our object and create a set of functions that operate on that table. 

```
type Person = {
    name: string,
    age: number
}

local function Person_create(name : string, age : number) : Person
    return {name = name, age = age}
end

local function Person_greet(person : Person) : string
    return "Yo wassup, " .. person.name
end

local function Person_growOlder(person : Person) : Person
    return {name = person.name, age = person.age + 1}
end
```

You can also use metatables to create objects with methods built into them that look more like traditional object oriented programming. It is this author's opinion that this pattern should be avoided. This pattern is covered in the advanced section as it is apparently many folks do not share this author's opinion.

## Metatables
Metatables allow you to override certain behavior in tables. Metatables are used extensively by other libraries often to create more "convenient" interfaces. It is this author's opinions that metatables should be avoided perhaps the one exception of making container classes.  Metatables are covered in the advanced section. 

## Table Gotchas
Here are some common gotchas when working with tables in Lua. Pay careful attention especially if you are coming from another language:

- Tables as arrays are 1-indexed. The first element of an array is at index 1, not 0. There is nothing preventing you from using 0 as an index, but the built-in functions for working with tables as arrays will not work as expected.
- Tables as arrays can still hold non-continuous-numeric keys. These will simply not be part of the "array" insofar as the built-in array manipulation functions are concerned. For example if you have `t = {1, 2, 3, [5] = 5}` the length `#t` will be `3`.
- the `#` operator only returns the length of the array portion of the table. It will not return the total number of elements in the table!!!!!! To get the total number of elements in a table, you must iterate over the table and count them yourself 😭.
- Using `ipairs` to iterate over a table as an array will stop at the first non-continuous-numeric key. 
- A `nil` value to a key in a table is equivalent to that key not existing in the table. To delete a key from a table, you can assign `nil` to it.
- Tables have no order to them!!!! To create an ordered set, you can use tables as arrays and sort them with the `sort` function.
- Tables are passed by reference. When you pass a table to a function, you are passing a reference to the table, not a copy of the table. This means that if you modify the table in the function, the changes will be reflected outside of the function.
- Luau table types take a bit to get use to as the static type checker will do it's best to update the type as you add and remove items from the table. Understanding how the typechecker works for tables will eliminate a lot of potential bugs so it's worth getting use to!!

## new Luau table stuff (maybe move to advanced section)


# Functions

Similar to Javascript, functions are first class objects in Luau. This means that functions can be assigned to variables, passed as arguments to other functions, and returned from other functions. This is a very powerful tool that you should get use

## Syntax

function objects can be created using the lambda syntax:

```
local add = function(arg1 : number, arg2 : number)
    return arg1 + arg2
end
print(tostring(add(1,2))) -- prints "3"
```

Once created, a function object can be used like any other value:

```
-- assign to another variable
local myFunction = add
print(tostring(myFunction(1,2))) -- prints "3"

-- change it to something else
myfunction = function(arg1 : number, arg2 : number)
    return arg1 - arg2
end
print(tostring(myFunction(1,2))) -- prints "-1"
```

The perhaps more familiar function declaration syntax used earlier is in fact shorthand for the above. The below definiton is equivalent to the above:

```
local function add(arg1 : number, arg2 : number)
    return arg1 + arg2
end
```

## Closures
<TODO>
See [https://www.lua.org/pil/6.1.html](https://www.lua.org/pil/6.1.html) 


## Callback Pattern
One of the main uses of functions as first class objects is to pass them as arguments to other functions. This is a common pattern in Luau. For example, the `table.sort` function takes an optional comparison function as an argument:

```
local myArray = {3, 1, 2}
table.sort(myArray, function(a, b) return a < b end) -- by default, uses `<` as comparison, so we use `>` here
print(myArray[1], myArray[2], myArray[3]) -- prints "3 2 1"
``` 

You will see this pattern all over the place in the Roblox API which uses [events](https://create.roblox.com/docs/scripting/events) e.g.

```
local Players = game:GetService("Players")

Players.PlayerAdded:Connect(function(player)
	print(player.Name .. " joined the game!")
end)
```

# Built in Libraries

Luau ships with several built in libraries for common operations. Some have already been covered and some more useful ones are covered here. For a complete list, see [lua.org/library](https://luau.org/library).

## String Manipulation
## assert/error
## pcall
## math
## table (maybe cover in tabel section)
## io
The `io` provides functions for reading and writing files. These methods are usually not permitted when using Luau as an embedding scripting language for security reasons and this is the case for Roblox. The Programming in Lua book has a [good section](https://www.lua.org/pil/21.html) on the `io` library if you are interested in learning more about it.




# New Luau Primitives!


## userdata types

Luau is intended for use as an embedded language. That's why if you've ever read the Lua manual you'll notice that the majority is dedicated to the [C API for embedding Lua](https://www.lua.org/manual/5.1/manual.html#3) in your program <sub>(yes, I linked the 5.1 Lua manual... we still need to write one for Luau...)</sub>

In order for Luau to be useful as an embedded language, it must be able to interact with the data types in the program it is embedded in. Examples of Roblox data types are things like `Instance` and `Player`. These data types are called "userdata" types. These are not to be confused with table types which can have new items added and removed. Userdata types have static definitions. 


```
Instance myInstance = workspace.FindFirstChild("bearModel")
myInstance.Name = "bear" -- `Name` is a property of the `Instance` datatype so this is valid
myInstance.location = "Canada" -- `location` is not a property of myInstance, this is not valid!
```

Roblox data types are all documented on the very useful [Roblox Creator Docs](https://create.roblox.com/docs/reference/engine) site.

## vector

The Luau vector type represents a 3D vector. This is in fact the same type as the differently named [`Vector3` type in Roblox](https://create.roblox.com/docs/reference/engine/datatypes/Vector3) although currently the type checker thinks they are different (we'll fix it soon). You can use either the bulit in vector library or the Roblox API variants. The vector library variants are more portable!

The vector type is either 3 or 4 dimensions (x,y,z + w) depending on what the compile time `LUA_VECTOR_SIZE` flag is set to. 3 component vectors work like you would expect representing x y and z components. Roblox is configered to use 3 component vectors. 4 component vectors are needed for affine transformations which allow for things like translations to be represented as a matrices. This is super duper useful for computer graphics and much less useful for most games on Roblox. 4 component vectors are not useable on Roblox and thus are not covered in this guide.

To learn more about the vector library, see the [Luau Vector Library](https://luau.org/library#vector-library) page.

## buffer

The buffer is a fixed size mutable (as in you can modify it's contents) block of memory. All buffer operations are done through the built in `buffer` library. Buffers are useful in applications where bandwidth or performance is critical. Otherwise consider using tables as arrays instead. Note that all buffer library operations convert the contents to and from the `number` or `string` type but the internal representation is still a byte array.

To learn more about the buffer library, see the [Luau Buffer Library](https://luau.org/library#buffer-library) page.

## thread 

The `thread` type are used to represent a coroutine. These can be manipulated with the builtin [coroutine library](https://www.lua.org/pil/9.html). The Programming in Lua book has a [good section](https://www.lua.org/pil/9.html) on coroutines if you are interested in learning more about them.

If you are working in Roblox, coroutines are often managed by the [task library](https://create.roblox.com/docs/reference/engine/libraries/task). These methods create coroutines that are managed by the Roblox engine's TaskSchedule such that should not (ever) manually `coroutine.yield` and `coroutine.resume` them. The `thread` type and the `coroutine` type mentioned on the Roblox API website are the same.


# New Luau Features!
<TODO>





# Luau Tooling

Luau is open source and has a number super useful community supported tooling!

<TODO lune, wally, npm, linter, useful libraries,>

Please see the [Third Party Tools](https://create.roblox.com/docs/projects/external-tools) for using Luau tooling with Roblox.


# Roblox UI in Luau
## native
All of Roblox's [UI instances](https://create.roblox.com/docs/ui) can be managed with Luau code allowing you to generate UI entirely from Luau. This is the simplest create UI in Roblox. Many creators will author their UI in the Roblox Studio editor and then add Luau code to manage the interactions. You can also create your UI entirely from Luau code.

Using native UI is the simplest way to create UI in Roblox. You may find that you will start running into limitations as your UI needs become mor demanding and complex. Thankfully, there are UI libraries that can help you with this!

## fusion
Fusion is a declarative UI, state management and animation library for Roblox. This is an awesome choice for building UI in Roblox and relatively easy to pick up. Please see [https://elttob.uk/Fusion/0.2/](fusion) for more information on Fusion.

## react-lua
React-lua is a port of React to Luau. React is an industry standard for many web and mobile apps these days and modern React has never been easier to use. Nonetheless the learning curve is steeper than using native UI or fusion. If you are new to programming avoid react-lua. Please see my [react-lua](https://github.com/minimapletinytools/react-lua-tutorial/blob/main/react-lua-expert.md) tutorial :).


# Advanced Topics

## Metatables

### Object Oriented Programming 🙅🏻‍♀️
### Functional Programming 🙆‍♀️


## Frozen Tables
<TODO>
See the [table library](https://luau.org/library#table-library) for more information on frozen tables.

## Weak Tables
Luau is a managed language meaning it's objects are automatically "garbage collected" and it's memory freed when there are no longer any "strong references" to that object. In general, anytime you assign an object to a variable or table, it becomes a strong reference to that object. A "weak reference" is a reference to an object that does not prevent the object from being garbage collected. Weak references are only available as keys and values in Luau tables. To create a table with weak keys, set the `__mode` field of the metatable to `"k"`. To create a table with weak values, set the `__mode` field of the metatable to `"v"`. To create a table with weak keys and values, set the `__mode` field of the metatable to `"kv"`.

```
a = {}
b = {}
setmetatable(a, b)
b.__mode = "k"         -- table `a` has weak keys now
local key = {} 
a[key] = 1
key = {}               -- this replaces the only strong reference to the `{}` object created earlier, there is still a weak reference in the table
a[key] = 2

collectgarbage()       -- force a garbage collection cycle

-- this will only print 2, because the 1 key was garbage collected and the corresponding value gets removed from the table
for k, v in pairs(a) do 
    print(v) 
end
```

In the example above, the entry created with `a[key] = 1` gets removed when the only strong reference to the key object is removed. A similar thing happens with weak values.


## Native Code Generation
See [https://create.roblox.com/docs/luau/native-code-gen](https://create.roblox.com/docs/luau/native-code-gen)