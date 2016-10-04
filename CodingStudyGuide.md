# Coding Study Guide

## Basic Program

### C++
```C++
#include <iostream>
using std::cin;
using std::cout;
using std::endl;
int main(int argc, char** argv)
{
    cout << "Hello World!" << endl;
}
```

\begin{minted}{java}
//Java
package com.mydomain;
public class MyClass
{
    public static void main(String[] args)
    {
        System.out.println("Hello world!!");
    }
}
\end{minted}

\begin{minted}{csharp}
//C#
using System;
class MyClass
{
    static void Main(string[] args)
    {
        Console.WriteLine("Hello World!!");
    }
}
\end{minted}

\begin{minted}{js}
// Javascript
console.log("Hello world!\n");
\end{minted}

\section{Types}

C\#: Value types: signed integer (sbyte, short, int, long), unsigned integer 
(byte, ushort, uint, ulong), real (float, double, decimal), logical (bool), 
character (char), as well as struct and enum types.  Reference types: all 
class, array, delegate, and interface types -- including string and object.
You can also use the var keyword to have the compiler deduce the type, or 
when you do not know the type.

\section{Arrays}

C\#: Arrays are created with the new keyword, e.g. int[] myarr = new int[33];.
When an array is created, it is default initialized, e.g. with 0 / null /
false. Arrays have a Length property.

\section{Initialization}

C\#: Local variable are not default initialized, but the compiler enforces
that they are initialized before they are used.  All other variables are 
automatically initialized to 0 / null / false.  You can initialize an array
with braces.
\begin{minted}{csharp}
char[] vowels = new char[] {'a', 'e', 'i', 'o', 'u'};
char[] vowels = {'a', 'e', 'i', 'o', 'u'};
\end{minted}

\section{Range For}

C\#: \mintinline{csharp}{foreach (char c in "beer")}.

\section{Access}

In C\#, members are private by default.

\section{Equality and Comparison}

In C\#, == and != perform value comparison for value types (always). By 
default, they perform reference comparison for reference types, but this
can be changed, e.g. comparing two strings with == or != performs a value
comparison.

\section{Function parameters}

In C\#, by default all parameters are passed by value.  However, the ref
and out keywords indicate pass by reference, and must be included both at
the function definition, and at the function call.

\section{Collections}

C\#: There are generic and nongeneric versions of collections and interfaces.
Generally, the generic versions should be used.  (Generic) collections 
implement the \mintinline{csharp}{IEnumerable<T>} interface, which returns an
\mintinline{csharp}{IEnumerator<T>}, which has method
\mintinline{csharp}{bool MoveNext()} and property
\mintinline{csharp}{Current}.  \mintinline{csharp}{MoveNext()} must be called
before accessing the first element, to account for empty collections.
\mintinline{csharp}{List<T>} is the standard list class, with methods
\mintinline{csharp}{void Add (T item)} and \mintinline{csharp}{void Insert
(int index, T item)}, and indexing \mintinline{csharp}{T this [int index]
{ get; set; }}.  Other collections include LinkedList, Stack, Queue, HashSet,
and SortedSet. Then there is \mintinline{csharp}{Dictionary<TKey,TValue>}, 
which has methods Add(key, value), ContainsKey(key), ContainsValue(value), 
and you can also do \mintinline{csharp}{foreach (KeyValuePair<TK,TV> kv 
in d)}.

\section{String Manipulation}

\section{The Stack and the Heap}

C\#: Local variables (value or reference) are created on the stack, however,
the contents of the reference (the objects) are created on the heap.  Static
variables are also created on the heap and are never garbage collected.

\section{OO / Inheritance}

C\#: Inheritance: \mintinline{csharp}{public class DerivedClass : 
BaseClass {}}. Methods must be declared virtual to allow subclasses to
override them, and subclasses must use override to do so.  Abstract classes
must use abstract keyword on the class and any abstrance methods / properties.
Use "base" and "this" keywords to refer to self and superclass. Create
an interface with "interface" keyword.

\section{IO and Streams}

\section{Concurrency and Asynchrony}

C\#: Create and run a basic thread with:
\begin{minted}{csharp}
using System;
using System.Threading;
Thread t = new Thread(SomeDelegate);
t.Start();
\end{minted}
Join a thread with \mintinline{csharp}{t.Join()}. Run a task on a 
thread from a thread pool with:
\begin{minted}{csharp}
using System.Threading.Tasks;
Task<int> task = Task.Run(() => { Console.WriteLine("Hello World!"); return 0;});
int result = task.Result;
\end{minted}
Example of asynchronous code:
\begin{minted}{csharp}
Task<int> DoSomeLongTaskAsync(int param1)
{
	return Task.Run(() => DoTheLongProcess());
}
async void DisplayTheResult()
{
	int result = await DoSomeLongTaskAsync(42);
	Console.WriteLine(result);
}
\end{minted}

\end{document}





