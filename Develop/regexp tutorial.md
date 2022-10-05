# RegEx

A regular expression is a sequence of characters/word that specifies a search pattern in text.

## Summary

Briefly summarize the regex you will be describing and what you will explain. Include a code snippet of the regex. Replace this text with your summary.

I will try to use the same example so that it would be clearer.

## Table of Contents
- [Syntax](#syntax)
- [Modifiers](#modifiers)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)


## Syntax

/pattern/modifiers;
for example, to look for a word 
let text = "Hi Bye Hi";
let n = text.search(/Hi/);  //that will return the index of the word Hi which is 0

## Modifiers

By default 
Regular expressions are

A-case sensitive  this can be changed by the use of i(case insensitive). i is one of the modifiers.
let text = "Hi Bye Hi";
let n = text.search(/hi/);   //this will return -1 which means not found as search is case sensitive
let n = text.search(/hi/i);   //this will return 0 which means it found h character regardless of case sensitivty as search is case insensitive now

B-find first match only this can be changed by the use of g(global search). g is one of the modifiers.
let text = "Hi Bye Hi";
let n = text.match(/Hi/); //Hi

let text = "Hi Bye Hi";
let n = text.match(/Hi/g); //Hi,Hi

C-treat the the text as a single line. This can be changed by the use of m(multiple line search) where each new line is considered a single different line. m is one of the modifiers.
let text = `Hi 
Bye hi`;
let pattern = /^Bye/;
let result = text.match(pattern);  //here nothing is displayed as it is looking for a Bye word at the begining of the line.
If we added /m    let pattern = /^Bye/m; //it will be found as it now treats each new line as a single line

## Regex Components



### Anchors
Anchors are 2 special characters have special meaning in regular expressions. They do not match any character. Instead, they match a position before or after characters:

- ^ which is called caret   it matches the beginning of the text
- $ which is called dollar  it matches the end of the text

### Quantifiers
Quantifiers indicate numbers of characters or expressions to match.

syntax:-
-x*    means Matches the preceding item "x" 0 or more times
-x+    means Matches the preceding item "x" 1 or more times
-x?    means Matches the preceding item "x" 0 or 1 time
-x{n}  means Matches the preceding item n times 
For example, /a{2}/ doesn't match the "a" in "candy", but it matches all of the "a"'s in "caandy", and the first two "a"'s in "caaandy".
/\b{n}\b/ /b will make it look for the words with the exact number of characters.
-x{n,}  means Matches at least "n" occurrences of the preceding item "x". 
For example, /a{2,}/ doesn't match the "a" in "candy", but matches all of the a's in "caandy" and in "caaaaaaandy".
-x{n,m}	 means matches from at least 2 characters to at most m character.

/\b{n}\b/ where n is the exact number of characters we are looking for so for example if we use
let text = "Hi 101 Bye Hi";
let n = text.match(/\d{2}/); that will return 10
BUT
let n = text.match(/\b\d{2}\b/); that will return null

if d(stands for digit) is added, that means will be looking for digits
let text = "Hi 101 Bye Hi";
let n = text.match(/\d{4}/);    //here, it will be empty
let n = text.match(/\d{3}/);    //here it will result in 101
let n = text.match(/\d{2}/);    //here it will result in 10
let n = text.match(/\d{1}/);    //here it will result in 1

### OR Operator
OR is written as | in regexp 
it means to search for either of the words or characters.

syntax

let regexp = /x|y|z/; where x,y,z can be characters of words

example
let regexp = /html|php|css|javascript/;
let str = "First HTML appeared, then CSS, then JavaScript";

alert( str.match(regexp) ); // here results will be any of these 'HTML', 'CSS', 'JavaScript' . Since, we did not add g for global, it will be
                            //  the first expression which is HTML


### Character Classes
A character class is a special notation that matches any symbol from a certain set.
there are many character classes, however will only explain the most common
- \d (“d” is from “digit”)
A digit: a character from 0 to 9.
- \s (“s” is from “space”)
A space symbol: includes spaces, tabs \t, newlines \n and few other rare characters, such as \v, \f and \r.
- \w (“w” is from “word”)
Word is either a letter of Latin alphabet or a digit or an underscore _.
- /./ A dot is “any character”
A dot . is a special character class that matches “any character except a newline”. Any character means a characterm not the abscence of a character

example1:-
alert( "I love HTML5!".match(/\s\w\w\w\w\d/) ); // ' HTML5'

example2:-
let str = "+7(903)-123-45-67";
let regexp = /\d/;
alert( str.match(regexp) ); // 7

Without the flag g, the regular expression only looks for the first match, that is the first digit \d.
Let’s add the g flag to find all digits:
let str = "+7(903)-123-45-67";
let regexp = /\d/g;
alert( str.match(regexp) ); // array of matches: 7,9,0,3,1,2,3,4,5,6,7


Inverse classes is matching all classes except the one we specified. It is written the same way as the character Classes
but in capital letters

### Flags
  Flags are the same as modifiers mentioned above.
  We will add here some other modifiers which are not as common as g,i or m.

-s
Enables “dotall” mode, that allows a dot . to match newline character \n (covered in the chapter Character classes).
-u
Enables full Unicode support. The flag enables correct processing of surrogate pairs. 
-y
“Sticky” mode: searching at the exact position in the text.


### Grouping and Capturing
it is a way creating an expression by adding more than one character so that this expression will be treated as a single character.
syntax
that expression that will be treated as a single character will be enclosed in parentheses (...). This is called a “capturing group”.

for example
Without parentheses, the pattern go+ means g character, followed by o repeated one or more times. For instance, goooo or gooooooooo.
With parentheses, the pattern (go)+ means go will be treated as a single character so to match, it will be go or gogo or gogogo and so on



### Bracket Expressions
Brackets indicate a set of characters to match.
[] will look for specific characters and operate on them.

example
[abc]	Any of the characters a, b, or c 
[A-Z]	Any character from uppercase A to uppercase Z
[a-z]	Any character from lowercase a to lowercase z
[A-z]	Any character from uppercase A to lowercase z
[^a-c]  Any character NOT between lowercase a to lowercase c
[0-9]	Find any character between the brackets (any digit)
(x|y)	Find either x or y

example
let text = "Is this all there is?";
let pattern = /[t*i]/;
let result = text.match(pattern); 
### Greedy and Lazy Match
'Greedy' means match longest possible string.
'Lazy' means match shortest possible string.

for example 
let text = "<div>Hi Bye Hi<div>";
let greedy = text.match(/<.+>/g);//that will return the whole sentence since it will look for < then matches the last > which would be at the end of the sentence
let lazy = text.match(/<.+?>/g);  //that will return the first div since we added ? which means 0 or 1 charcater to evaluate it in the shortest match(lazy) 



### Back-references
A backreference in a regular expression identifies a previously matched group and looks for exactly the same text again.
Back reference can be done by name or number
If a regexp has many parentheses, it’s convenient to give them names.

By name:-
To reference a named group we can use \k<name>.
example:-
let str = `He said: "She's the one!".`;

let regexp = /(?<quote>['"])(.*?)\k<quote>/g;

alert( str.match(regexp) ); // "She's the one!"

By number:-
A group can be referenced in the pattern using \N, where N is the group number.

let str = `He said: "She's the one!".`;

let regexp = /(['"])(.*?)\1/g;

alert( str.match(regexp) ); // "She's the one!"


### Look-ahead and Look-behind
You can define patterns that only match when they're followed or not followed by another pattern with lookaheads.

Positive and negative lookaheads:

x(?=y) –  lookahead (matches 'x' when it's followed by 'y')
x(?!y) –  lookbehind (matches 'x' when it's not followed by 'y')

“lookahead” and “lookbehind”, together referred to as “lookaround”.
Lookahead
The syntax is: X(?=Y), it means "look for X, but match only if followed by Y". There may be any pattern instead of X and Y.
let str = "1 turkey costs 30€";

alert( str.match(/\d+(?=€)/) ); // 30, the number 1 is ignored, as it's not followed by €

Lookbehind
Lookbehind is similar, but it looks behind. That is, it allows to match a pattern only if there’s something before it.
(?<=Y)X, matches X, but only if there’s Y before it.


## Author
Mina Ghaly
