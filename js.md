# Intro to JS

## vars
variables must be declared through **let** or **const**  
**var** is the old convention, preferably don't use  

## vartypes
8 diff types
### number
numerical value, can be operated mathematically

### string
sequence of characters

### boolean
in js, equals True or False

### object
tba

### symbol
tba

### bigInt
numerical value grater than the perceived range of a **number** type

### null
input value of "nothing"

### undefined
uninputed value of "nothing"

## type conversions
3 types

### numerical
any type into number
#### a string of numbers
becomes the numerical value of the string
```
Number("123") = 123
```
Empty spaces get ignored  
non numerical characters in the string will result in returning a NaN (not a number)  

#### others
a boolean returns 0 for false and 1 for true  
a null returns 0  
undefined returns NaN

### string
a non string variable's value can be turned into a string
```
String(123) = "123"
String(True) = "True"
String(undefined) = "undefined"
etc
```

### boolean
a var can be turned into a boolean  
#### returns true
value < 0 < value
"[anything]"

#### returns false
undefined
null
0
"[empty]"
