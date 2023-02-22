# Regex-planation

This little markdown is written to help beginners start to make some sense of some common regular expression (regex) notation to make search functions and data validation more efficient. 

## Summary


Regular Expressions can look very intimidating to the uninitiated. Take for example the regular expression for an email:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```


See the pattern? 

If not read on.

Don't worry, with just a little explanation, they start to make sense! Anyone who needs to find or validate information will soon recognize their usefulness.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

```/^``` example regular expression ```$/```

The ```^``` and ```$``` in this example are **anchors**, and surrounded by "```/```" to signify that this regular expression is a literal. 

The ```^``` anchor says "look for a string that *begins* with the following characters. Whatever comes after the ```^``` should be the first letter or letters in the desired expression.

The ```$``` anchor says "this is the end of the string." For example the word "donut" satisfies the regex ```/t$```, however "chocolate" does not because we're looking for a word that *ends* with t.


### Quantifiers

The ```{2,6}``` represents a quantifier range for the top-level-domain-suffix of the email. Emails follow the pattern of somebody@somedomain.com, but the .com might be .net or .org or .io or even .asia. In this case, the second argument ```6``` places the upward limit of 6 characters for the email suffix. The first number ```2``` is necessary and gives the minimum number of characters in the email top level domain. Patterns like something@thisplace.e would not be considered.

### Grouping Constructs

The email regex has three groupings:

```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```
```([a-z0-9_\.-]+)```

```([\da-z\.-]+)```

```([a-z\.]{2,6})``` <-(recognize that the quantifier is included in in this grouping.)

Groupings are marked by "```()```" parentheses. The first grouping says "we want a group of any of these possible charaters," then an at symbol "```@```", then "some characters like this" (second grouping), then a period "```.```", then "2 to 6 more characters."


### Bracket Expressions

You may notice that many of the above described groupings contain brackets with dashes  such as:

```[a-z0-9_\.-]``` 

```[\da-z\.-]```

```[a-z\.]```

These brackets indicate that **any** of the characters inside the brackets may be present. Sometimes emails look like this.dude@abides.com or michael_scott@dunder-mifflin.com, so the underscore and dash are listed out in the brackets. But these brackets also contain ...

### Character Classes

The ```a-z0-9``` in the first regular expressions are "any letter a through z" and "any numeral 0 through 9." Combined with the other special characters listed, these let us know we are looking for all these charcters in a string before the @ symbol. The brackets ```[]``` let us know we are defining a character class. (Character classes can also be negated with ```^```, see the [MDN docs for examples](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Cheatsheet#character_classes).)

### The OR Operator

While not present in the email example, certain cases call for the OR operator signified by the pipe character "```|```" 

In the email example, no whole word strings are given as alternative choices. "Or" is implied in the character classes. ```[abc]``` says, effectively "a OR b OR c." If there were specific words we wanted to search for, such as a more restricted search between two domains, we could do something like:

```
/^([a-z0-9_\.-]+)@[this\.com|that\.com]$/
```

### Flags

Certain letters in javascript constitute flags for regular expressions in javascript. There are six in javascript and you can read about them [here.](https://javascript.info/regexp-introduction#:~:text=A%20regular%20expression%20consists%20of,otherwise%2C%20only%20the%20first%20one.)

(None are used in this example.)

### Character Escapes

You may have noticed that there's an extra backslash before the period in between the first and second grouping in the email example. This is because ```.``` in regex also serves as a wildcard for any single letter. So ```/.y/``` would match "by" and "my" but not "yes." However by putting the backslash before the period ```\.```, it is recognized that we actually want a period before the top level domain. (.com or .net, et cetera)

Backslash provides character escapes for any other reserved characters in regular expressions such as ```\$``` or ```\^``` or ```\(``` and ```\)``` or even ```\\``` and ```\/```.

## Author

This article is by Josh Goeke https://github.com/joshuagoeke

For some other resources on regex, check out these helpful sites that helped me figure these things out:

https://www.rexegg.com/regex-quickstart.html

Great game for practice: https://m.regexcrossword.com/puzzles

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
