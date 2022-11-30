# Regex Tutorial to Search and Match a Username 
```md
As a web development student
I wanted to research and create a tutorial explaining a specific regex
So that I can better understand the search pattern to check and validate username. 
```

## Summary
```md
Regex is short word for Regular Expressions. Regular expressions are a series of special characters that define a search patter. The search pattern I want to describe is matching a username which can be done by the following series of characters. 
```

`/^[a-z0-9_-]{3,16}$/`

```md
This example is a uses literal notation, meaning the pattern must be wrapped in the slash character `/`. In this example, characters wrapped inside the slash characters checks to see if a string meets a required criteria for a username. The criteria is: 

* A string can contain any lowercase letter between a-z. 
* Any number between 0-9
* An underscore or hyphen
* The length of the string is between 3-16 characters. 

I will futher explain the components of a regex and how they work in the sections below.
```
> **Note**: Javascript provides two ways to create a regex object. Mine usees literal notation indicated by enclosing the characters in the `/` character. The second way is by using a RegEx constructor which encloses the characters in `?` instead. 

## Table of Contents

- [Regex Tutorial to Search and Match a Username](#regex-tutorial-to-search-and-match-a-username)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [Grouping Constructs](#grouping-constructs)
    - [Bracket Expressions](#bracket-expressions)
    - [Character Classes](#character-classes)
    - [The OR Operator](#the-or-operator)
    - [Flags](#flags)
    - [Character Escapes](#character-escapes)
  - [Author](#author)
    - [Sources](#sources)

## Regex Components

### Anchors
* `^` is an anhcor to indicate a string being with the character that comes after `^`. A regex is case sensitive so if the letter following `^` is uppercase then it will match with that uppercase letter, but not the lowercase letter. For example, `W` would look for an exact string match and would find a string such as `We are going to the store` since the string starts with an uppercase `W`. However it would not find `we are going to the store` becasue it starts with a lowercase `w`. 
  
* `$` is an anchor that indicates a string that ends with the character(s) that came before it. 

In the example `/^[a-z0-9_-]$/` the string must start and end with something matching that pattern. However in the example `/^[a-z0-9_-]{3,16}$/` the `{3, 16}` is called a `Quatifier` which I will describe next. 
  
### Quantifiers
Quantifiers set the limit of the string, or section of the string, and idicate that a character must be matched a certain number of times. In the example `{3, 16}` this is setting the minimum and maximum amout of characters to a minimum of 3 and maximum of 16. 

* `*` Mathes the patern zero or more times of the preceeding character. 
* `?` Matches the pattern zero or one time.
* `+` Matches the pattern one or more times.
* `{}` Has 3 different possibilities to set the limits for matching. 
* `{ n }` Matches the pattern exactly `n` number of times, where `n` is any number entered.
* `{ n, }` Matches the pattern AT LEAST `n` number of times. 
* `{ n, x }` Matches the pattern to a minimum of `n` times, and a maximum of `x` times.

In the example `{3, 16}` the minimum is 3 and the maximum is 16. 

`Quatifiers can be considered  "greedy" or "lazy".`

* `Lazy` Meaning it will match as few occurrences as possible. This is done using the `?` symbol after the character.
* `Greedy` By default, quantifiers are `Greedy` and will match as many characters as possible. 

### Grouping Constructs
* Some regular expression are more complicated than the example I am using. When the regex is more complicated it is easier to check multiple parts of a string if you want to make sure different sections meet different requirements. That is what `grouping constuctors` are used for, to break sections up.
* You can group a section using `()` where each section with a parentheses is called a `subexpression`.
* `(abc)` is looking for a part of the string that matches `abc` exactly. In otherwords, `cba` would not match. 

### Bracket Expressions
* `[]` what is inside the `[]`represents a range of characters we want to include in the search. A `-` can be used between letters or numbers to represent a range. Or you can type in the range for the same results. 

* For example, `[xyz]` will look for a string that includes `x` or `y` or `z` and the lenght of the string doesn't matter. So `extra` would be a match `zebra` would be a match `yyy` would also be a match, and so on. 
This could also be accomplished using the `-` symbol. In this case you would type `[x-z]` to get the same results that `[xyz]` would result in. 

* `[a-z]` means the string can contain any `lowercase` letter between `a` and `z`. 
* `[0-9]` mmeans the string can contain any number between `0` and `9`.
* `_` and `-` are special characters. Special characters  are characters that is not a number or letter. In the example used in this tutorial, `/^[a-z0-9_-]{3,16}$/`, we are including the special characters `_` and `-` by adding them after the number `9` as shown. Alone it would look like `[_-]`to include both the underscore and hyphen symbol. 
* A `bracket expression` can be turned into a `negative character group` by adding the `^` symbol at the beginning of the expression inside the brackets. This would be done to `exclude` characters in the search. A common example is if you wanted to exclude all vowels, both upper and lower case. This would be done by `[aeiouAEIOU]`. 

* In the example to match a username `/^[a-z0-9_-]{3,16}$/` this would look for a stirng between`3` and `16` characters that begins and ends with any combination of lowercase characters, numbers between `0` and `9`, and the special characters `_` and `-`. It does not need to meet all the requirements becasue it is inside the `[]`. It only needs to meet any of those requirements. So `aaa` would work since it is a lowecase letter and a lenght of 3. `a_a-b_bxyzzzzzzz` would also work because it has lowecase letters and the special characters we allowed for, and has a length of 16. 

### Character Classes
A `character class` defines a set of characters that can occur in an input string and create a match. Bracket expressions are an example of a character class. 
More examples include:
* `\d` matches any Arabic numeral digit so it's effectively the same as `[0-9]` 
* `\w` matches any alphanummeric character and includes the underscore symbol `_`. It is effectively the same as `[A-Za-z0-9_]`
* `\s` matches a single whitespace character, tabs and line breaks.

### The OR Operator
* The `OR` operator is the symbol `|`, a character some people call a `pipe`. If we were to use the `grouping constructor` example from above `(abc)` we could change that to `(a|b|c)` which would now look for a string containing `a` or `b` or `c` rather than just `abc` as the only match.
* This is more commonly used when you have more complicated searches and is often used with the `grouping constructor` and a `:` between `grouping constructors`. 
* For example, `(abc)!(xyz)` would be a match for `abc!xyz` but not `cba!zyx`. Whereas `(a|b|c)!(x|y|z)` would match with `abc!xyz` of course, but would also match with `cba!zyx` or `a!z`. But it would not match with `xyz!abc` because the order is not correct since there are 2 `grouping constructors` separated by a `!`.

### Flags
A flag are placed at the end of a regex after the 2nd slash. Their purpose is to define limits or additonal functionality of the regex. There are 6 flags that can be used individually or together.

* `i` makes the search NOT case sensitive. Meaning a or A will match.
* `g` looks for all matches, without it only the first match is returned.  
* `m` this is multiline mode and effects the behavior of `^` and `$` where they match at the beginnig and the end of the string, but also at the start/end of the line. 
* `s` enables the `dotall` mode that allows a dot `.` to match newline character `\n`
* `u` enables full unicode support. This flag enables correct processing of surogate pairs. 
* `y` enables sticky mode which is searching at the exact position in the text. 

### Character Escapes
Character escapes is a character that invokes an alternative interpretation on the following characters in a character sequence. They are a common way of looking for special characters in a string. 

* The `\` is a character escape.
* If you wanted to find a dot. You could use `\.`
* `\{` means the regex should look for the open curly brace character. 
  
  
## Author
Drum Holliday

I'm currently a student at the UC Irvine Fullstack Coding Bootcamp 

### Sources
* RegexBuddy (https://www.regular-expressions.info/backref.html)
* Link given in class via resources in slack (https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial)
* Javascript.Info (https://javascript.info/regular-expressions)

My Github [github] https://github.com/CoderCoding00
