## Data structures using Go: Doubly Linked List

## Doubly Linked List

In the previous post, we implemented the BaseImplementer interface for the Circular Linked List. In this post, we will implement the same for the doubly Linked List. Doubly Linked List differs from Singly Linked List in the fact that each node of DLL will have an extra pointer variable refering to the previous node in addition to the existing next node's address. 

![DLL.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1606568343191/z90AE4QDK.jpeg)

BaseImplementer Interface

```
type BaseImplementer interface {
    Insert(data int32)
    Print()
    DeleteAtGivenPosition(position int32)
    Length() int32
    Reverse()
}
``` 

1. Create a folder "doubly-linked-list" under previously created linked list folder
2. Create a file called doubly-linked-list.go under the above created folder

```
package doublylinkedlist

import (
	"fmt"
)

type node struct {
	data int32
	next *node
	prev *node
}

// DoublyLinkedList is the struct for hold one head of DLL
type DoublyLinkedList struct {
	head *node
}

// New creates a empty doubly linked list and returns the reference to it
func New() *DoublyLinkedList {
	return &DoublyLinkedList{
		head: nil,
	}
}

/*
	Insert function creates a node and adds if the head does not exist
	or traverses to the end of the linked list until the last node
	and attaches the new node
*/
func (dll *DoublyLinkedList) Insert(data int32) {
	newNode := &node{
		data: data,
		next: nil,
		prev: nil,
	}
	if dll.head == nil {
		dll.head = newNode
	} else {
		temp := dll.head
		for temp.next != nil {
			temp = temp.next
		}
		temp.next = newNode
		newNode.prev = temp
	}
}

//Print prints the linked list
func (dll *DoublyLinkedList) Print() {
	temp := dll.head
	if temp == nil {
		return
	}
	for temp != nil {
		fmt.Printf("<- %d -> ", temp.data)
		temp = temp.next
	}
	println()
}

// Length returns the length of the linked list
func (dll *DoublyLinkedList) Length() int32 {
	var count int32 = 0
	temp := dll.head
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
func (dll *DoublyLinkedList) DeleteAtGivenPosition(position int32) {
	defer func() {
		if err := recover(); err != nil {
			fmt.Println("panic occurred:", err)
		}
	}()
	lengthOfdll := dll.Length()
	if lengthOfdll < position {
		panic("Position out of bound")
	} else {
		if dll.head == nil {
			return
		}

		temp := dll.head
		if position == 1 {
			dll.head = temp.next
			dll.head.prev = nil
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
			if temp.next != nil {
				temp.next.prev = temp
			}
		}
	}
}

func (dll *DoublyLinkedList) Reverse() {
	temp := dll.head
	if temp == nil {
		return
	}
	for temp != nil {
		swap := temp.next
		temp.next = temp.prev
		if swap == nil {
			dll.head = temp
		}
		temp.prev = swap
		temp = temp.prev
	}
}
``` 
As usual all the code is up-to date on the [repo](https://github.com/omprakashsridharan/go-data-structures)

We modify the main.go in the root of the project to the below

```
package main

import (
	"data-structures/linkedlist"
	circularlinkedlist "data-structures/linkedlist/circular-linked-list"
	doublylinkedlist "data-structures/linkedlist/doubly-linked-list"
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
	dll := doublylinkedlist.New()
	performInterfaceMethods("Doubly Linked List", dll)
	cll := circularlinkedlist.New()
	performInterfaceMethods("Circular Linked List", cll)
}
``` 
