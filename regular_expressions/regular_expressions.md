### Regular Expressions

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

#### Multiple Character Matching: []
    "[rRy]a"
    matches: "rate", "Rate", "yay"
    does not match: "Yay!", "array"

#### Character Range: -
    "[0-9][a-z]"
    matches: "0a", "==9z=="
    does not match: "a0", "9Z"

#### Character Escaping: \
To use special characters (i.e. .^$[]), use the \ as an escape character

    "e\."
    matches: "done.", "overrate."
    does not match: "done\.", "bee"

#### Multiple Expression Matching: |
    "cat|dog"
    matches: "catfish", "doggie", "hotdog"
    does not match: "dot", "goat"

#### N-times Repeating Expressions: {}
    "[0-9]{5}"
    matches: "00000", "29104"
    does not match: "0", "9234234"

#### Infinite Repeating Expressions: *
    ".*"
    matches everything!

    "[0-9a-z]*"
    matches: "somanyrun0nw0rd5"
    does not match: " ", "\n", "\t"
