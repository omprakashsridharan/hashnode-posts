## Hello Go

# Introduction
Go is an open-source systems programming language developed and maintained by Google. The syntax of Go is very close to C/C++ and hence college students who are preparing for job interviews can use Go for their competitive programming rounds. Though not faster than C, Go compiles quickly and runs relatively fast compared to other languages. Use cases of Go have emerged to be much more than what it was initially developed for (Systems programming - Creating tools and services for infrastructure or other core hardware interfaces). Golang can be used for web development, Command Line Interfaces (CLIs), System software and wide variety of embedded IOT device platforms. This article will help in understanding the basic syntax of Go that is sufficient for us to navigate and solve some data structure problems.

# Hello World
It is customary to start with a "Hello World" program to learn a language, so why not :) 

```
/* Every go executable project must have the main
 file associated with a package main and a main function
which will serve as the entry point to our application */
package main 

/* Next is the import section where all the dependent modules/libs
are imported which provide additional functionality.
"fmt" -  formatted I/O with functions analogous to C's printf and scanf */
import "fmt"

/* The main function which gets executed when the command
"go run <file>.go" is issued by the user. fmt package exports a
method by name Println which prints the contents within the parenthesis
to the standard output and appends a new line character \n at the end.
In addition to Println, fmt exports other utility functions for formatting
I/O functions. (https://golang.org/pkg/fmt/) */
func main() {
    fmt.Println("hello world")
}
``` 
You can save the above code in a new file called "hello-world.go" and run the code using the command 
> go run hello-world.go

*Note: You should have a working Go installation. Follow this [link](https://golang.org/doc/install) to install go on your machine *

Just like C/C++, Go is a compiled language meaning the Go compiler reads the .go file and spits out a binary which can be transferred and run on any machine. We can read about building go later when the need arises.

# Up Next
We will go through the various features of Go in the upcoming articles and start with the implementation of Common DS in Go and build our way up to Complex/Advanced ones.
