# Lexical Analysis
- Divide code up into lexical units
- Token Classes: identifiers, keywords, numbers
- Token classes are sets of strings in a program, identifiers: a string of letters/digits starting with a letter
- Integer: non-empty string of digits, and optionally a "-" sign at the start
- Keywords - if, else
- Whitespace - non empty sequence of spaces or tabs
- Goal: classify substrings of the program according to their role, and communicate this to the parser
- Token: Token class + substring of input

Code written by programmer
```
if (i == j)
	z = 0;
else
	z = 1;
```

What the computer sees
```
if (i == j)\n\tz = 0;\nelse\n\tz = 1;
```

Necessary token classes: Whitespace, Keywords, Identifiers, numbers, (, ), ;, =, operators

Tokenised program:
```
if - keyword
" " - whitespace
( - Open Bracket
i - identifier
" " - whitespace
== - Operator
" " - whitespace
) - Close Bracket
\n\t - Whitespace
z - Identifier
" " - Whitespace
= - Assignment
...
```
- Must do 2 things - Recognise the substrings corresponding to tokens (lexemes)
- Identify the token class of each lexeme

-  lookahead: look forward in the code to work out the meaning of a token in the current context, when doint a left to right scan
-  Lookahead should be minimised, as it is inefficient

- Lexical structure: set of token classes
- regular languages - used to say which set of strings belong to a token class
- regular expressions
- Single character: $\text{'c'} = \{\text{"c"}\}$
- Epsilon - empty string: $\epsilon = \{\text{""}\}$, not an empty set of strings
- Union - $A + B = \{a\mid a\in A\} \cup \{b\mid b\in B\}$
- Concatenation: all possible combinations of a followed by b - $AB = \{ab\mid a\in A\wedge b\in B\}$
- Iteration - A concatenated with itself i times, where i is 0 or positive: $A* = \cup_{i\ge0} A^i$

example:
regular language - the set including 0 and 1:
$\Sigma = \{0, 1\}$
`(0 + 1)*1(0 + 1)*`
a 0 or a 1, an unlimited number of times, or nothing, a 1, and a 0 or a 1 no times or an unlimited number of times
`0*1*10`
unlimited or no 0s, unlimited or no 1s, and 1 and a 0

- the 5 constructs in regular expressions: Two base cases: empty and 1 character strings, the three compoud expressions: union, concatenation, iteration

- A formal language is any set of strings formed from an alphabet
- example: alphabet: ASCII, formal language: All C programs
- A meaning function maps the syntax of a language to semantics
- Meaning function (denoted as L) makes clear what is syntax, and what is semantics
- Notation and semantics can be separated
- Expressions and Meanings are not a one to one mapping
$L(A+B) = L(A)\cup L(B)$
- Meaning functions are never one to many, a piece of syntax cannot have more than 1 meaning