# Coding Study Guide

## Basic Program

### C++
```cpp
#include <iostream>
using std::cin;
using std::cout;
using std::endl;
int main(int argc, char** argv)
{
    cout << "Hello World!" << endl;
}
```

### Java
```java
package com.mydomain;
public class MyClass
{
    public static void main(String[] args)
    {
        System.out.println("Hello world!!");
    }
}
```

### C# 
```csharp
using System;
class MyClass
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello World!!");
    }
}
```

### Javascript
```javascript
console.log("Hello world!\n");
```

## Types

### C++
* Primitive boolean: bool
* Primitive charaacter: char (8 bits), wchar_t (16+), char16_t (16), char32_t (32)
* Primitive integer: short(16+), int(16+), long(32+), long long(32+); can prefix with "unsigned"
* Primitive floating: float(32+), double(64+), long double (96/128+)
* Fixed length integer types (in <cstdint>): int8_t, int16_t, int32_t, int64_t, uint8_t, uint16_t,
uint32_t, uint64_t.  These are optional, if directly supported by an implementation.  They are in the
std namespace.

### C# 
* Value types: signed integer (sbyte, short, int, long), unsigned integer 
(byte, ushort, uint, ulong), real (float, double, decimal), logical (bool), 
character (char), as well as struct and enum types.
* Reference types: all 
class, array, delegate, and interface types -- including string and object.
You can also use the "var" keyword to have the compiler deduce the type, or 
when you do not know the type.

## Arrays

### C++

In C++, array size must be known at compile time, so size must be a constant expression.

### C# 
Arrays are created with the new keyword, e.g. `int[] myarr = new int[33];`.
When an array is created, it is default initialized, e.g. with 0 / null /
false. Arrays have a Length property.

## Initialization

### C++

In C++, initialization and assignment are conceptually different things.  Also, "declaration" and 
"definition" are conceptually different (but can happen at the same time).

#### Object / class variable initialization
Object/class variables are always initialized when they are defined, whether or not explicit
initialization is given, and regardless of whether they are defined at block scope or outside
of any block.  If no explicit initialization is given, then the no-arg constructor is called. 
If no constructors are explicitly defined, the compiler-generated default synthesized constructor
will be called.  If there is no no-arg constructor, or if it is not accessible, this is an error.
Any member variables of object / class type follow this same process when the object is defined.
Elements of containers of object / class type follow this same process when container is defined.
Elements of an array that are not explicitly initialized follow this same process when the array
is defined.

#### Built-in / primitive type initialization
Built-in / primitive typed variables that are defined outside of any block, as well as static
variables (of built-in or primitive type) that are defined at block scope, and which do not have
explicit initialization are "value initialized" to 0 or false.  This includes when a container
(such as vector) is defined without explicit initialization for its elements -- they are value
initialized.  For arrays that are defined in block scope, there is no

#### Default initialization
"Default initialization" means that all objects will be initialized with no-arg constructor,
built-in / primitive types and array elements will either be undefined (non-static block scope)
or "value initialized" (outside of block or static in-block).

#### Value initialization
"Value initialization" means that all objects will be initialized with no-arg constructor,
built-in / primitive types and array elements will be assigned 0 or false.

#### List initialization
```cpp
int myint{4}; // (A)
int myint = {4}; // Equivalent to A
vector<int> vec{1, 2, 3}; // (B)
vector<int> vec = {1, 2, 3}; // Equivalent to B
```

#### Copy initialization
```cpp
std::string mystr = "hello"; // Copy initialization
MyClass myobj; // Default initialization (no-arg constructor)
MyClass myobj2 = myobj; // Copy initialization (copy assignment operator)
MyClass myobj3(myobj); // Copy initialization (copy constructor)
int myint = 4;
```

#### Direct initialization
```cpp
std::string mystr("hello");
int myint(4);
```

#### Aggregate initialization
```cpp
struct MyAggregate // all members public, no initializers, no constructors, no inheritance
{
	int mem1;
	string mem2;
}
MyAggregate myagg = { 4, "hello" };
```

### C# 
Local variable are not default initialized, but the compiler enforces
that they are initialized before they are used.  All other variables are 
automatically initialized to 0 / null / false.  You can initialize an array
with braces.

```csharp
char[] vowels = new char[] {'a', 'e', 'i', 'o', 'u'};
char[] vowels = {'a', 'e', 'i', 'o', 'u'};
```

## Range For

### C# 
```csharp
foreach (char c in "beer")
```

## Access

### C# 
In C\#, members are private by default.

## Equality and Comparison

