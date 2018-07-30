# pphp syntax (rev. 1)

Heads up: all the code sections are represented by code blocks
```
Like this one
```

fate of the sections marked with `(*)` should be decided separately

## ToC

* [Initial structure](#initial-structure)
* [Types, Variables and constants](#types-variables-and-constants)
* [Output](#output)
* [Arrays](#arrays)
* [Logic](#logic)
* [Functions](#functions)
* [Modules](#modules)
* [Includes](#includes)
* [Magic constants](#magic-constants)

## Initial script structure

***pphp*** scripts, similar to php, come with their own tags `<?pp ?>` that denote the beginning and end of the script. For non-embedded *pphp* code the closing tag must be ommited.

```
<?pp

// Get some code here
# Oh look, an alternative comment notation
/*
  And here's a multi-line comment
*/
```

## Types & Variables
```
// variables
x = 'variable'
y = 2
y #=> 2

// you can also do multiple assignment on them
y = x = 2
y #=> 2
x #=> 2

// you can declare them as good 'ol php ones (*)
$x = 2
$x #=> 2

// you can unset the variable like this (*)
x = 2

x = nil
x.unset
x.nil

// variables starting with $$ are global
$$z = "global variable, everyone"
defined? $$z #=> "global variable"

// variables starting with @ have module scope
@z = "i'm only valid in the module"
defined? @z #=> "module variable"

// variable starting with ~ are constants (*)
~w = "I'm a constant"
defined? ~w #=> "constant"

// integers
x = 25 #=> 25
x = -12 #=> -12
x = 025 #=> 25
x = 0x0F #=> 15 (0x marks a hex literal)
x = b11111111 #=> 255 (b marks a binary number)

// floats
y = 1.234
y = 1.4e5
y = 7E-10

// some math
1 + 1 #=> 2
8 - 1 #=> 7
10 * 2 #=> 20
35 / 5 #=> 7
2 ** 5 #=> 32
5 % 3 #=> 2

//shorthands
num = 0
num += 1 //increment by 1
echo num++ //#=> 1
echo ++num //#=> 3
num /= float //divide and assign the quotient to num

// Bitwise operators
3 & 5 #=> 1
3 | 5 #=> 7
3 ^ 5 #=> 6

//naming
//good naming
RootPath = '/tmp/root'
PathToProjectRoot = '/tmp/root'
root_path = '/tmp/root'

//bad naming
w = '/tmp/root'
👌🤣 = 'SecurePassword10201ASD0129"

// Strings

string = 'i\'m a string'
anotherString = 'now i\'m a string with #{val}'
anotherString = 'now i\'m a string with {$val}' //also true
anotherString = 'now i\'m a string with ${val}' //also true (*)
anotherString = 'now i\'m a string with $${val}' //also true (*)

//heredocs are a thing for multiline strings

multiline = <<<HereDOC
totally multi line
string
here
HereDOC

//concats 
concat = 'hi ' + 'there' #=> "hi there"
concat = 'hi ' + 5 #=> TypeError: can't convert Fixnum into String, whoops careful here, strings only
concat = 'hi ' + 5.to_s #=> "hi 5"
concat = 'hi #{5}'

//combine string and operators
'hi ' * 5 #=> "hi hi hi hi hi "

//append to string
'hi' << ' there' #=> "hi there"
'hi' >> ' there' #=> " there hi" (*)


```

## Output

`echo` is an alias of `puts` that prints to the output with a new line, while `print` is used to print to the output __without__ a new line

```
<?pp
  # you can use both single and double quotes for strings
  echo "hi there"
  print "_nice to meet you"
  puts 'hi there'
```
**Result:**
```
hi there_nice to meet you
hi there
```

## Arrays
WIP 

## Logic
WIP

## Functions
WIP

## Modules
WIP

## Modules
WIP

##Includes
WIP

## Magic constants
WIP
