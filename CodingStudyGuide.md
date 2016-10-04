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

### C# 
Value types: signed integer (sbyte, short, int, long), unsigned integer 
(byte, ushort, uint, ulong), real (float, double, decimal), logical (bool), 
character (char), as well as struct and enum types.  Reference types: all 
class, array, delegate, and interface types -- including string and object.
You can also use the var keyword to have the compiler deduce the type, or 
when you do not know the type.

## Arrays

### C# 
Arrays are created with the new keyword, e.g. `int[] myarr = new int[33];`.
When an array is created, it is default initialized, e.g. with 0 / null /
false. Arrays have a Length property.

## Initialization

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

# The Stack and the Heap

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




