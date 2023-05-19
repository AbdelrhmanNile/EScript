# Expert System Script
EScript is a simple language for writing expert systems. It has a simple syntax and is easy to learn. EScript is written in Python and compiled to C for speed.

## Syntax
EScripts can be divided into three parts: concepts, blocks, and rules. Concepts are the basic building blocks of an EScript. They are used to represent the data that the expert system will use. Blocks are used to group rules together.

### Concepts
To define a concept use the `cpt` keyword followed by the name of the concept, then the datatype of this concept or the string values options this concept can take seperated by `/`.<br />

Example:<br />
We want to define a concept named color that can take the values red, green, and blue. We would write the following:<br />
```
cpt color red/green/blue
```
let's define a concept named `is_alive` which is of type `boolean`:
```
cpt is_alive bool
```
now let's define a concept named `age` which can take any number value:
```
cpt age num
```
note: all numbers are trated as floats in EScript.

To sum up, the syntax of a concept is:
```
cpt <concept_name> {<datatype> | <value1>/<value2>/.../<valueN>}
```

### Rules
Rules are the building blocks for Blocks.
rules are written in the following format:
```
if <condition> then <concept>
```

#### Operations
the following operations are supported:
* `and` - logical and
* `or` - logical or
* `gt` - greater than
* `lt` - less than
* `eq` - equal to

#### Conditions
conditions are written in the following format:
```
<concept> <operation> <value>
```
example:
if we want to define a rule that says that if the color is red and the age is greater than 18 and is alive, then the person is an adult, we would write:
```
if (color eq red) and (age gt 18) and (isAlive eq true) then isAdult
```
note that the parentheses are used to define the order of operations.

isAdult is a boolean concept, so we can use it in other rules.


### Blocks
Blocks are used to group rules together, these rules must be representing the same problem, for example if we are writting an expert system that does medical diagnosis, we can have a block for each disease, and each block will contain the rules that represent the symptoms of this disease.

To define a block just you only nned to give it a name followed by the `:`, then you can write the rules of this block, each rule must be written in a new line, and when you are done writing the rules of this block you can end it with a `;` in a new line.

note: each block must have a unique name and at least one rule.

each block will be evaluated sperately, and any concept that is yielded by any rule inside a block will be local to this block, and can't be used in other blocks.

after all the blocks are evaluated, they will be ranked based on the number of rules that were evaluated to true.

Example:
```
cpt color red/green/blue
cpt isAlive bool
cpt age num

adult:
if (color eq red) and (age gt 18) and (isAlive eq true) then isAdult
;
```

## Compiling 
EScript interpreter is written in Python and compiled to C for speed. To compile use nuitka:
```
nuitka3 --standalone escript.py
```