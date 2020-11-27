## Data structures using Go: Circular Linked List

# Circular Linked List

In the previous post, we implemented the BaseImplementer interface for the Singly Linked List. In this post, we will implement the same for the Circular Linked List. Circular Linked List differs from Singly Linked List in the fact that the last node of CLL will now point to the head node rather than null.

![CLL.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1606495375323/4SU050L9X.jpeg)

 Let us implement the interface methods for circular linked list.


```
type BaseImplementer interface {
	Insert(data int32)
	Print()
	DeleteAtGivenPosition(position int32)
	Length() int32
	Reverse()
}
``` 


1. Create a folder "circular-linked-list" under previously created linked list folder
2.Create a file called circular-linked-list.go under the above created folder


```
package circularlinkedlist

import (
	"fmt"
)

type node struct {
	data int32
	next *node
}

// CircularLinkedList is the struct for hold one head of cll
type CircularLinkedList struct {
	head *node
}

// New creates a empty singly linked list and returns the reference to it
func New() *CircularLinkedList {
	return &CircularLinkedList{
		head: nil,
	}
}

/*
	Insert function creates a node and adds if the head does not exist
	or traverses to the end of the linked list until the last node
	and attaches the new node
*/
func (cll *CircularLinkedList) Insert(data int32) {
	newNode := &node{
		data: data,
		next: nil,
	}
	if cll.head == nil {
		cll.head = newNode
		newNode.next = cll.head
	} else {
		temp := cll.head
		for temp.next != cll.head {
			temp = temp.next
		}
		temp.next = newNode
		newNode.next = cll.head
	}
}

//Print prints the linked list
func (cll *CircularLinkedList) Print() {
	temp := cll.head
	if temp == nil {
		return
	}
	if temp.next == cll.head {
		fmt.Printf("%d -> ", temp.data)
	}
	for temp.next != cll.head {
		fmt.Printf("%d -> ", temp.data)
		temp = temp.next
	}
	fmt.Printf("%d -> ", temp.data)
	println("HEAD")
}

// Length returns the length of the linked list
func (cll *CircularLinkedList) Length() int32 {
	var count int32 = 1
	temp := cll.head
	if temp == nil {
		return 0
	}
	for temp.next != cll.head {
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
func (cll *CircularLinkedList) DeleteAtGivenPosition(position int32) {
	defer func() {
		if err := recover(); err != nil {
			fmt.Println("panic occurred:", err)
		}
	}()
	lengthOfcll := cll.Length()
	if lengthOfcll < position {
		panic("Position out of bound")
	} else {
		if cll.head == nil {
			return
		}

		temp := cll.head
		if position == 1 {
			secondNode := temp.next
			if secondNode == cll.head {
				cll.head = nil
				return
			}
			for temp.next != cll.head {
				temp = temp.next
			}
			temp.next = secondNode
			cll.head = secondNode
			return
		}

		var currentPosition int32 = 1
		for temp.next != cll.head {
			if currentPosition+1 == position {
				break
			}
			currentPosition += 1
			temp = temp.next
		}
		if temp.next == cll.head {
			temp.next = cll.head.next
			cll.head = cll.head.next
		} else {
			temp.next = temp.next.next
		}
	}
}

func (cll *CircularLinkedList) Reverse() {
	if cll.head == nil {
		return
	}
	current := cll.head
	originalHead := cll.head
	var previous, next *node = nil, nil
	for current.next != cll.head {
		next = current.next
		current.next = previous
		previous = current
		current = next
	}
	current.next = previous
	cll.head = current
	originalHead.next = current
}
``` 
As usual all the code is up-to date on the [repo](https://github.com/omprakashsridharan/go-data-structures)

We modify the main.go in the root of the project to the below


```
package main

import (
	"data-structures/linkedlist"
	circularlinkedlist "data-structures/linkedlist/circular-linked-list"
	singlylinkedlist "data-structures/linkedlist/singly-linked-list"
	"fmt"
)

func performInterfaceMethods(listType string, ll linkedlist.BaseImplementer) {
	fmt.Printf("--- %s ---", listType)
	println()
	ll.Insert(10)
	ll.Print()
	ll.Insert(20)
	ll.Print()
	ll.Insert(30)
	ll.Print()
	ll.Insert(40)
	ll.Print()
	println("Length of singly linked list: ", ll.Length())
	println("Deleteing node at position 4")
	ll.DeleteAtGivenPosition(4)
	ll.Print()
	println("Reversing linked list")
	ll.Reverse()
	ll.Print()
	println("Deleteing node at position 5 which is not existent")
	ll.DeleteAtGivenPosition(5)
	ll.Print()
	println()
	println()
}

func main() {
	sll := singlylinkedlist.New()
	performInterfaceMethods("Singly Linked List", sll)
	cll := circularlinkedlist.New()
	performInterfaceMethods("Circular Linked List", cll)
}
``` 

> Notice that we have a created a function **performInterfaceMethods** that takes an linked list of type BaseImplementer. Since we have satisfied the base implementer contract both for Singly Linked List and Circular Linked List, we can pass both of them as input and call the methods of the interface, thereby having multiple implementations based on the business needs. 


