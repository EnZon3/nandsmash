# NANDsmash language specifications

## Macros

The only built-in instruction in NANDsmash is the NAND gate. The syntax is `!&(a, b)`, where `a` and `b` are the inputs to the gate.

`!&(a, b);`

To define a custom macro, use the command `#`, then the name of the macro (can be anything without whitespace, and cannot start with `#` or `*`), the arguments (comma-separated and enclosed within parentheses), then an assignment operator `=`, and then the body.

For example, to define the NOT gate, it looks like this:

`#!(a) = !&(a, a);`

where `a` is the input and `!` is the name of the macro.

To call a macro, simply use its name and the arguments. For example, the AND gate looks like this:

`#&(a, b) = !(!&(a, b));`

(Note that arguments must be enclosed within parentheses, so !& does not mean "apply ! on &", but rather it is an instruction on its own.)

## Functions*

To define a function, the syntax is the same as a macro, but with an asterisk used:

`*!(a) = !&(a, a);`

The main difference between a macro and a function is that a macro replaces its usage with the definition, while a function runs through the body, and replaces its usage with the return value. For this reason, we recommend you use macros over functions.

Note that until you implement registers, all inputs are assumed to be singular bits.

*NOTE: Functions have been deemed to be obsolete and may be removed entirely soon. This does not guarantee anything.

## Comments

Inline comments are denoted with a double slash //, while multi-line comments are opened with a slash and asterisk, followed by an asterisk then slash /* */.

`#!(a) = !&(a, a); // NOT gate using NAND`

(This syntax is similar to many languages, such as Java, C++, and Kotlin.)

## Delimiters

If you haven't noticed yet, the semi-colon ; is used as a delimiter in NANDsmash (similar to other languages). After each statement, you should include this delimiter so that the compiler understands that it's the end of the statement.

```
#!(a) = !&(a, a) // could work, but not recommended
#!(a) = !&(a, a); // better, compiler knows that this is the end of the statement
```

If you want, you can put multiple statements on the same line, but delimiters must be used to separate them. However, this should only be used with short statements in practice because it makes code a little bit harder to read.

`#!(a) = !&(a, a); #&(a, b) = !(!&(a, b)); // okay, but a little bit hard to read`

[more features written soon]
