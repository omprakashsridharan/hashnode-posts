## Data structures using Go: Singly Linked Lists

# Singly Linked Lists

As discussed on the previous chapter, we have defined the interface for a base set of functions needed for linked lists. Singly linked lists have a head and the last node of the linked list points to null. Let us implement the interface methods for singly linked list.


```
type BaseImplementer interface {
	Insert(data int32)
	Print()
	DeleteAtGivenPosition(position int32)
	Length()
	Reverse()
}
``` 



1. Create a folder "singly-linked-list" under previously created linked list folder
2. Create a file called singly-linked-list.go under the above created folder

## Code

```
package singlylinkedlist

import (
	"fmt"
)

type node struct {
	data int32
	next *node
}

// SinglyLinkedList is the struct for hold one head of SLL
type SinglyLinkedList struct {
	head *node
}

// New creates a empty singly linked list and returns the reference to it
func New() *SinglyLinkedList {
	return &SinglyLinkedList{
		head: nil,
	}
}

/*
	Insert function creates a node and adds if the head does not exist
	or traverses to the end of the linked list until the last node
	and attaches the new node
*/
func (sll *SinglyLinkedList) Insert(data int32) {
	newNode := &node{
		data: data,
		next: nil,
	}
	if sll.head == nil {
		sll.head = newNode
	} else {
		temp := sll.head
		for temp.next != nil {
			temp = temp.next
		}
		temp.next = newNode
	}
}

//Print prints the linked list
func (sll *SinglyLinkedList) Print() {
	temp := sll.head
	for temp != nil {
		fmt.Printf("%d -> ", temp.data)
		temp = temp.next
	}
	println("NULL")
}

// Length returns the length of the linked list
func (sll *SinglyLinkedList) Length() int32 {
	var count int32 = 0
	temp := sll.head
	for temp != nil {
		count += 1
		temp = temp.next
	}
	return count
}

/*
	defer is a keyword which halts the execution until the rest of the body gets executed.
	In the below function, if the position to be deleted, is more than the
	length of the linked list, then we panic ( quit abruptly causing the program to exit)
	Sometimes, we need to handle and recover from panics and shutdown gracefully.
	The defer statement catches the panic and recovers from it by printing the error.
*/
func (sll *SinglyLinkedList) DeleteAtGivenPosition(position int32) {
	defer func() {
		if err := recover(); err != nil {
			fmt.Println("panic occurred:", err)
		}
	}()
	lengthOfSll := sll.Length()
	if lengthOfSll < position {
		panic("Position out of bound")
	} else {
		if sll.head == nil {
			return
		}

		temp := sll.head
		if position == 1 {
			sll.head = temp.next
			return
		}

		var currentPosition int32 = 1
		for temp != nil {
			if currentPosition+1 == position {
				break
			}
			currentPosition += 1
			temp = temp.next
		}
		if temp.next == nil {
			return
		} else {
			temp.next = temp.next.next
		}
	}
}

func (sll *SinglyLinkedList) Reverse() {
	current := sll.head
	var previous, next *node = nil, nil
	for current != nil {
		next = current.next
		current.next = previous
		previous = current
		current = next
	}
	sll.head = previous
}

``` 


> The above functions have a ( sll *SinglyLinkedList) in between the definition. This is similar to a method of a class in an OOP language. These are called receiver functions in Go.

> Go has implicit interface implementations meaning, we never specifically say that SinglyLinkedList implements the BaseImplementer Interface discussed in previous post rather we implement the methods to the SinglyLinkedList struct and it implicitly conveys that SinglyLinkedList struct type is of type LinkedList BaseImplementer

As usual all the code is up-to date on the [repo](https://github.com/omprakashsridharan/go-data-structures)

We modify the main.go in the root of the project to the below


```
package main

import (
	singlylinkedlist "data-structures/linkedlist/singly-linked-list"
)

func main() {
	sll := singlylinkedlist.New()
	sll.Insert(10)
	sll.Print()
	sll.Insert(20)
	sll.Print()
	sll.Insert(30)
	sll.Print()
	sll.DeleteAtGivenPosition(3)
	sll.Print()
	println("Length of singly linked list: ", sll.Length())
	println("Deleteing node at position 3 which is not existent")
	sll.DeleteAtGivenPosition(3)
	println("Reversing linked list")
	sll.Reverse()
	sll.Print()
	println("Program exited successfully")
}
``` 

## Output

![SllOutput.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606324726316/0eiXmlsKN.png)




