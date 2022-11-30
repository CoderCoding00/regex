# Regex Tutorial to Match an Email Address
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
The criteria for matching an email address is: 

* It can contain any lowercase letter between a-z. 
* Any number between 0-9
* It can contain an underscore `_`, a dash `-`, and a dot `.`
* The length of the string after the final dot is between 2-6 characters. For example `.com `or `.co.uk` etc..

I will futher explain the components of a regex and how they work in the sections below.
```


## Table of Contents

- [Regex Tutorial to Match an Email Address](#regex-tutorial-to-match-an-email-address)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [Grouping Constructs](#grouping-constructs)
    - [Bracket Expressions](#bracket-expressions)
    - [Character Classes](#character-classes)
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

* Their are 3 main parts of this regex with an optional 4th part.

* 1st is the username. `([a-z0-9_\.-]+)` This can include any `lowercase letters a-z`, any `numbers 0-9`, an underscore `_` or a dash `-`. The `+` at the end means it must be _at least_ 1 character long, but can be more than that.

* 2nd is the domain `([\da-z\.-]+)`. This can include `lowercase letters, numbers, hyphens`.

* 3rd is the extension `([a-z\.]{2,6})` any lowercase letters between `a-z`.

* 4th is another possible extension. This is an optional extension but will always begin with a `.`
  * Between the main parts 1 and 2 is the symbol `@`. This is required between part 1 and part 2 which is the username and the domain. For example `john_doe@gmail` where `john_doe` is the `username` `@` gmail which is the `domain`. Here are those sections of the regex `([a-z0-9_\.-]+)@([\da-z\.-]+)`
  * Part 3 is the dot symbol `.` and has a backslash `\` before the period to make it a `literal` character, because the `.` by itself can have other meanings in a regex which I will describe later. The dot is followed by any `lowercase letters a-z` with the option of ending there, but if not it must be followed by another dot and domain name.
* The `{2, 6}` at the end is called a `Quatifier` which I will describe next. 
  
### Quantifiers
Quantifiers set the limit of the string, or section of the string, and idicate that a character must be matched a certain number of times. In the example `{2, 6}` this is setting the minimum and maximum amout of characters to a minimum of 2 and maximum of 6. I don't use all of the following quatifiers but I will describe what each one does as they could be used.

* `*` Mathes the patern zero or more times of the preceeding character. This was not used in the example.
* `?` Matches the pattern zero or one time. This was not used in the example.
* `+` Matches the pattern one or more times. This was used to at the end of the username and domain. 
* `{}` Has different possibilities to set the limits for matching. 
* `{ n, x }` Matches the pattern to a minimum of `n` times, and a maximum of `x` times.

In the example `{2, 6}` the minimum is 2 and the maximum is 6. For an email this would be in the form of `.co.uk` which is the United Kingdom's way of ending an email address. Or `.com` which is the ending for email addresses in the US and elsewhere. The ending could be .ca for california. That's why a minimum of 2 is needed. I can't think of a 6 digit ending but I'm sure there are some.

`Quatifiers can be considered  "greedy" or "lazy".`

* `Lazy` Meaning it will match as few occurrences as possible. This is done using the `?` symbol after the character.
* _By default_, quantifiers are `Greedy` and will match as many characters as possible. 

### Grouping Constructs
* You can group a section using `()` where each section with a parentheses is called a `subexpression`.
  
* When the regex is more complicated it's easier to check multiple parts of a string if you want to make sure subexpression meet different requirements. `Grouping Constuctors` delineate the subexpression of a regex and capture the substrings of an input string. In the email example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` the subexpression can be seen broken up as `/^` `([a-z0-9_\.-]+` `@` `([\da-z\.-]+)` `\.` `([a-z\.]{2,6})` `$/` where the parts in parenthesees are subexpression of grouping constuctors. 

### Bracket Expressions
* `[]` what is inside the `[]`represents a range of characters we want to include in the search. A `-` can be used between letters or numbers to represent a range. Or you can type in the range for the same results. 

* For example, `[xyz]` will look for a string that includes `x` or `y` or `z` and the length of the string doesn't matter. So `extra` would be a match, `zebra` would be a match, `yyy` would also be a match, and so on. 
This could also be accomplished using the `-` symbol. In this case you would type `[x-z]` to get the same results that `[xyz]` would result in. 
* In the email example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` the input inside the brackets means that _ANY_ of those characters are acceptable, not _ALL_ of them are required. The `()`surrounding those brackets makes the content of the brackets a requirement, while the input inside the brackets is required, not _ALL_ of the input is. _ANY_ of that input will work. For example `a` alone would work since it's part of the input inside the brackets. I'll explain the email example in more detail below. 

* `[a-z]` means the string can contain any `lowercase` letter between `a` and `z`. 
* `[0-9]` mmeans the string can contain any number between `0` and `9`.
* `_` `.`and `-` are special characters. Special characters are characters that is not a number or letter.
* Since a `.` alone in a regex can have its own meaning, to get an actual dot we need to use `\.` to get the dot character.
* In the example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, eveything inside the `[]` is an option, but not all of those characters are required. 

* The carrot `^` symbol is the beginning of the input, and the `$` is the end of the input. The `^` matches the starting position with the string, the `$` matches the ending position of the string, in this case the characters of the email address. 

* In summary, the example `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/` can be looked at by each subexpression within the brackets. The brackets indicate that the regex does not need to meet _ALL_ the requirements becasue it is inside the `[]`. It only needs to meet _ANY_ of those requirements. The `+` at the end of the first subexpression `([a-z0-9_\.-]+)` means it _must be at least 1 character long_, but can be a great deal amount longer. So `a` would work since it is a lowecase letter and a lenght of 1. `a_a-b_bxyzz9` would also work because it has lowecase letters, special characters we allowed for, and a number; all of which are allowed in the regex `([a-z0-9_\.-]+)`. 

### Character Classes
A `character class` defines a set of characters that can occur in an input string and create a match. Bracket expressions are an example of a character class. 

Another example include:
* `\d` matches any Arabic numeral digit so it's effectively the same as `[0-9]`. So `\d` could be used in place of `0-9` and have the same effect. 

### Flags
A flag are placed at the end of a regex after the 2nd slash. Their purpose is to define limits or additonal functionality of the regex. There are 6 flags that can be used individually or together. I didn't use any flags in the email matching but I think it might be useful to mention the `i` flag because it could be used.

* `i` makes the search NOT case sensitive. Meaning `a` or `A` will match.

### Character Escapes
Character escapes is a character that invokes an alternative interpretation on the following characters in a character sequence. They are a common way of looking for special characters in a string. 

* The `\` is a character escape.
* If you wanted to find a dot. You could use `\.`
  
## Author
Drum Holliday

I'm currently a student at the UC Irvine Fullstack Coding Bootcamp 

## Sources
* RegexMagic (https://www.regular-expressions.info/email.html)
* Javascript.Info (https://javascript.info/regular-expressions)
* Microsoft Learn (https://learn.microsoft.com/en-us/dotnet/standard/base-types/grouping-constructs-in-regular-expressions)
  
## My Github 
https://github.com/CoderCoding00