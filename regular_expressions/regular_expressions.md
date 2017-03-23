### Regular Expressions

http://regexr.com/

#### Basic Matching
Regular expressions search for sequence matches within strings, case sensitive

    "ab"
    matches: "ab", "abc", "fabulous"
    does not match: "a", "b", "ba", "AB", "ball", "acrobatic"

#### Any Character: .
    "b.t"
    matches: "bat", "bet", "bitter", "habitual"
    does not match: "boot", "tub"

#### Starts With: ^
    "^bi"
    matches: "bit", "binomial"
    does not match: "habit", "alibi"

#### Ends With: $
    "bi$"
    matches: "alibi"
    does not match: "bit", "habit"

#### End of Word Boundary: \b
    "\bg"
    matches: g from "bag of words"

#### Start of Word Boundary: \B
    "\Bw"
    matches: w from "bag of words"

#### Character Escaping: \
To use special characters (i.e. .^$[]), use the \ as an escape character

    "e\."
    matches: "done.", "overrate."
    does not match: "done\.", "bee"

#### Multiple Character Matching: []
    "[rRy]a"
    matches: "rate", "Rate", "yay"
    does not match: "Yay!", "array"

#### Character Range: [-]
    "[0-9][a-z]"
    matches: "0a", "==9z=="
    does not match: "a0", "9Z"

#### Negated Character Set: [^]
    "[^0-9]"
    matches: "abc" ".?/"
    does not match: "123"

#### Character Classes: [.] or [\\]
Special character classes for commonly used character classes
* `.`: any non-linebreak, equivalent to [^\n\r]
* `\d`: digits, equivalent to [0-9]
* `\D`: non-digits, equivalent to [^0-9]
* `\w`: alphanumeric and underscore
* `\W`: non-alphanumeric or non-underscore
* `\s`: whitespace
* `\S`: non-whitespace

    "[\d]"
    matches: "123"
    does not match: "abc" ".?/"

    "[^\w\s]"
    matches: essentially, all non-underscore punctuation



#### OR Expression Matching: [|]
    "cat|dog"
    matches: "catfish", "doggie", "hotdog"
    does not match: "dot", "goat"

#### N-times Quantifier: []{}
Exact n-times match

    "[0-9]{5}"
    matches: "00000", "29104"
    does not match: "0", "9234234"

Greater than or equal to match

    "[0-9]{5,}"
    matches: "00000", "9234234"
    does not match: "1234"

Range match

    "[0-9]{1,4}"
    matches: "0", "1234"
    does not match: "29104", "9234234"

#### One or More Quantifier: [+]
    "[0-9+]"
    matches: "0", "3453453495024950345"
    does not match: ""

#### Lazy Operator: [?]
    "[0-9+?]"
    matches first number only: 0 from "0", 3 from "3453453495024950345"
