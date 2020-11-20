## Data structures using Go: Linked Lists

# Theory

Linked lists are linear data structures where the individual unit is called a node and multiple nodes are connected together using links to form a link, hence the name Linked Lists.

### How it is supposed to look

![Screenshot 2020-11-19 at 12.13.43 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1605768244138/YTfGdDbmC.png)

### How it really looks

```
/* Struct is a composite data type in Go, meaning it is a data type
formed by the composition of primitive/composite data types */
type Node struct {

/* next is a Pointer to Node type. Pointer variables
store the memory location of the stored values rather
than the actual value. */
    next *Node

/* data is of interface type which is special in Go. interface
is similar to any type in JavaScript. It is the base type of every
type in Go and hence every data type in Go is also an interface {}
type. We can provide an int32, string, float or any composite type
as data, but since it is loosely typed, we lose the type
inferencing power of Go. */
    data interface{}
}

/* This is the data type that will store the head pointer 
(Memory address of the first node in the linked list) */
type List struct {
	head *Node
}

``` 

## Flavors

There are many flavors of linked lists, but the more common ones are
1. Singly Linked List -> Head points to the first node and the last node points to null
2. Doubly Linked List -> Every node has another pointer called previous which as you guessed stores the address of the previous node
3. Circular Linked List -> This is same as SLL but the last node points to the head

## Interface

As we know, Go is statically typed language and everything has a contract to be satisfied by all parts of the code. Interface in Go is a collection of **Method** signatures which is a like a contract that needs to be satisfied by the data type that is implementing the interface.

> Note: Methods and functions are different. A function is an independent piece of code that can be called anywhere. Methods are functions that are attached to a data type as receiver and called using the dot (.) syntax. 

# Project Setup

1. Let's create a folder called data-structures wherever you like. 
2. Go projects can be initialized using something called as Go modules. Checkout this [article](https://blog.golang.org/using-go-modules#:~:text=A%20module%20is%20a%20collection,needed%20for%20a%20successful%20build.) for more info on go modules. 
3. Change directory to the one you just created "data-structures"
4. Run the command 
> go mod init data-structures
5. You can now have as many submodules in your project
6. Create a folder called linkedlist
7. Create a file in the linkedlist folder as base.go where all the basic definitions about our linked list will be there
8. Create a file called main.go in the main project data-structures directory which will be the entry point of our application.

## data-structures/main.go

```
package main

import (
	"data-structures/linkedlist"
	"fmt"
)

func main() {
	fmt.Println("Hello Go")
	linkedlist.HelloLinkedList()
}

``` 

## data-structures/linkedlist/base.go

```
package linkedlist

import "fmt"

// BaseImplementer creates an interface for all the base methods a linked list should have
type BaseImplementer interface {
	Insert(data interface{})
	Print()
	DeleteAtGivenPosition(position int32)
	Length()
	Reverse()
}

// HelloLinkedList is a dummy method to see if the package exports correctly
func HelloLinkedList() {
	fmt.Println("Hello Linked List")
}

``` 

> Note: 
1. Notice the first line in base.go. We are creating a new submodule/package called linkedlist
2. Any function/struct/method/variable that is declared within a package will be accessible / eligible for export only when they are named with **CapitalCamelCase**
3. Notice how we import the linkedlist package in the main.go and call the exported HelloLinkedList function.


All the code snippets used in the articles of this series will be available in [https://github.com/omprakashsridharan/go-data-structures](https://github.com/omprakashsridharan/go-data-structures)

## Up Next
In the upcoming posts we will make the individual flavors of linked list implement the interface that we have drafted above.




