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

//double quoted text does not need escaping
anotherString = "I'm not escaped" #=> "I'm not escaped"

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

**Arrays** - arrays are simple collections of items, that store values only.
```
array = [1,2,3,4,5] #=> [1,2,3,4,5]
# shorthand arr is also valid

//different types? Yes, please
array = [1,'hi',false] #=> [1,"hi",false]

//indexing arrays
array[0] #=> -1
array.first #=> -1
array[-1] #=> 5
array.last #=> 5
array[12] #=> nil

//with defined start index and length
array[2,3] #=> [3,4,5]

//reverse
a = [1,2,3]
a.reverse! #=> [3,2,1]
# also rev is an alias
a.rev! #=> [3,2,1]

//range
array[1..3] #=> [2,3,4]

//add to array
array << 6 #=> [1,2,3,4,5,6]
# or
array.push(6) #=> [1,2,3,4,5,6]

//remove from array
array.delete(6) #=> [1,2,3,4,5]

//check if item exists
array.include?(1) #=> true
# also
array.exists?(1) #=> true (*)
``` 

**Hashes** - hashes are classical associative arrays found in php, they store key-value pairs.
```
// Hashes

php people know how it goes, but instead of _array_ you should write _hash_

hash = {
'wow' => 'arrays',
'much' => 'assoc',
'so' => 'php',
'doge' => 🐶
}

hash.keys #=> ['wow','much','so','doge']

hash['wow'] #=> 'arrays',
hash['doge'] #=> 🐶

//non-existant value returns nil
hash['nope'] #=> nil

hash.key?('wow') #=> true
hash.value?('arrays') #=> true
```

## Logic
```
if true
  'if statement'
elsif false
  'else if, optional'
else
  'else, also optional'
end

//each loops ~ for loops

(1..5).each do |counter|
  puts "iteration #{counter}"
end

for counter in 1..5
  puts "iteration #{counter}"
end

//contents of data structures can also be iterated using each
array.each do |element|
  puts "#{element} is part of the array"
end
hash.each do |key, value|
  puts "#{key} is #{value}"
end

#ieach is an alias of each_with_index
array.ieach do |element, index|
  puts "#{element} is number #{index} in the array"
end

counter = 1
while counter <= 5 do
  puts "iteration #{counter}"
  counter += 1
end
#=> iteration 1
#=> iteration 2
#=> iteration 3
#=> iteration 4
#=> iteration 5

# a bunch of other helpful looping functions from ruby,
# for example "map", "reduce", "inject", the list goes on. Map,
# for instance, takes the array it's looping over, does something
# to it as defined in your loop, and returns an entirely new array.
array = [1,2,3,4,5]
doubled = array.map do |element|
  element * 2
end
puts doubled
#=> [2,4,6,8,10]
puts array
#=> [1,2,3,4,5]

grade = 'B'

case grade
when 'A'
  puts 'Way to go kiddo'
when 'B'
  puts 'Better luck next time'
when 'C'
  puts 'You can do better'
when 'D'
  puts 'Scraping through'
when 'F'
  puts 'You failed!'
else
  puts 'Alternative grading system, eh?'
end
#=> "Better luck next time"

# cases can also use ranges
grade = 82
case grade
when 90..100
  puts 'Hooray!'
when 80...90
  puts 'OK job'
else
  puts 'You failed!'
end
#=> "OK job"

# exception handling:
begin
  # code here that might raise an exception
  raise NoMemoryError, 'You ran out of memory.'
rescue NoMemoryError => exception_variable
  puts 'NoMemoryError was raised', exception_variable
rescue RuntimeError => other_exception_variable
  puts 'RuntimeError was raised now'
else
  puts 'This runs if no exceptions were thrown at all'
ensure
  puts 'This code always runs no matter what'
end

```

## Functions
```
# def is an alias of func which is an alias of function

func function1()
  puts 'Hi'
end
echo function1()

func function2(x,y = 1)
  result = x + y
  return result
end
echo function2(4) #=> 5
echo function2(4,2) #=> 6

# result is not accessible outside the function
# print result # Gives a warning.

inc = func(x)
  return x + 1
end

echo inc(2) #=> 3

// functions can return functions
func bar (x, y)
    // Use 'use' to bring in outside variables
    return function (z) use (x, y)
        foo(x, y, z);
    end
end

bar = bar('A', 'B')
bar('C') # Prints "A - B - C"

// you can call named functions using strings
function_name = 'add';
echo function_name(1, 2) #=> 3
// useful for programatically determining which function to run
```

## Modules
```
//you can embed modules or use them separately, they have a `.ppm` extension

Module mod1(x)
  @intro = "it's time for greetings:"
  func sayhi(x)
    return 'hi, #{x}'
  end
  return @intro + sayhi(x)
end

//result
mod1("Waffle")
"it's time for greetings:"
"hi, Waffle"

//from somewhere else
use mod1
mod1("Ginger")

//to call a function
use mod2
mod2.echo("Walter")
#=> "Walter"

//to use just that function
use mod2.echo
# now you can use it
echo("Penny")
#=> "Penny"
```

## Includes
```
<?pp
// pphp code within included files must also begin with a pp open tag

include 'my-file.pp';
// The code in my-file.pp is now available in the current scope.
// If the file cannot be included (e.g. file not found), a warning is emitted.

include_once 'my-file.pp';
// If the code in my-file.pp has been included elsewhere, it will
// not be included again. This prevents multiple class declaration errors

require 'my-file.pp';
require_once 'my-file.pp';
// Same as include(), except require() will cause a fatal error if the
// file cannot be included.

// Contents of my-include.pp:
<?pp

return 'Anything you like.';
// End file

// Includes and requires may also return a value.
value = include 'my-include.pp';

// Files are included based on the file path given or, if none is given,
// the include_path configuration directive. If the file isn't found in
// the include_path, include will finally check in the calling script's
// own directory and the current working directory before failing.
/* */

```

## Magic constants
```
// Get current module name. Must be used inside a module declaration.
echo "Current class name is " . __MODULE__;

// Get full path directory of a file
echo "Current directory is " . __DIR__;

    // Typical usage
    require __DIR__ . '/modules/init.pp';

// Get full path of a file
echo "Current file path is " . __FILE__;

// Get current function name
echo "Current function name is " . __FUNCTION__;

// Get current line number
echo "Current line number is " . __LINE__;

```
