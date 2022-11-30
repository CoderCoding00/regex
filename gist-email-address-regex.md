# Regex Tutorial to Search and Match a Username 
```md
As a web development student
I wanted to research and create a tutorial explaining a specific regex
So that I can better understand how to match an email address. 
```

## Summary
```md
Regex is short word for Regular Expressions. 
Regular expressions are a series of special characters that define a search patter. 
The search pattern I want to describe is `matching an email address` which can be done by the following series of characters. 
```

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

```md
This example is a uses literal notation, meaning the pattern must be wrapped in the slash character `/`. In this example, characters wrapped inside the slash characters checks to see if a string meets a required criteria for a username. The criteria is: 

* It can contain any lowercase letter between a-z. 
* Any number between 0-9
* An underscore
* A dot (period) `.`
* The length of the string after the final dot is between 2-6 characters. For example `.com `or `.ca` etc..

I will futher explain the components of a regex and how they work in the sections below.
```


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
  - [My Github](#my-github)

## Regex Components

### Anchors
* `^` is an anhcor to indicate a string being with the character that comes after `^`. A regex is case sensitive so if the letter following `^` is uppercase then it will match with that uppercase letter, but not the lowercase letter. For example, `W` would look for an exact string match and would find a string such as `We are going to the store` since the string starts with an uppercase `W`. However it would not find `we are going to the store` becasue it starts with a lowercase `w`. 
  
* `$` is an anchor that indicates a string that ends with the character(s) that came before it. 

In the example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` 
* Their are 3 main parts of this regex with an optional 4th part. The 3 main parts are sectioned off by the parenthesees `()`.

* 1st is the username. `([a-z0-9_\.-]+)` This can include any `lowercase letters a-z`, any `numbers 0-9`, an underscore `_` or a dash `-`. The `+` means it must be at least 1 character long, but can be more than that.

* 2nd is the domain `([\da-z\.-]+)`. This can include `lowercase letters, numbers, hyphens`.

* 3rd is the extension `([a-z\.]{2,6})` any lowercase letters between `a-z`.

* 4th is another possible extension. This is an optional extension but will always begin with a `.`
  * Between the main parts 1 and 2 is the symbol `@`. This is required between part 1 and part 2 which is the username and the domain. For example `john_doe@gmail` where `john_doe` is the `username` (1) `@` gmail is the `domain` (2). Here are those sections of the regex `([a-z0-9_\.-]+)@([\da-z\.-]+)`
  * Part 3 is the dot symbol `.` and has a backslash `\` before the period to make it a `literal` character, because the `.` by itself can have other meanings in a regex which I will describe later. The dot is followed by any `lowercase letters a-z` with the option of ending there, but if not it must be followed by another dot and domain name.
* The `{2, 6}` at the end is called a `Quatifier` which I will describe next. 
  
### Quantifiers
Quantifiers set the limit of the string, or section of the string, and idicate that a character must be matched a certain number of times. In the example `{3, 16}` this is setting the minimum and maximum amout of characters to a minimum of 3 and maximum of 16. 

* `*` Mathes the patern zero or more times of the preceeding character. 
* `?` Matches the pattern zero or one time.
* `+` Matches the pattern one or more times.
* `{}` Has 3 different possibilities to set the limits for matching. 
* `{ n }` Matches the pattern exactly `n` number of times, where `n` is any number entered.
* `{ n, }` Matches the pattern AT LEAST `n` number of times. 
* `{ n, x }` Matches the pattern to a minimum of `n` times, and a maximum of `x` times.

In the example `{2, 6}` the minimum is 2 and the maximum is 6. For an email this would be in the form of `.co.uk` which is the United Kingdom's way of ending an email address. Or `.com` which is the ending for email addresses in the US and elsewhere.

`Quatifiers can be considered  "greedy" or "lazy".`

* `Lazy` Meaning it will match as few occurrences as possible. This is done using the `?` symbol after the character.
* _By default_, quantifiers are `Greedy` and will match as many characters as possible. 

### Grouping Constructs
* You can group a section using `()` where each section with a parentheses is called a `subexpression`.
  
* When the regex is more complicated it's easier to check multiple parts of a string if you want to make sure subexpression meet different requirements. `Grouping Constuctors` delineate the subexpression of a regex and capture the substrings of an input string. In the email example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` the subexpression can be seen broken up as `/^` `([a-z0-9_\.-]+` `@` `([\da-z\.-]+)` `\.` `([a-z\.]{2,6})` `$/` where the parts in parenthesees are subexpression of grouping constuctors. 

### Bracket Expressions
* `[]` what is inside the `[]`represents a range of characters we want to include in the search. A `-` can be used between letters or numbers to represent a range. Or you can type in the range for the same results. 

* For example, `[xyz]` will look for a string that includes `x` or `y` or `z` and the length of the string doesn't matter. So `extra` would be a match `zebra` would be a match `yyy` would also be a match, and so on. 
This could also be accomplished using the `-` symbol. In this case you would type `[x-z]` to get the same results that `[xyz]` would result in. 
* In the email example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` the input inside the brackets means that _ANY_ of those characters are acceptable, not _ALL_ of them are required. The `()`surrounding those brackets makes the content of the brackets a requirement, while the input inside the brackets is required, not _ALL_ of the input is. _ANY_ of that input will work. For example `a` alone would work since it is part of the input inside the brackets. I'll explain the email example in more detail below. 

* `[a-z]` means the string can contain any `lowercase` letter between `a` and `z`. 
* `[0-9]` mmeans the string can contain any number between `0` and `9`.
* `_` `.`and `-` are special characters. Special characters are characters that is not a number or letter.
* In the example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, eveything inside the `[]` is an option, but not all of those characters are required. 

* The carrot `^` symbol is the beginning of the input, and the `$` is the end of the input. The `^` matches the starting position with the string, the `$` matches the ending position of the string, or in this case the characters of the email address. 

* In summary, the example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` can be looked at by each subexpression within the brackets. The brackets indicate that the regex does not need to meet _ALL_ the requirements becasue it is inside the `[]`. It only needs to meet _ANY_ of those requirements. The `+` at the end of the first subexpression `([a-z0-9_\.-]+)` means it _must be at least 1 character long_, but can be a great deal amount longer. So `a` would work since it is a lowecase letter and a lenght of 1. `a_a-b_bxyzz9` would also work because it has lowecase letters, special characters we allowed for, and a number; all of which are allowed in the regex `([a-z0-9_\.-]+)`. 

### Character Classes
A `character class` defines a set of characters that can occur in an input string and create a match. Bracket expressions are an example of a character class. 
More examples include:
* `\d` matches any Arabic numeral digit so it's effectively the same as `[0-9]`. So `\d` could be used in place of `0-9` and have the same effect. 
* `\w` matches any alphanummeric character and includes the underscore symbol `_`. It is effectively the same as `[A-Za-z0-9_]`
* `\s` matches a single whitespace character, tabs and line breaks.

### The OR Operator
* The `OR` operator is the symbol `|`, a character some people call a `pipe`. If we were to use the `grouping constructor` in `(abc)` we could change that to `(a|b|c)` which would now look for a string containing `a` or `b` or `c` rather than just `abc` as the only match. 


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

## Sources
* RegexMagic (https://www.regular-expressions.info/email.html)
* Javascript.Info (https://javascript.info/regular-expressions)
* Microsoft Learn (https://learn.microsoft.com/en-us/dotnet/standard/base-types/grouping-constructs-in-regular-expressions)
  
## My Github 
https://github.com/CoderCoding00
