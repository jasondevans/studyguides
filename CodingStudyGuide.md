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

## Console input / output

### C# 
Console input/output uses the `System.Console` class.  There are two properties that represent standard
input and output -- `Console.In` (standard input stream as a `System.IO.TextReader`), and `Console.Out`
(standard output stream as a `System.IO.TextWriter`).  These two properties can be used directly, but
typically, methods defined directly in the `Console` class are called.  In particular, 
`Console.ReadLine()` reads one line, or `null` if no more lines are available.  `Console.Write()` and
`Console.WriteLine()` write to standard output, with many arguments -- typically with a `string`, but
there are overloads that accept many different types to write out.

## Parsing and Conversions

### C# 
```csharp
int i = int.Parse("1234"); // Throws an exception if not a valid int.
bool success = int.TryParse("1234", out i); // Returns false if conversion failed.
bool b = bool.Parse("True");
double d = double.Parse("1.234"); // etc.
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
initialized.  For arrays that are defined in block scope without explicit initialization, there
is no initialization performed (I believe).

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
MyClass myobj2 = myobj; // Copy initialization (copy constructor)
MyClass myobj3(myobj); // Copy initialization (copy constructor)
myobj2 = myobj3;  // Copy initialization (copy assignment operator)
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

### C++
```cpp
std::string mystr("hello");
for (char c : mystr) {} // or, for (auto c : mystry)
std::vector<int> myvec { 1, 2, 3, 4 };
for (auto elem : myvec) {} // elem takes on copies of the elements in myvec
for (auto &elem : myvec) {} // elem takes on references to the elements in myvec (and can modify them)
```

### C# 
```csharp
foreach (char c in "beer")
```

## Access

### C++
In C++, members of `struct` are public by default, and members of `class` are private by default.

### C# 
In C\#, members are private by default.

## Equality and Comparison

### C++
In C++, == and != are by default not defined for objects, but you can overload these and the relational
operators to provide that functionality.  For example, these are overloaded for `string`.

### C# 
In C\#, == and != perform value comparison for value types (always). By 
default, they perform reference comparison for reference types, but this
can be changed, e.g. comparing two strings with == or != performs a value
comparison.

## Function parameters

### C++
In C++, by default all parameters are passed by value.  For primitive types, this is a straightforward
copy.  For arrays, a copy of the pointer to the first element is passed.  For class types, the copy
constructor is called to create the copy.  To pass by reference, indicate that the parameter is a 
reference (with &).

### C# 
In C\#, by default all parameters are passed by value.  However, the ref
and out keywords indicate pass by reference, and must be included both at
the function definition, and at the function call.

## Collections / Containers

### C++ 
* Sequential containers include: vector, deque, list, forward_list, array, string
* Associative containers include: map, set, multimap, multiset (and unordered versions)
* `vector` is the most popular  

Basic `vector` methods include:
* `size()`: number of elements
* `begin()`: iterator to first element
* `end()`: iterator to one past last element
* [Prepend 'c' to get const iterators, 'r' for reverse, 'cr' for both]
* `push_back(element)`: append element
* `push_front(element)`: prepend element
* `myvec[n]`: reference to element at position n
* `insert(args)`: insert element at specific position
* `empty()`: whether there are no elements

Examples:
```cpp
vector<int> myvec;  // Empty vector
vector<int> myvec { 1, 2, 3 }; // or = { 1, 2, 3 }
for (auto iter = myvec.begin(); iter != myvec.end(); iter++) // old-school way to do it
{
	*iter += 10;
}
for (auto &elem : myvec) elem += 10; // easier way to do it -- make sure you use a reference, or you'll get a copy
```

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

### C++
C++ inherits C's null-terminated character array format for strings, but prefers its own `std::string` type.
Equality and relational operators are overloaded to compare string values.  Strings can be concatenated with +.
Strings are not immutable.  There are many issues around strings and encodings -- char sizes are implementation-
dependent, most string methods are unaware of UTF-8, and string indexing could land in the middle of a code point
and/or not correspond to number of characters.
```cpp
using std::string;
using std::cout;
using std::cin;
using std::endl;
string s = "hello";
cout << s << endl;
cin >> s; // Read in a whitespace-separated string
getLine(cin, s);  // Read in a full line
s.empty();
s.size();  // length of the string
char c = s[0]; // individual character by index
```

### C# 
In C#, `char`'s are natively stored as 16-bit UTF-16 values. String type is `string`, which is a reference
type.  Operators == and != are overridden to do value comparison (ordinal).  You can access individual characters (as
long as they fit in a single 16-bit character) with [] indexing.  Some useful string methods include 
`StartsWith`, `Substring`, and `Replace`.  `CompareTo` perfoms "culture-sensitive" (non-ordinal) comparison.
```csharp
string s1 = "Hello world!\n"; // Create a string
string s2 = @"Hello \n\r\t\\hello she said ""hi""."; // Verbatim string, no escape characters except "" for double quote.
int x = 5;
string s3 = $"The value is {x}."; // Interpolated string, any expression inside braces.
string s4 = new string(s1); // string constructor.
bool isStringEmpty = "".Empty; // True
int strLen = s1.Length; // String length.
bool isPrefix = "12345".StartsWith("12"); // True
int patternLoc = s1.IndexOf("world"); // 6
patternLoc = s1.IndexOf("o", 5); // 7, index of pattern starting at specified index
string helloStr = "Hello world!".Substring(0, 5); // "hello"
string remainderStr = "Hello world!".Substring(5); // " world!"
string insertedStr = "onethree".Insert(3, "two"); // "onetwothree"
string trimStr = "     \tWhat up  \r\n\t  ".Trim(); // "What up"
string[] indivWords = "one two three".Split(); // { "one", "two", "three" }
indivWords = "one&two|three".Split("|", '&'); // { "one", "two", "three" }
string backTogether = indivWords.Join("--"); // "one--two--three"
bool areSame = "one" == "one"; // True
int compareResult = "James".CompareTo("Jim"); // -1
compareResult = "James".CompareTo("James"); // 0
StringBuilder sb = new StringBuilder(); // Create new string builder
sb.Append("one"); sb.Append(" two");
string builtStr = sb.ToString(); // "one two"
```

## The Stack and the Heap

### C++
C++ does not require there to even be a stack or heap, but in practice, local variables are created on the stack
and variables initialized with `new` are created on the heap.  Individual classes can control internal memory
allocation however they want, for example, `vector` typically stores its elements on the heap, even if it's 
header information is on the stack.  Arrays with `new` are created on the heap, otherwise they are on the stack.

### C# 
Local variables (value or reference) are created on the stack, however,
the contents of the reference (the objects) are created on the heap.  Static
variables are also created on the heap and are never garbage collected.

## Pointers / References

## OO / Inheritance

### C++
In C++, there are many details, too much to discuss fully here.  Here are some examples:
```cpp
class MyTestClass
{
public:
	MyTestClass() : myint(0), mystr("") {}  // Constructor with initializations
	MyTestClass(int paramint, string paramstr) : myint(paramint), mystr(paramstr) {} // Constructor with args
	MyTestClass(const MyTestClass& rhs) : myint(rhs.myint), mystr(rhs.mystr) {} // Copy constructor
	MyTestClass& operator=(const MyTestClass& rhs) {  // Copy assignment operator
		myint = rhs.myint; mystr = rhs.mystr; return *this; }
	virtual void printme() const {  // Member function
		std::cout << "myint is " << myint << ", mystr is " << mystr << endl; }
	virtual ~MyTestClass() { } // Destructor
private:
	int myint;
	string mystr;
};

