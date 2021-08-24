# Lexical Analysis
The purpose of Lexical Analysis is to divide the program into lexical units, this involves classifying substrings of a program according to their purpose and communitcating this to the parser, the next step in compilation

## Tokens
- Tokens are the smallest meaningful unit of information in a computer program
- A Token class is a set of tokens within a programming language that have related meanings
- Token classes include: Identifiers, keywords, string literals, whitespace etc
- They can be described by a token class, and a substring of the input program
- The lexical structure of a programming languages is the set of token classes that exist within the language
- A lexer must be able to recognise which substrings (lexemes) correspond to which tokens, and identify the token class of each lexeme

The compiler will recieve a program as input:
```
if (i == j)\n\tz = 0;\nelse\n\tz = 1;
```
and extract the substrings, labeling them with their token class:
```
if - keyword
" " - whitespace
( - Open Bracket
i - identifier
" " - whitespace
...
```

## Regular Languages and Expressions
A regular language is a language specification used to determine which set of strings belong to a token class, A regular expression determines whoch strings belong to a regular language.

A regular language is a class of formal language (any set of strings formed from an alphabet) that can be defined using regular expressions

The 5 basic constructs in a regular expression are the 2 base cases: empty and 1 character strings, and the three compound expressions: union, concatenation, iteration

### Regular Expression Notation
- The set containing a single character: $\text{'c'} = \{\text{"c"}\}$
- Epsilon - The set containing the empty string: $\epsilon = \{\text{""}\}$
- Union - the set contaning all strings in set $A$ and set $B$: $A + B = \{a\mid a\in A\} \cup \{b\mid b\in B\}$
- Concatenation - The set containing all possible concatenations of a string in $A$ then a string in $B$: $AB = \{ab\mid a\in A\wedge b\in B\}$
- Iteration - The set containg all possibilities of "A character from the set $A$ repeated 0 or any number of times": $A* = \cup_{i\ge0} A^i$

#### Meaning functions
- A meaning function represents the mapping of the syntax of a language to the semantics (meaning)
- Meaning functions (denoted by L) make clear what is notation, and what is semantics in a regular expression
- Meaning functions are most often a many to one mapping, and never one to many
$L(A+B) = L(A)\cup L(B)$

#### Common shorthand notations
| Description  | Shorthand | Meaning                  |
|:------------ |:--------- |:------------------------ |
| At least one | A+        | AA*                      |
| Option       | A?        | A + ε                    |
| Union        | A \| B    | A + B                    |
| Range        | \[a-z\]   | 'a' + 'b' + ... + 'z'    |
| Complement   | \[^a-z\]  | Any character except a-z |
| String       | 'abc'     | 'a''b''c'                |
 
## Lexical Analysis process using regular expressions
### The process
#### (1) Write the regular expressions for the lexemes in each token class
```
Number = digit+
Keyword = 'if' + 'else' + ...
Identifier = letter(letter + digit)*
OpenBracket = '('
...
```

#### (2) Construct a single regular expression for all tokens (R)
```
R = Number + Keyword + Identifier + ...
```

#### (3) Iterate over the input
input = $x_1 \cdots x_n$
For $1 \le i \le n$ check if it matches the regular expression, if not, get the next character in the input and run the check again

#### (4) If the string matches the regular expression
If successful, then the sequence is in the language $x_1 \cdots x_n \in L(R_j)$ where $R_j$ is a token class in the language.
Remove $x_1 \cdots x_n$ from the input and go to step 3

### Problems with this method
**Problem:** using this method, the shortest substring that matches will always be used, for example, with the string "\==", this will match "=" which is incorrect
**Solution:** always use the longest possible match, lookahead can be used to see if there is a better match, but this should be minimised as ideally, you want to look at each character in the input once

**Problem:** which token should be used in the even of more than one match, i.e. a string could be matched as both a keyword and an identifier.
**solution:** order token classes by priority, and place keywords over identifiers

