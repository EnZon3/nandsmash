# Examples

### Simple NAND operation
```ns
!&(0,0);
```

### Chaining NAND operations
```ns
!&(!&(0,0),!&(1,1));
```

### Create a macro
```ns
#macroname(a,b) = !&(!&(a,1), !&(b,1));
```

### Use a macro
```ns
#macroname(0,1);
```

### Create a function
```ns
*function(a,b) = !&(!&(a,1), !&(b,1));
```

### Use a function
```ns
*function(0,1);
```

## Difference between a macro and function:
A macro is a simple text replacement, while a function is a more complex operation that can take arguments and return values. Macros are typically used for simple operations, while functions are used for more complex operations.

## Ports

Access parts of memory using ports.

### Read from a port

```ns
@(0b..); // Read from port 0b...

!&(1,@(0b...)); // NAND operation with port
```

### Write to a port

```ns
@(0b...) = 1; // Write 1 to port 0b...
```

### Read from a port and write to another port

```ns
@(0b...) = @(0b...); // Read from port 0b... and write to port 0b...
```

## Circuits

Multibit manipulation using circuits.

### Create a circuit

```ns
$circuitname(inputs) {
  // circuit ops...
} = (outputs);

circuitname(inputs); // returns outputs
```

### Operations

```ns
$circuitname(D, E) {
  *nand1() = !&(D, E)
  *nand2() = !&(!(D), E))
  *set() = !&(nand1(), reset())
  *reset() = !&(nand2(), set())
} = (set, reset);
circuitname(inputs); // returns outputs
```