class MySubClass : public MyTestClass
{
public:
	MySubClass() : MyTestClass(), mydbl(0.0)  {}  // Constructor with initializations
	MySubClass(int paramint, string paramstr, double paramdbl)  // Constructor with args
		: MyTestClass(paramint, paramstr), mydbl(paramdbl) {}
	MySubClass(const MySubClass& rhs)  // Copy constructor
		: MyTestClass(rhs), mydbl(rhs.mydbl) {} 
	MySubClass& operator=(const MySubClass& rhs) {  // Copy assignment operator
		MyTestClass::operator=(rhs); mydbl = rhs.mydbl; return *this; }
	virtual void printme() const {  // Member function
		MyTestClass::printme();
		std::cout << "mydbl = " << mydbl << endl; }
	virtual ~MySubClass() { } // Destructor
private:
	double mydbl;
};
```

### C# 
Inheritance: `public class DerivedClass : BaseClass {}`. Methods must 
be declared `virtual` to allow subclasses to
override them, and subclasses must use `override` to do so.  Abstract classes
must use abstract keyword on the class and any abstrance methods / properties.
Use `base` and `this` keywords to refer to self and superclass. Create
an interface with `interface` keyword.

## IO and Streams

## Concurrency and Asynchrony

### C++
"High level", attempt to run a task on another thread via async / futures:
```cpp
#include <string>
#include <iostream>
#include <future>
#include <thread>
int main(int argc, char** argv)
{
	// May or may not actually start another thread here, depending on platform capabilities.
	std::future<int> myResult { std::async([](int val) { return val * 2; } , 6) };
	// ... do other work here.
	// Next line gets result if completed, or waits for completion, or starts thread synchronously
    // if unable to start asynchronously above.  If an exception was thrown, calling get() rethrows the
	// exception here. 
	cout << "Result is " << myResult.get() << endl; 
}
```
"Lower level", starting a thread directly:
```cpp
int result = 0;
// Of course, not typically the best way to return a value; you must handle inter-thread communication
std::thread t{ [&result](int val) {result = val * 2; }, 6 }; 
// ... do something else here (not using result)
t.join();
cout << "Result is " << result;
```
Also, you can use `promise` to return results and exceptions from one thread to another.
Also, there are mutexes, which can be locked and unlocked, particularly `std::mutex` (standard
mutex) and `std::recursive_mutex` (reentrant mutex).  Typically, you will use these with a
lock guard such as `std::lock_guard`, which uses RAII to ensure that the mutex is unlocked when
the lock guard goes out of scope, even if an exception is thrown.  You can also use `std::unique_lock`,
which has all the functionality of `lock_guard` but also allows you to explicitly lock and unlock the
mutex manually.  Condition variables, `std::condition_variable` have methods `wait()`, `notify_one()`,
and `notify_all()`.  Finally, there are atomics, with `std::atomic<type>`, with methods `store()`
and `load()`.

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

## Function Pointers / Delegates / Functions as Objects / Callable Objects

### C++
C++ has a number of callable objects: functions, pointers to functions, types with the call operator `()`
overloaded, and lambdas.

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

### C++
Example C++ lambda:
```cpp
auto mylambda = [] (int x) { return x * 3; };
```
You can capture local non-static variables by placing them in the `[]`, can capture either
by value or by reference.  Values are captured at the time the lambda is defined, not when 
it is executed.  For any captured references, you must make sure that the referred to variable
is still alive when the lambda is executed (unlike in C#, where referred to variables will have
their lifetime extended to as long as needed, even if they are local and have gone out of scope).

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

## Generics / Templates

### C++
There are function templates and class templates:
```cpp
// Function template definition
template <typename T> T myTemplateFn(T param1, T param2) { /* do something... */ return param1; };
// Then later...
myTemplateFn(4, 5);  // Compiler infers type.
myTemplateFn<int>(4, 5);  // Explicitly indicate type.

// Class template definition
template <typename T> class MyTemplateClass { public: T data; };
// Then later...
MyTemplateClass<int> mtc;
mtc.data = 7;
```

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

## Values, References, Pointers, Memory Management, Garbage Collection