### C# 
In C\#, == and != perform value comparison for value types (always). By 
default, they perform reference comparison for reference types, but this
can be changed, e.g. comparing two strings with == or != performs a value
comparison.

## Function parameters

### C# 
In C\#, by default all parameters are passed by value.  However, the ref
and out keywords indicate pass by reference, and must be included both at
the function definition, and at the function call.

## Collections

### C# 
There are generic and nongeneric versions of collections and interfaces.
Generally, the generic versions should be used.  (Generic) collections 
implement the `IEnumerable<T>` interface, which returns an
`IEnumerator<T>`, which has method `bool MoveNext()` and property
`Current`.  `MoveNext()` must be called
before accessing the first element, to account for empty collections.
`List<T>` is the standard list class, with methods
`void Add (T item)` and `void Insert (int index, T item)`, and indexer 
`T this [int index] { get; set; }`.  Other collections include 
LinkedList, Stack, Queue, HashSet,
and SortedSet. Then there is `Dictionary<TKey,TValue>`, 
which has methods Add(key, value), ContainsKey(key), ContainsValue(value), 
and you can also do `foreach (KeyValuePair<TK,TV> kv in d)`.

## String Manipulation

### C# 
In C#, `char`'s are natively stored as 16-bit UTF-16 values. String type is `string`, which is a reference
type.  Operators == and != are overridden to do value comparison (ordinal).  You can access individual characters (as
long as they fit in a single 16-bit character) with [] indexing.  Some useful string methods include 
`StartsWith`, `Substring`, and `Replace`.  `CompareTo` perfoms "culture-sensitive" (non-ordinal) comparison.

## The Stack and the Heap

### C# 
Local variables (value or reference) are created on the stack, however,
the contents of the reference (the objects) are created on the heap.  Static
variables are also created on the heap and are never garbage collected.

## OO / Inheritance

### C# 
Inheritance: `public class DerivedClass : BaseClass {}`. Methods must 
be declared `virtual` to allow subclasses to
override them, and subclasses must use `override` to do so.  Abstract classes
must use abstract keyword on the class and any abstrance methods / properties.
Use `base` and `this` keywords to refer to self and superclass. Create
an interface with `interface` keyword.

## IO and Streams

## Concurrency and Asynchrony

### C# 
Create and run a basic thread with:
```csharp
using System;
using System.Threading;
Thread t = new Thread(SomeDelegate);
t.Start();
```
Join a thread with `t.Join()`. Run a task on a thread from a thread pool 
with:
```csharp
using System.Threading.Tasks;
Task<int> task = Task.Run(() => { Console.WriteLine("Hello World!"); return 0;});
int result = task.Result;
```
Example of asynchronous code:
```csharp
Task<int> DoSomeLongTaskAsync(int param1)
{
	return Task.Run(() => DoTheLongProcess());
}
async void DisplayTheResult()
{
	int result = await DoSomeLongTaskAsync(42);
	Console.WriteLine(result);
}
```
For exclusive locking, use `lock (lockObject)`, where `lockObject` is any reference
object.  For signaling, you can use the `EventWaitHandle`s `AutoResetEvent` and `ManualResetEvent`.
On both of these, you call `WaitOne()` to wait for the signal to proceed, and `Set()` to send a
signal to proceed.  The difference between these two is that `AutoResetEvent` automatically "closes"
after `Set()` is called, only allowing one thread to proceed, whereas `ManualResetEvent` stays "open"
for all threads, until manually closed again.

## Function Pointers / Delegates / Functions as Objects

### C# 
Delegates:
```csharp
// Defining a delegate type (outside of any class).
delegate int MyDelType(int myparam);

// Create a delegate instance:
MyDelType afunc = SomeFunc;

// Alternatively, you could have:
MyDelType afunc = (int x) => x * 3;

// where:
static int SomeFunc(int x) => x * 3;

// Then you can call it like:
int ninevar = afunc(3);
```

## Lambdas / Closures

### C# 
In C#, lambda's are created with:
```csharp
(int x) => x * 3;
(int x) => { x++; return x * 2; }
(x) => x * 3; // if the type of x can be inferred
x => x * 3; // if the type of x can be inferred and there is exactly one parameter
```
C#'s lambdas are full closures, which have dynamic access to enclosing variables, which are evaluated at 
execution time, not definition time, and which can be updated inside the lambda.

## Generics

### C# 
No template keyword, types can be primitive / value types, not limited to reference types.
```csharp
public class MyGen<T>
{
	T info;
	public void setInfo(T info) => this.info = info;
	public T getInfo() => this.info;
}
MyGen<int> mygenint = new MyGen<int>();
```
