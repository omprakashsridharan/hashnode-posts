## Go: Declarations, Conditions, Loops

# Declarations

Every language needs to have the ability to declare variables and constants in order to hold some information as state for the code to run with.

## Variables

In Go, variables are declared using the syntax 
> var name string
var -> variable
name -> name of our variable
string -> type of our variable

As the name suggests, variables are mutable, meaning their values can be changed throughout it's lifecycle or scope. 

## Short variable declaration operator ( := )

Most of the times we have the declarations with an initial value in mind.
For ex:

> var i int32 = 0

For these scenarios, Go reduces the verbosity by provide a new operator := ( Short variable declaration ) which is written like

> i :=  2*8 // The expression is evaluated and the result type is assigned to the variable

## Constants

There will be scenarios according to the business login or a proven fact that certain values cannot change throughout the program. Those can be termed as constants which are immutable, meaning their value can never be mutated/modified.

> const pi = 3.14

> Note: A numeric constant has no type until it’s given one, such as by an explicit conversion.

# Conditions

## If - Else / If - Else If - Else 

No magic here :)


```
if 7%2 == 0 {
    fmt.Println("7 is even")
} else {
    fmt.Println("7 is odd")
}
``` 

There will be scenarios where we need to define a temporary variable before evaluating a condition. Go's if statements provide the capabilities to assign and then check.


```
if num := 9; num < 0 {
    fmt.Println(num, "is negative")
} else if num < 10 {
    fmt.Println(num, "has 1 digit")
} else {
    fmt.Println(num, "has multiple digits")
}
``` 

> Note: We don’t need parentheses around conditions in Go, but that the braces are required.

> Bummer: There is no ternary if in Go, so we need to use a full if statement even for basic conditions. :/

## Switch

Switch statements express conditionals across many branches. We can use commas to separate multiple expressions in the same case statement. We use the optional default case for handling the rest of corner cases.


```
i := 2

switch i {
    case 1:
        fmt.Println("one")
    case 2:
        fmt.Println("two")
    case 3:
        fmt.Println("three")
}
``` 

# Loops

**for is Go’s only looping construct** No more pain of deciding which loop to use. The Beauty of Go is that there is an opinionated way for everything and it's easy to learn.

## Declare outside loop

```
 i := 1
    
for i <= 3 {
    fmt.Println(i)
    i = i + 1
}
``` 

## Inline loop

```
for j := 7; j <= 9; j++ {
    fmt.Println(j)
}
```

## Loop with break

```
for {
    fmt.Println("loop")
    break
}
``` 

## Infinite loop

```
for {
    fmt.Println("loop")
}
``` 

# Conclusion

Whatever we have seen so far covers the basics of Go and doesn't even showcase the complete power of Go. Next, we will jump right into creating Data Structures like Linked lists, Trees, Queues, Graphs, ...etc using Go and yeah semicolon is not needed in Go if expressions are in separate lines :)

 

 