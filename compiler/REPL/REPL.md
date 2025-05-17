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

Exceptions (also Errors) happen when the REPL cannot determine the evaluation of an expression, which can occur in different ways. When you make an error, the REPL will show you where that error occurred. There are two types of errors in the NANDsmash REPL: `SyntaxError` and `MacroError`.

### `SyntaxError`

A `SyntaxError`, as the name suggests, occurs when the syntax of the expression is used incorrectly (e.g. forgetting to close parentheses, using a comma without an input before it). For example, take a look at these:

```
>>> !&(1, 0;
Error: SyntaxError: Expected ')'
!&(1, 0;
       ^
>>> !&(, 0);
Error: SyntaxError: Expected value before ','
!&(, 0);
   ^
```

Syntax errors can easily be fixed, as the error is identified by the REPL and logged.

### `MacroError`

A `MacroError` occurs when you try to use a macro that is a) not defined, or b) contains the wrong number of inputs. You might try to use a macro that is not defined, or you may use a macro that is defined but with a different number of inputs. For example:

```
>>> !(1);
Error: MacroError: No defined macro for 1-input !
!(1);
^
>>> #!(a) = !&(a, a);
<Macro@"!(a)">
>>> !(0, 1);
Error: MacroError: No defined macro for 2-input !
!(0, 1);
^
```

Macro errors are also easy to find, but you may have to re-define a macro with a different number of inputs to fix the problem.
