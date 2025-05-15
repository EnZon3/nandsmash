# NANDsmash REPL (read-eval-print loop)

## Evaluation

The NANDsmash REPL evaluates expressions the same way that the compiler does. When given an expression, the REPL will expand any macros used and evaluate all the NAND gates from there. For example, take a look at the following:

```
>>> !&(0, 1);
1
>>> !&(1, 1);
0
>>> !&(0, 0);
1
```

As you can see, the REPL evaluates each expression according to the NAND truth table. Nesting NAND gates also works, as each inner NAND gate will be evaluated to get the final result.

```
>>> !&(!&(1, 1), 1);
1
```

## Macros

Creating a macro in the REPL is the same as creating a macro in a file - you use the same syntax as you would normally. However, in the REPL, an output will be sent in the form of `<Macro@"name(inputs)>`, which indicates a macro creation.

```
>>> #!(a) = !&(a, a);
<Macro@"!(a)">
>>> #&(a, b) = !(!&(a, b));
<Macro@"!&(a, b)">
```

This output does not correspond to the evaluation of any expression - it is simply there to signal that the macro has been successfuly stored. You may then use these macros as you please.

```
>>> #!(a) = !&(a, a);
<Macro@"!(a)">
>>> !(0);
1
>>> !(1);
0
```

You can also nest macros within each other, or use a macro in another macro's definition. All in all, macro syntax and rules are the same as in the compiler.

## Exceptions

[will be implemented soon]
