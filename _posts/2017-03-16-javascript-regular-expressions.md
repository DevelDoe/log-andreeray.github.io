---
date: '2017-03-16 06:14 +0100'
published: true
title: JavaScript - Regular Expressions
category:
  - JavaScript
---

 > A regular expression, regex or regexp (sometimes called a rational expression)is, in theoretical computer science and formal language theory, a sequence of characters that define a search pattern. Usually this pattern is then used by string searching algorithms for "find" or "find and replace" operations on strings (2017, wikipedia).
 
## Syntax

`/pattern/modifiers; `


## Working with regular expressions

Regular expressions are used with the RegExp methods test and exec and with the String methods match, replace, search, and split.

When you want to know whether a pattern is found in a string, use the test or search method; for more information (but slower execution) use the exec or match methods. 

### Methods 

|method|desc|
|--|--|
|exec|Executes a search for a matching in a string. It returns an array of information or null on a missmatch.|
|test|Tests for a match in a string and returns a boolean|
|match|Executes a search for a matching in a string and returns array of information or null.|
|search|Tests for a mach in a string and returns the index of the match or -1.|
|repleace|Executes a search for match in a string and replaces the substring with a replacement substring.|
|split|Uses a regular expression or fixed string to break a string into an array of substrings.|

If you use exec or match and if the match succeeds, these methods return an array and update properties of the associated regular expression object and also of the predefined regular expression object, RegExp. 

If the match fails, the exec method returns null (which coerces to false).

### Examples 

**Find a match**

```js
var myRe = /d(b+)d/g
var myArray = myRe.exec(' cdbbdb sbz')
console.log(myArray) // => ["dbbd", "bb"]
```

**If you do not need to access the properties of the regular expression**
* If you need to use a method like indexOf on the regular expression at a later state, you cannot use this syntax*

```js
var myArray = /d(b+)d/g.exec('cdbbdbsbz')
```

**Equivalent**

```js
var myArray = "cdbbdbsbz".match(/d(b+)d/g)
```

**construct the regular expression from a string**

```js
var myRe = new RegExp('d(b+)d', 'g')
var myArray = myRe.exec('cdbbdbsbz')
```

### Using parenthesized substring matches

Including parentheses in a regular expression pattern causes the corresponding submatch to be remembered. For example, /a(b)c/ matches the characters 'abc' and remembers 'b'. To recall these parenthesized substring matches, use the Array elements [1], ..., [n].

The number of possible parenthesized substrings is unlimited. The returned array holds all that were found. The following examples illustrate how to use parenthesized substring matches.

The following script uses the replace() method to switch the words in the string. For the replacement text, the script uses the $1 and $2 in the replacement to denote the first and second parenthesized substring matches.

```js
var re = /(\w+)\s(\w+)/;
var str = 'John Smith';
var newstr = str.replace(re, '$2, $1');
console.log(newstr); // => "Smith, John"
```


## Modifiers

|modifier|description|
|--------|-----------|
|i|Case-insensitive|
|g|Global match (find all matches rather then stopping after the first)|
|m|Multiline matching|

## Brackets

Brackets are used to find a range of characters. 

|expression|description|
|--------|-----------|
|[abc]|Find any character between the brackets|
|[^abc]|Find any character NOT between the brackets|
|[0-9]|Find any character between the brackets (digits)|
|[x|y]|Find any of the alternatives specified|

## Metacharacters

Metacharacters are characters with spacial meaning.

|metacharacter|description|
|--------|-----------|
|.|find a single character, except newline or line terminator|
|\w|find a word character|
|\W|find a non-word character|
|\d|find a digt|
|\D|find a non-digit character|
|\s|Matches a single white space character, space, tab,form feed, line| feed|
|\S|Matches a single character other than white space|
|\b|find a match at the beginning/end of a word|
|\B|find a match not at the beginning/end of a word|
|\O|find a NUL character|
|\n|find a new line character|
|\f|find a form feed character|
|\r|find a carriage return character|
|\t|find a tab char|
|\v|find vertical tab char|
|\xxx|find the char specified by an octal number|
|\xdd|find the character specified by a hexadecimal nuber dd|
|\uxxx|Find the Unicode character specified by a hexadecimal number xxxx|

## Quantifiers

|quantifier|description|
|--------|-----------|
|n+|Match any string that contains at leas one *n*|
|n*|Match any string that contains zero and more *n*|
|n?|Match any string that contains zero or one occurences of *n*|
|n{X}|Matches any string that contains a sequence of X n's|
|n{X,Y}|Matches any string that contains a sequence of X to Y n's|
|n{X,}|Matches any string that contains a sequence of at least X n's|
|n$|Matches any string with n at the end of it|
|^n|Matches any string with n at the beginning of it|
|?=n|Matches any string that is followed by a specific string n|
|?!n|Matches any string that is not followed by a specific string n|

## RegExp Object Properties

|Property|Description|
|--------|-----------|
|constructor|returns the function that created the RegExp objects prototype|
|global|checks whether the "g" modifier is set|
|ignoreCase|checks whether the "i" modifier is set|
|lastIndex|specified the index at which to start the next match|
|multiline|checks whether the "m" modifier is set|
|source|return the text of the regEx pattern|