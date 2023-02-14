# language-mambascript README

This is the README for extension "language-mambascript"

## Features

Adds syntax highlighting and snippets to MambaScript files in VSCODE.

# Basic MambaScript

## Values and Variables

Values can have different datatypes and their are 6 basic types in MambaScript

### Numbers
Numbers are written the way numbers are usually written
```coffee
144
```
### Strings
Strings are used for storing and manipulating text. A String in MambaScript is
zero or more characters written inside of quotes.

```coffee
goat = 'Kobe Bryant'
```

You can use either single or double quotes:

```coffee
carName1 = 'Mercedes Benz S550'
carName2 = "Tesla Model S"
```

You can also create multiline strings with either triple single quotes, or triple
double quotes.

```coffee
theRaven = '''
    Once upon a midnight dreary while I pondered, weak and weary,
    Over many quaint and curious volume of forgotten lore -
    While I nodded, nearly napping, suddenly there came a tapping,
    As of some one gently rapping, rapping at my chamber door
    "'Tis some visiter". I muttered, "tapping at my chamber door" -
    "only this and nothing more."

    Ah distinctly I remember it was in the bleak December;
    And each separate dying ember wrought its ghost upon the floor.
    Eagerly I wished the morrow - vainly I had sought to borrow,
    From my books surcease of sorrow - sorrow For the lost Lenore -
    For the rare and radiant maiden whom the angels name Lenore -
    Nameless here For evermore
'''

hamlet = """
    To be or not to be, that is the question
    Whether tis Nobler in the mind to suffer
    The Slings and Arrows of outrageous Fortune,
    Or to take Arms against a Sea of troubles,
    And By opposing end them, to die, to sleep
    No more. and By a sleep, to say we end
    The heart-ache and the thousand Natural shocks
    That Flesh is heir to?
"""
```

### Booleans
A MambaScript Boolean represents one of two types of values: `truthy and falsey`

Truthy values are values that the MambaScript compiler considers `true` and are of
the type Boolean. `yes, on and true`

Falsey values are values that the MambaScript compiler considers `false` and are of
the type Boolean. `no, off and false`

```coffee
present '------- is  and Booleans --------'
present 'Truthy Booleans true, on, yes'
present 'Falsey Booleans false, off, no'
present true is on
present true is yes
present false is off
present false is no
```

### Objects

Objects in MambaScript are a way to store data that in an individual container

```coffee
obj =  {
  "MambaScript": "JavaScript"
  "is": "==="
  "isnt":	"!=="
  "not":	"!"
  "and also":	"&&"
  "or":	"||"
  "true yes on":	"true"
  "false no off":	"false"
  "@ this": 	"this"
  "of": "in"
  "in": "no JS Equivalent"
}
```

### Functions
Functions are one of the fundamental building blocks in MambaScript. A function in MambaScript is similar to a procedure—a set of statements that performs a task or calculates a value, but for a procedure to qualify as a function, it should take some input and return an output where there is some obvious relationship between the input and the output. To use a function, you must define it somewhere in the scope from which you wish to call it.
```coffee
# eat is a function that accepts a string and returns nothing
eat :: String -> () = (food :: String ) ->
  present "yum #{food.toUpperCase()} !!!"

eat food forEvery food in ['toast', 'cheese', 'wine']

eat food forEvery food in  ['toast', 'cheese', 'wine'] when food isnt 'cheese'
```
### Undefined and Null Values
```coffee
a :: Int?
a = 1
a = null

b :: Int = 1
# b = a # can't assign nullable to non-nullable
a = b

listWithNull :: Int?[] = [1, 2, 3, null, 5]
listMaybeNull :: Int?[]? = null
listMaybeNull = listWithNull

intByConditional :: Int =
  if Math.random() > 0.5
    1
  else
    2

# can't be Int
nullableIntByConditional :: Int? =
  if Math.random() > 0.5
    1

intBySwitch :: Int =
  switch ~~(Math.random()* 10)
    when 1
      1
    when 2
      2
    else
      3

# can't be Int
nullableIntBySwitch :: Int? =
  switch ~~(Math.random()* 10)
    when 1
      1
    when 2
      2
```

## Control Flow
```coffee
isCool = true

# traditional if else
if isCool
  present 'You are cool'
else
  present 'You are lame'

# ternary in MambaScript
if isCool then present 'You are cool' else 'You are lame'

# Unless is the opposite of if or the equivalent if !isCool
unless isCool
  present 'You are lame'
else
  present 'You are cool'

# ternary with unless
unless isCool then present 'You are lame' else present 'You are cool'

# loops with when clause and function

foods :: String[] = ['lettuce', 'filet mignon', 'steak', 'burger', 'pork chop']
# function named printFood
# It accepts a String and returns nothing 
printFood :: String -> () = (food :: String ) -> present food

printFood food forEvery food in foods when food isnt 'lettuce'
```

## What is a pessimistic type interface?

To pass the dynamic type system, MambaScript expects symbol to be `implicit` node by default. If compiler compares implicit node type and implicit node type fails, it recovers to `implicit` `Any` automatically.

## Examples

### Assigment with type

```coffee
n :: Int = 3
```

### Pre defined symbol

```coffee
x :: Number
x = 3.14
```

### Nullable

```coffee
x :: Number?
x = 3.14
x = null
```

### Typed Array

```coffee
list :: Int[] = [1..10]
listWithNull :: Int?[] = [1, null, 3]
```

In `v0.10`, imperfect to struct.

### Struct

```coffee
struct Point
  @name :: String
  x :: Number
  y :: Number
p :: Point = {x: 3, y: 3}
name :: String = Point.name

struct Point3d implements Point
  z :: Number
```

### Module

MambaScript has module system like TypeScript

```coffee
module A.B
	class @C
		a :: Int
abc :: A.B.C = new A.B.C
```

### Typed Function

```coffee
# pre define
f1 :: Int -> Int
f1 = (n) -> n

# annotation
f2 :: Number -> Point = (n) -> x: n, y: n * 2

# multi arguments
f3 :: (Int, Int) -> Int = (m, n) -> m * n

# another form of arguments
f4 :: Int * Int -> Int = (m, n) -> m * n

# partial applying
fc :: Int -> Int -> Int
fc = (m) -> (n) -> m * n
```

### Blueprint instead of class with this scope

```coffee
blueprint X
  # bound to this
  num :: Number
  f   :: Number -> Number

  f: (n) ->
    @num = n

x :: X = new X
n :: Number = x.f 3
```

### Blueprint with implements

```coffee
blueprint Point
  x :: Int
  y :: Int

struct Size
  width  :: Int
  height :: Int

blueprint Entity inheritsFrom Point implements Size
e :: {x :: Int, width :: Int} = new Entity
```

### Generics and type arguments

```coffee
# struct
struct Value<T, U>
	value :: U
struct Id<A, B>
	id :: Value<A, B>
obj :: Id<Int, String> =
  id:
    value: 'value'

# function type arguments
map<T, U> :: T[] * (T -> U) -> U[]
map = (list, fn) ->
  for i in list
    fn(i)
list :: String[] = map<Int, String> [1..10], (n) -> 'i'

# blueprint type arguments
blueprint Blueprint<A>
  f :: Int -> Int
  constructor :: A -> ()
  constructor: (a) ->
c = new Blueprint<Int>(1)
```