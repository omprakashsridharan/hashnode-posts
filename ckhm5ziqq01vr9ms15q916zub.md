## Go: Data-types

# Data-Types

Go is a statically typed language meaning all the variables defined in the code will have a type either implicit or explicit. Like every programming language, go has Basic data types ( primitive ) and Composite data types.

## Basic data types

### Integers

1. int - platform dependent ( 32 bit machines will have 32 bits int and 64 bit machines will have 64 bits )
2. int8 - 8 bits
3. int16 - 16 bits
4. int32 - 32 bits
5. int64 - 64 bits
6. uint - unsigned integer
7. uint8 - 8 bits
8. uint16 - 16 bits
9. uint32 - 32 bits
10. uint64 - 64 bits


> Note: int32 / int is sufficient for most of the use cases and takes care of the allocation, but the above types will be useful for optimising the memory usage of the go application.


> int variants have range from negative to positive values while uint variants start from 0 and contains only positive numbers

### Floats

1. float32 - 32 bits ( Uses single-precision floating point format to store values )
2. float64 - 64 bits ( Uses a double-precision floating-point format to store values )

### Complex Numbers

1. complex64 Both real and imaginary part are float32
2. complex128 Both real and imaginary part are float64

### Byte

Byte in Go is an alias for uint8 meaning it is an integer value. This integer value is of 8 bits and it represents one byte i.e number between 0-255). A single byte therefore can represent ASCII characters. Golang does not have any data type of ‘char’. If we don’t specify the type, then the default type is meant as a **rune**.

### Rune

Rune in Go is  an alias for int32 meaning it is an integer value. This integer value is meant to represent a Unicode Code Point. Unicode is a superset of ASCII characters which assigns a unique number to every character that exists. This unique number is called Unicode Code Point.

Ex: 0 is represented as Unicode point U+0030 ( Hexadecimal representation ). The decimal value is ( 0*16 pow 1 + 3*16 pow 1 = 0 + 48 = )  48.

Click [here](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to know more about Unicode Point. 

> In GO every string is encoded using utf-8

### String

String is a read only slice of bytes in golang. String can be initialized in two ways

using double quotes “” eg “this”
string in double quotes honors the escape sequences. For eg if the string contains a \n then while printing there will be a new line

using back quotes ` eg  \`this`
String in back quotes is just a raw string and it does not honor any kind of escape sequences.

### Booleans

The data type is bool and has two possible values true or false.

## Composite Types

Composite types are a composition of multiple heterogenous or homogeneous primitive types. They can be further divided into Non-Reference and Reference types.

In Non-Reference types, copy of the data type is made and in reference types, the memory address of the data type variable is being used.

### Arrays ( Non-Reference )

Arrays are fixed-length sequences of the same type. They are just values and not references and what it means is that, if we assign an array variable to a new variable, a new copy of the array is created rather than the address of the array being referenced like being done in python or any OOP language. Arrays have fixed length.

### Structs ( Non-Reference )

Struct is one of the most important data type which is the base for all the custom types that we create to represent our business entity with. They contain heterogeneous types of data and we will be using them more often than not in go.

### Slices ( Reference )

Slices are dynamically sized, reference into the elements of an array. As mentioned above arrays are of fixed size, so slices give a more flexible interface to arrays. A slice is a reference type as it internally references an array. We will be using slices more often than arrays due to the flexible nature of slices. The built in Go functions append is used to add more values to the slice pointed array. Slice by itself is a bigger topic and it is highly suggested to have a good understanding of slices. Reference:  [Slice](https://medium.com/rungo/the-anatomy-of-slices-in-go-6450e3bb2b94) 

### Maps ( Reference )

Maps are similar to a dictionary in Python, Hashmap in Java which holds key-value pairs and can be referred in O(1) time.

### Functions ( Reference )

In Go function are values and can be passed around like a value. Basically, function can be used as first-order objects and can be passed around. A function has a name, arguments and returns values.

# Conclusion

These cover most of the data types in Go and I have not mentioned few like pointers, channels, nil for the simplicity for the initial learnings but will be covered as and when the need arises. Interfaces are constructs that gives the flexibility of data structure design in Go and will be dealt with later in future articles.









