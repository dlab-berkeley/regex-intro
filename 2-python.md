## Regular Expressions in Practice: Python

The module for using regular expressions in Python is `re`. It is part of the Python standard library, so you don't have to install 
anything. To be able to use the module, import it first. Also import the csv module, since we'll be reading in a csv file. Then
let's read in the leader data file we just converted from .txt to .csv:

~~~ {.input}
>>> import re
>>> import csv

>>> with open('/Users/natalieahn/Documents/D-Lab/example_data_leaders.csv', 'rU') as f:
...     reader = csv.reader(f)
...     data = [row for row in reader]

~~~

The `re` module contains several functions to enable us to match strings by regular expressions, find and replace instances
of a pattern, etc. Let's start with the function `match()`. It takes two arguments: the regular expression pattern to match,
then the string that we want to match to that pattern.

Let's say that we want to find any position in a leader's prior experience that involved military or police service. We'll use
a simple for loop to iterate through the rows in our data, look at the cell for prior experience, and print it out if it matches
the regular expression for military or police. (To keep this very simple, we're just looking at the last cell in each row.)

~~~ {.input}
>>> for row in data:
...     if re.match('military|police', row[-1]): print(row[-1])

~~~
~~~ {.output}
military officer
military colonel
~~~

Why did we only get the military positions, but we have a police position in there too? If you recall, the police
position was "head of police". The function `match()` only matches from the beginning of the given string. To find
a sequence anywhere within the given string, we can use the function `search()`, with the same arguments:

~~~ {.input}
>>> for row in data:
...     if re.search('military|police', row[-1]): print(row[-1])

~~~
~~~ {.output}
military officer
military colonel
head of police, college instructor, mayor
~~~

Great, we found all three. But the third result printed out the leader's entire list of positions, and we might only want
to look at the position that had "police" in it. Let's capture the specific position in a group and just print out that
group. We want to make sure we capture the full position, not just the word "military" or "police". So we want to get all of
the characters before and after "military" or "police" that are not a comma.

The functions `match()` and `search()` return a regex match object, that contains information about what matching sequence
was found in the given string. If there is no match, the function returns the value None, which is why we were able to treat
it like a logical value in the examples above. (We used an `if` statement to say that if there was any match found, we
wanted to print out the whole string.) Now we want to assign the function's output to a variable, so that we can retrieve
certain components from it.

Notice that we've created nested groups, because we need the inner parentheses to make sure the OR operator only applies
to "military" or "police", but we want both the preceding characters and succeeding characters in either case. When we
use nested groups, they are numbered with the outter one first, so we can use the method `.group(1)` to get the sequence
that matched everything inside the outter parentheses. (Python's regex module also allows you to name the groups, for
greater clarity, which you can look into on your own.)

~~~ {.input}
>>> for row in data:
...     match = re.search('([^,]*(military|police)[^,]*)', row[-1])
...     if match:
...         print(match.group(1))

~~~
~~~ {.output}
military officer
military colonel
head of police
~~~
