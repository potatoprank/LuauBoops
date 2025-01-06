
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

Using global variables us discouraged by 9/10 software engineers so instead please avoid globals as much as possible!!

Local variables are variables that are scoped to the block or chunk in which they are declared. Local variables shadow any globals or locals in the parent scope. Local variables are declared with the `local` keyword. If you'd like to create a scope (block) for your local variables, you can use the `do` control expression

```
do
    local myLocalVariable = "I am a local variable"
    print(myLocalVariable)
    -- prints 
end
print(myLocalVariable) -- prints nil
```

All variables in Luau are typed either implicitly on explicitly. We'll go into this more in the typing section.

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

The `nil` _type_ can also take the _value_ `nil`. The `nil` _value_ can still be the type of all other types (except the `never` type). The nil type is special and is also rarely useful. Don't worry too much about it. 

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
local c: string | number = unknown() -- not ok
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

## thread types

The `thread` type are used to represent a coroutine. These can be manipulated with the builtin [coroutine library](https://www.lua.org/pil/9.html). The Programming in Lua book has a [good section](https://www.lua.org/pil/9.html) on coroutines if you are interested in learning more about them.

```
If you are working in Roblox, coroutines are often managed by the [task library](https://create.roblox.com/docs/reference/engine/libraries/task). These methods create coroutines that are managed by the Roblox engine's TaskSchedule such that should not (ever) manually `coroutine.yield` and `coroutine.resume` them.
```

## userdata types

Luau is intended for use as an embedded language. That's why if you've ever read the Lua manual you'll notice that the majority is dedicated to the [C API for embedding Lua](https://www.lua.org/manual/5.1/manual.html#3) in your program <sub>(yes, I linked the 5.1 Lua manual... we still need to write one for Luau...)</sub>

In order for Luau to be useful as an embedded language, it must be able to interact with the data types in the program it is embedded in. Examples of Roblox data types are things like `Instance` and `Player`. These data types are called "userdata" types. These are not to be confused with table types which can have new items added and removed. Userdata types have static definitions. 


```
Instance myInstance = workspace.FindFirstChild("bearModel")
myInstance.Name = "bear" -- `Name` is a property of the `Instance` datatype so this is valid
myInstance.location = "Canada" -- `location` is not a property of myInstance, this is not valid!
```

Roblox data types are all documented on the very useful [Roblox Creator Docs](https://create.roblox.com/docs/reference/engine) site.

## typecasting

You can force a value to be a certain type with the `::` symbol. This is called typecasting. You can only typecast if the value type shares a subtype with the type being casted too. Luau can not verify that the typecast will be valid during runtime. For this reason avoid typecasting as much as possible.

```
local a : string | number = 1
local b : number = a -- not ok
local c : number = a :: number -- ok
local d : string = x :: string -- ok, but d will not actually be a string
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

Tables are the heart and soul of Luau

tables aret he be all end all data structure in Lua. Tables are still just as iportant in Luau although we added `vector` and `buffer` types )

## As Arrays
## As Objects
## Metatables
### Object Oriented Programming 🙅🏻‍♀️
### Functional Programming 🙆‍♀️
## new Luau stuff (maybe move to advanced section)


# Functions
## Closures



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

## Vector
## Buffer
## Thread

# New Luau Features!
<TODO>





# Luau Tooling
<TODO>


# Roblox UI in Luau
## native
## Fusion
## React





# Advanced Topics

## Metatables




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
