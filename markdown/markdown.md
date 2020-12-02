# Basic Cheat Sheet using Markdown
Usage should be relatively self-documenting.

Best used using a code editor with a markdown viewer, so you can see the source and formatted text side-by-side.

## Headers
    # h1
    ## h2
    ### h3
    #### h4
    ##### h5
    ###### h6

## Code Block
    text for block quote
        <-- 4 spaces to get code block

Non-code block text 

    After normal text

        ^additional newline need for code block

No newline
    = code block fail

## Code Span
This is a `code span`

This is also a ``code span``

    `code span text`
    or
    ``code span text``

``use extra backticks (`) to escape the single backtick ``

## *Italic* & **Bold**
Also: _italic_ and __bold__

    *italic*
    **bold**
    _italic_
    __bold__

## Lists
### Bulleted List
* bullet list
* next item
  * indented item <-- 2 spaces
    * sub-bullet <-- 4 spaces
### Numbered List
1. nested numbered list
1. next numbered item
   1. indented number item <-- 3 spaces
      1. further indented <-- 6 spaces

---
## Horizontal Rule
    ---
---

## Links
### Hyperlink
https://github.com/jykong/reference-jyk/blob/master/markdown/markdown.md

[My Self-Referential Markdown Cheat Sheet](https://github.com/jykong/reference-jyk/blob/master/markdown/markdown.md)

    [linked text](https://github.com/jykong/reference-jyk/blob/master/markdown/markdown.md)

### Anchor Tag
[Jump to Code Block section](#code-block)

    [linked text](#header-name-with-dashes)

## Image

    ![](<insert_img_url>)

## Escape Character
    \
\#
\*
\1.
\---
\    not a code block
\`not a code span`