**Problem:** what if no rule matches the string
**Solution:** Create a category of error strings: all strings not in the lexical specification, put it last in the matching priorty

## Finite Automata
A method to implement regular expressions

### A finite automata consists of:
- An input alphabet $\Sigma$
- A set of states $S$
- A start state $n$
- A set of accepting states $F \subseteq S$
- A set of transitions $state \to^{input} state$

### Transitions
- $s_1 \to^a s_2$, if the automaton is in state 1, and recieves the input "a" it will move to state 2
- After the transition, it moves to the next item in the input
- If at the end of the input, it is in an accepting state, it will accept the input
- Otherwise, it will reject the input if: it did not terminate in an accepting state $s \notin F$, or it gets stuck due to no state transition existing for the input

### Graphical Representation of a finite automata
![Graphical representation of a finite state automata|500](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/DFAexample.svg/1280px-DFAexample.svg.png)
- circles represent states
- double circles represent an accepting state
- arrows between circles represent state transitions
- arrow pointing to S1 indicates the starting state

### ε-moves
- The state machine can make a transition without advancing the input
- Epsilon moves are optional, the machine can decide to make it or not

### Deterministic Finite Automata (DFA)
- One state cannot have more than one transition per input
- No epsilon moves
- Can only take one path through the graph for an input (deterministic)
- Can only be in a singe state at any one time
- Are faster to execute, as there are no choices to consider

### Nondeterministic finite automata (NFA)
- Can have multiple transitions for one input in a given state
- Can have epsilon moves
- Multiple paths through the graph can exist for one input (non deterministic)
- An NFA will accept if some of the choices lead to an accepting state (usually 1 or more)
- Is always in a set of states
- Are often much smaller than DFAs


## Implementation
The lexical analyser design pipeline:
- Lexical Specification
- Regular Expressions
- NFAs
- DFAs
- Table driven DFA implementation
### Converting Regular Expressions to NFAs
- Define an NFA for each regexp
#### NFAs for the fundamental regular expressions
The NFA for the regexp M can be represented as:
![[Pasted image 20210824213713.png]]
NFA for Epsilon:
![[Pasted image 20210824213808.png]]
NFA for the character 'a':
![[Pasted image 20210824213942.png]]
NFA for AB:
Input is passed through machine A, then B, without advancing the input
![[Pasted image 20210824214050.png]]
NFA for A+B:
If either A or B finishes in an accepting state, the string will be accepted
![[Pasted image 20210824214337.png]]
NFA for A*:
![[Pasted image 20210824214611.png]]

### Converting NFAs to DFAs
#### Epsilon Closure
- The epsilon closure of state A is the set of all states that can be reached from A only following epsilon moves
- If B is in the ε-closure of A, then all states in the ε-closure of B are also in the ε-closure of A
#### How many different states can an NFA be in?
- An NFA can be in many states at any time (a DFA must be in 1 state at any time)
- If an NFA has $N$ states, $|S| \le N$, where S is the subset of all states where the NFA is in that state
- there are $2^N - 1$ possible sets of states that the NFA can be in
- There is a finite number of possible configuration
#### Conversion Process
**NFA:**
- states: $S$
- starting state: $s \in S$
- final states: $F \subseteq S$
- Transition function: $a(X) = \{y \mid x \in X \wedge x \to^a y\}$ where a is a character in the input language, and X is a set of states, gives the set of states that can be reached from the states in X using input a
- Epsilon Closure

**DFA:**
- states: all possible non empty subsets of $S$
- start state: Epsilon Closure of $s$, this gives all the states an NFA could be in before any input is read
- final states: $\{X \mid X \cap F \neq 0\}$, capture every state that has at least 1 final state
- Transition function: $X \to^a Y$ if $Y = \epsilon\text{-closure}(a(X))$
- Is a DFA as: finite set of states, a single start state, a finite set of final states, only 1 transition per input, no epsilon moves

![[Pasted image 20210824225749.png]]

