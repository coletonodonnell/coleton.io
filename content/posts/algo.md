---
author: "Coleton O'Donnell"
title: "Data Structures and Algorithms Notes"
date: "2022-07-01"
description: "These are my notes for Data Structures and Algorithms. Current notes are for Abdul Bari's excellent DSA Udemy Course, but will include COP3530 at UF whenever I take it next semester."
tags: ["math", "algorithms", "programming"]
math: true
---

# Introduction

These notes are on the COP3530 Data Structures and Algorithm class with the excellent Professor Kapoor at the University of Florida as well as on [Abdul Bari's DSA Course on Udemy](https://www.udemy.com/course/datastructurescncpp). What I have learned from each has been compounded into one living document. If you are interested in Abdul Bari's course but want a bit of a taste for it, there is also a free YouTube version that is [consolidated](https://youtube.com/playlist?list=PLDN4rrl48XKpZkf03iYFl-O29szjTrs_O). Please note that these are **notes**, I can't stress this enough. These are written with prior knowledge in mind, and are basically useless if you aren't following along with a textbook or a course. They won't be teaching you well. These can act as a good reference for concepts and important explanations. Think of it as a TL;DR on things, but you're doing yourself a disservice if you even think of using these as your main source of info. For textbooks, check out the excellent [OpenDSA Book](https://opendsa-server.cs.vt.edu/ODSA/Books/Everything/html/index.html). If you prefer paper, check out "Introduction to Algorithms" by Cormen & Leiserson and "Data Structures and Algorithm Analysis in C++" by Weiss.

## Definition of the Data Structure and the Algorithm

* What is a Data Structure?
  
  * A **data structure** can be defined as the arrangement of a collection of data items so that they can be utilized efficiently. It is all about data and the operations of the data.

* What is an Algorithm?
  
  * An **algorithm** can be defined as a procedure used for solving a problem or performing a computation. It is a fininte set of instructions to execute a task. All algorithms have an input, an output, and are definite and unambiguous. This means that they always have the same output for a given input.

## Algorithm vs. Program

|                         | Algorithm           | Code or Program      |
| ----------------------- | ------------------- | -------------------- |
| Focus                   | Design              | Implement a Solution |
| Form                    | Psuedocode          | Language Specific    |
| Dependence on H/W or OS | No                  | Yes                  |
| Cognitive State         | Thinking            | Doing                |
| Correctness/Performance | Mathematical Proofs | Test Cases           |

Algorithms focus more on how to solve versus programs which is how we implement the solution.

## Multiple Solutions to a Problem

The proverb "more than one way to skin a cat" holds very true here, and there is definitely some more efficient ways to solve a problem. This is the difference between solutions, some are **naïve**, or silly, whereas others are more artful, or better. For instance, imagine we are given this objective:

* Determine if a sorted array contains any duplicates.

One possible solution is to compare every element to every other following element so as to create pairs, and if a pair shares identical elements, then there is a duplicate. The issue with this solution is that it is not taking full advantage of the **characteristics** of the data it has been given. Note that this array is **sorted.** This means that another, much better solution, is to compare each value with the value immediately proceeding it. Because it is sorted, duplicates will be right next to each other! Each solution yields the same result, but our latter solution is much more efficient. So this yields a very important question? Are all algorithms equal in terms of performance? And if not, how do we evaluate performance in a meaningful way?

## What is Performance and Why Should We Care?

Performance for algorithms is defined in terms of **time** and **space.** These will be discussed later. Algorithm analysis is important for a few reasons. For one, it allows us to think critically about what we are creating, and as a result allows us to find the best solution to a problem. It also allows us to sell a product, if we can boast that our product is the best because of its performance, it'll sell more. Performant algorithms also cost less to run, it might seem negligable at first, but faster algorithms save time, and time is money. In some cases, a solution to an issue with certain data sets can take 30 seconds, or a year. 

## How to Measure Performance?

It is great that we know the importance of performance, but what are some ways that we can truly understand performance in a meaningful way? 

### Approach 1: Simulation with Timing

A logical way of checking performance is to just time two solutions, and then compare the times. 

Code #1:

```cpp
auto t1 = Clock::now();
for (int i=0; i < 1000; i++);
auto t2 = Clock::now();
```

Code #2

```cpp
auto t1 = Clock::now();
for (long i = 0; i < 1000000; i++);
auto t2 = Clock::now();
```

Looking at the difference between `t2` and `t1` for each snippet:

* Code 1: 1873 nanoseconds
* Code 2: 1644295 nanoseconds

The pros of timing is that it is easy to measure and interpret. The cons are that results vary across machines, compilers, and implementations. It isn't predictable for smaller inputs. There isn't a clear relationship between input and time.

### Approach 2: Modeling by Counting

Instead of counting time, we count the number of operations there are:

```cpp
int sum = 0;
for (int i = 0; i < n; i++)
    sum += i;
std::cout << sum;
```

| Operation           | Symbolic Count |
| ------------------- | -------------- |
| `int sum = 0;`      | 1              |
| `int i = 0;`        | 1              |
| `i < n;`            | $0..n = n + 1$ |
| `i++`               | $n$            |
| `sum += i;`         | $n$            |
| `std::cout << sum;` | 1              |
| $T(n)$              | $3n + 4$       |

The pros of counting is that it is independent of the computer and its input dependence is captured in modeling. The cons is that there is no formal definition of which operation to count, and it is tedious to compute. Also results still vary across implementation and it doesn't really tell you the time.

### Approach 3: Asymptotic Behavior: Order of Growth

An order of growth are functions whose asymptotic behavior is seen as equivalent. For example, $8n$, $100n$, and $n + 1$ all fall into the same order of growth, $n$. The major order of growths that algorithms follow with inputs are:

| Inputs: $n$ | $O(1)$, Constant | $O(\log n)$, Logarithmic | $O(n)$, Linear | $O(n \log n)$, Linearithmic | $O(n^2)$, Quadratic | $O(n^3)$, Cubic | $O(2^n)$, Exponential | $O(n!)$, Factorial |
|:-----------:|:----------------:|:------------------------:|:--------------:|:---------------------------:|:-------------------:|:---------------:|:---------------------:|:------------------:|
| 1           | 1                | 0                        | 1              | 0                           | 1                   | 1               | 2                     | 1                  |
| 10          | 1                | 3                        | 10             | 30                          | 100                 | 1000            | 1024                  | 3628800            |
| 100         | 1                | 7                        | 100            | 700                         | 10000               | 1000000         | 1.26765E+30           | 9.3326E+157        |
| 1000        | 1                | 10                       | 1000           | 10000                       | 1000000             | 1E+9            | 1.0715E+301           | Too Big            |
| 10000       | 1                | 13                       | 10000          | 130000                      | 1E+8                | 1E+12           | Too Big               | Too Big            |
| 100000      | 1                | 17                       | 100000         | 1700000                     | 1E+10               | 1E+15           | Too Big               | Too Big            |
| 1000000     | 1                | 20                       | 1000000        | 20000000                    | 1E+12               | 1E+18           | Too Big               | Too Big            |
| 10000000    | 1                | 23                       | 10000000       | 230000000                   | 1E+14               | 1E+21           | Too Big               | Too Big            |
| 100000000   | 1                | 27                       | 100000000      | 2700000000                  | 1E+16               | 1E+24           | Too Big               | Too Big            |

This can be further illustrated by:

![How to find time complexity of an algorithm?  Adrian Mejia Blog](https://adrianmejia.com/images/time-complexity-examples.png)

So if we return to the example in Approach 2, we note that $T(n) = 3n + 4$. How would we express the time complexity of this algorithm utilizing order of growth? This can be done with the **Big O** notation, which represents the **upper bound** of a function's growth rate. There are other notations that describe other aspects of a function, but for the sake of algorithm performance, Big O is usually what is considered. In this way, Big O notation represents the **worst case** of an algorithm. Let's look at how these notation sare formally defined and how to use them to describe the performance of an algorithm.

## Asymptotic Analysis (Time Complexity)

Asymptotic Analysis (aka. asymptotics) is a mathematical method to describe the limiting behavior of functions. For instance, imagine we are considering a function $f(x) = x^2 + 3x$, as $x \rightarrow \infin$, the term $3x$ becomes more and more insignificant when compared to the term $x^2$. In this way, it is said that $f(x)$ is *asymptotically equivalent to $x^2$* as $x \rightarrow \infin$. In Computer Science, we are especially interested in asymptotic analysis because it allows us to analyze algorithms in a meaningful and quantifiable way.

### Notation

#### Big O

Let $T(n)$, $f(n)$ be functions. Therefore, $T(n) \in O(f(n))$ if there exists two positive constants $n_0$ and $M$ such that $T(n) \le Mf(n)$ for all $n \ge n_0$. Formally speaking, this is a more restrictive definition that is of most concern to us as Computer Scientists, but if you are interested in other definitions check out [the formal definition for Big O notation here.](https://en.wikipedia.org/wiki/Big_O_notation#Formal_definition) With this definition, a function $T(n) = n$ will yield $T(n) \in O(n!)$, but although true, isn't terribly useful. As a result, when figuring out the Big O of a function, it is best to figure out the tightest upperbound, so in the previous case, $T(n) \in O(n)$. Taking a look at our example from Approach 2, $T(n) = 3n+4$. When considering this, what should the value $M$ be? The easiest way to do this is to set $M$ to equal each of the integers in the function, so $M = 3 + 4 = 7$, and we set $n_0 = 0$. So, $3n+4 \le 7n$ for all $n > 1$, so $T(n) \in O(n)$. The function $f(n)$ always acts as an upper bound on performance, and $T(n)$ will grow no faster than the constant $M$ times $f(n)$.

#### Big Ω

Let $T(n), g(n)$ be functions. Therefore, $T(n) \in \Omega(g(n))$ if there exists two positive constants $n_0$ and $M$ such that $T(n) \ge Mg(n)$ for all $n \ge n_0$. Similar to Big O, this means that when $T(n) = n^3$, $T(n) \in \Omega(1)$, but that isn't useful. So, whenever you figure out the Big Ω of a function, find the tightest lowerbound, so in the previous case, $T(n) \in \Omega(n^3)$. The function $g(n)$ always acts as a lower bound on growth rate of $T(n)$, and $T(n)$ will grow no slower than the constant $M$ times $g(n)$.

#### Big Θ

Let $T(n), g(n)$ be functions. Therefore, $T(n) \in \Theta(g(n))$ if $T(n) = O(g(n))$ and $T(n) = \Omega(g(n))$. Another way of expressing it is $T(n) \in \Theta(g(n))$ if there exists two positive constants $n_0$ and $M$ such that $Mg(n) \le T(n) \le Mg(n)$ for all $n \ge n_0$. This function represents the upper *and* lower bound on the growth rate of $T(n)$.

### Rules

The rules for Asymptotic Analysis are pretty simple, but are incredibly important to learn.

1. Addition (Independence): $T(n) = O(n+m)$

Given different parts of an algorithm, their time complexities can be added:

```cpp
void my_function(int n, int m)
{
    for (int i = 0; i < n; i++)
        // Do stuff

    for (int i = 0; i < m; i++_
        // Do more stuff
}
```

The time complexity of lines 3 and 4 is $O(n)$ and the time complexity of lines 6 and 7 is $O(m)$, the time complexity for this algorithm is $O(n+m)$

2. Drop Constant Multipliers: $T(n) = O(n+n) = O(2n) = O(n)$

Given the following algorithm:

```cpp
void my_function(int n)
{
    for (int i = 0; i < n; i++)
        // Do stuff

    for (int i = 0; i < n; i++_
        // Do more stuff
}
```

Lines 3 and 4 is $O(n)$ and lines 6 and 7 are $O(n)$, which is $O(n+n) = O(2n) = O(n)$

3. Always Differentiate Input Variables

Using the algorithm from Rule #1, we would never write the time complexity as $O(n)$ or $O(m)$, but always $O(n + m)$ unless there is an indication of a relationship between the variables given.

4. Dropping Lower Order Terms

Given the following algorithm:

```cpp
void my_function(int n, int m)
{
    for (int i = 0; i < n; i++)
        // Do stuff

    for (int j = 0; j < m; j *= 2)
        // Do stuff
}
```

Lines 3 and 4 is $O(n)$ and lines 6 and 7 are $O(log_2 m)$, thus the time complexity for this algorithm is $O(n + log_2 m))$. Now, if we were told that $n$ and $m$ grow at the same rate, then $O(n + log_2 m) = O(n)$. This is because we drop the lowest order term whenever variables grow at the same rate, or they are identical variables. 

### Cases

Algorithms that have a purpose that allows them to stop their process (eg. searching algorithms, they stop once they find what they are looking for) due to a condition have different cases. These are the best case, average case, and worst case. The best case is the lowest cost, average case is the average cost for all n, and worst case is the highest possible cost.   

## Stack and Heap

### What is the Stack?

In a stack, memory is allocated in blocks that are of fixed size. Accessing this data is fast, and the (de)allocation is handled by the compiler entirely. The stack is preffered when possible, as it is safer to work with as it is thread safe, and it costs less to use. Memory is always temporary in the stack. The cons are that it isn't dynamic, so everything that lives in the stack must be predefined in size.

### What is the Heap?

In a heap, memory is allocated in random order in dynamic size. In other words, it isn't fixed and the size of what is stored on there can be changed. The heap is slow and costs a lot, but it is very flexable.

## What is an Abstract Data Type?

A data type consists of its representation and its operation. The 
representation is what it actually is and how it is implemented. The 
operation portion is what can be done with the data. In other words, the
 representation is the technical details of a data type, and the 
operation is what we can actually do with it. An Abstract Data Type is a
 Data Type where the operation is known, but the representation is not. A
 real life example is a book, a book is Abstract, but a Telephone Book 
is a representation. We will look at all of these Logical Data 
Structures as ADT first, so we can understand them, and then we can 
delve into how they work.

## Physical and Logical Data Structures

### Basic Physical Data Structures

#### Array

An array is a collection of memory locations, all of which are side by side. Arrays are static, so once established, their size cannot be adjusted. An array can be created in the stack or the heap. An array is chosen when the size of the collection is known.

#### Linked List

A linked list also a collection of memory locations as well, but it is created differently. A linked list uses nodes, and these nodes contain a head and a pointer pointing to the next node. In this way, Linked Lists are dynamic and must always be created in the heap. A linked list is chosen when the size of the collection is unknown.

### Logical Data Structures

There are linear, non-linear, and tabular Logical Data Structures. The linear ones are the Stack and Queues. The non linear ones are the Tree and Graph. The tabular one is the Hash Table. We will delve into these later, but it is important to understand that the Physical Data Structures build these Logical Data Structures.

# Recursion

## Introduction

Given the function `fun`:

```cpp
int fun(int n) {
    if (n > 1) {
        return fun(n-1) * 2;
    } else {
        return n;
    }
}
```

We can see that the function consists of an if-else statement, where if the input is greater than 1, we return the value of the function `fun(n-1)*2`, and if not, we just return n. In this way, we can simplify the function to just be:

```cpp
int fun(int n) {
    if (n > 1) {
        return fun(n-1) * 2;
    }
    return n;
}
```

This is an example of a recursive function. A recursive function consits of two parts, an ascending portion and a descending portion. We ascend by returning values of the function, and descend once we reach our catch value, in this case it is once $n \le 1$. The algorithm returns $2^n$.

## Tail Recursion

Tail recursion is defined as recursion in which the last statement is the recursive call, for example:

```cpp
void fun(n) {
    if (n > 0) {
        // Do stuff Here
        // ...
        fun(n-1);
    }
}
```

So all the processing is done before the recursive call.

## Head Recursion

Head recursion is defined as recursion in which the first statement is the recursive call, for example:

```cpp
void fun(n) {
    if (n > 0) {
        fun(n-1);
        // Do stuff Here
        // ...
    }
}
```

So all the processing is done after the recursive call.

## Linear Recursion vs. Tree Recursion

Linear Recursion is recursion in which there is only one branch of recursion, in other words it maintains a straight line, for example:

```cpp
void fun(n) {
    if (n > 0) {
        // Do stuff here
        // ...
        fun(n-1);
        // Do stuff here
        // ...
    }
}
```

Tree Recursion is recursion in which there is more than one branch of recursion, kind of like a tree, for example:

```cpp
void fun(n) {
    if (n > 0) {
        // Do stuff here
        // ...
        fun(n-1);
        // Do stuff here
        // ...
        fun(n-1);
        // Do stuff here
        // ...
    }
}
```

An example of tree recursion can be found here:

```cpp
#include <stdio.h>

void fun(int n) {
    if (n > 0) {
        printf("%d ", n);
        fun(n-1);
        fun(n-1);    
    }
}
```

This will give the output `3 2 1 1 2 1 1`. This is because we call the function with the input 3, we print 3, and then call `fun(3-1)`, it then prints 2, and then calls `fun(2-1)`, which prints 1, and then calls `fun(2-1)` again, which prints 1. Then we descend, and `fun(3-1)` is called a second time, which repeats the same process over again one last time.

## Indirect Recursion

Indirect recursion is recursion that happens between two or more functions, which makes a sort of circular pattern, for example:

```cpp
void A(int n) {
    if (<-->) {
        // Do stuff here
        // ...
        B(n-1);
    }
}
void B(int n) {
    if (<-->) {
        // Do stuff here
        // ...
        A(n-1);
    }
}
```

## Nested Recursion

Nested Recursion is recursion within recursion, in other words a recursive call within a recursive call, for example:

```cpp
void fun(int n) {
    if (<-->) {
        // Do stuff here
        fun(fun(n-1));
    }
}
```

In this way, we evaulate the parameter of the recursive call first, then whatever that is, place it into that recursive call.

## Examples of Recursion

### Fibonacci Sequence

The Fibonacci Sequence is defined as $F_n = F_{n-1} + F_{n-2}$, where $F_0 = 0$ and $F_1 = 1$. We can use Tree Recursion to write an algorithm to calculate the sum of the sequence:

```cpp
int fib(int n) {
    if (n <= 1) {
        return n;
    }
    return fib(n-1) + fib(n-2);
}
```

### Sum of Natural Numbers

The sum of all natural numbers at point n, is equal to the sum of the natural numbers $(n-1)$, plus $n$. In other words, `sum(n) = sum(n-1)+n`

```cpp
int sum(int n) {
    if (n == 0) {
        return 0;
    }
    else {
        return sum(n - 1) + n;
    }
}
```

# Arrays

As spoken about in the introduction, an array is a collection of memory locations, all of which are side by side. The basic way of declaring an array is as follows:

```cpp
type variable[size];
```

For instance:

```cpp
int A[5];
```

This is an array of integers, with length 5. This is a **static** array, which means that once declared, the size is not changable, and it lives on the stack. A dynamic array is as follows:

```cpp
int main() {
    int size; // Declare variable size as an integer
    std::cin >> size; // Get user input for the size
    int *array = new int[size]; // Declare pointer array as a new array
                                // with length size
    delete [] array;            // Always delete arrays made with new
    array = NULL;               // Delete the location of the pointer
    return 0;
}
```

This is an unsafe way of doing it, but is how you'd do it with `new`, using a smart pointer, you could do this in C++14, which skips all the crazy `new[]` and `delete[]` stuff:

```cpp
auto array = std::make_unique<int[]>(size);
```

A bit semantical, just something that should be kept in mind when actually doing this in practice. You can also declare arrays that are two dimensional, eg.

`int A[3][4];`

This means there are three integer arrays, all four in length.

## A Low Level Look At Arrays

```cpp
#include <iostream>

using namespace std;

int main() {
    int array[2] = {0, 1}; // Declare an Array of Length 2
    int *array_pointer = array; // Declare a ponter

    cout << array << endl; // Prints 0x7ffdc44f1460
    cout << array_pointer << endl; // Prints 0x7ffdc44f1460

    cout << *array_pointer << endl; // Prints 0
    cout << array[0] << endl; // Prints 0

    ++array_pointer; // Incrementing the pointer

    cout << array_pointer << endl; // Prints 0x7ffdc44f1464

    cout << *array_pointer << endl; // Prints 1
    out << array[1] << endl; // Prints 1
}
```

Full output:

```
0x7ffdc44f1460
0x7ffdc44f1460
0
1
0x7ffdc44f1464
1
1
```

The integer type consists of 4 bytes, so when we increment the pointer, we are looking at the memory 4 bytes to the right. 

## Array ADT

The Data of an Array consists of:

1. Array Space
   
   * In C++ this is done with `int A[10];`

2. Size
   
   * In C++ this is done with:
   
   * ```cpp
     int *A;
     A = new int[size];
     ```

3. Length (Number of Elements)
   
   * When we initialize an array, it has length 0. When we add an element, it is length 1, etc.

Operations an array should support:

* `Display()`

* `Append(x)`

* `Insert(index, x)`

* `Delete(index)`

* `Search(x)`

* `Get(index)`

* `Set(index, x)`

* `max()/min()`

* `Reverse()`

* `Shift()`

### Initial Creation

```cpp
#include <iostream>

class Array {
    private:
        int* A; // integer pointer
        int size; // size of the array
        int length; // length of the number of elements in the array

    public:
        // to be done
}

int main() {
    // to be done
}
```

As we can see, we have created the class Array which consists of a pointer, the size of the array, and the length of the number of elements in the array. What we need to create are the following:

* `Create()`

* `Display()`

```cpp
#include <iostream>
using namespace std;

class Array {
    private:
        int* A; // integer pointer
        int size; // size of the array
        int length; // length of the number of elements in the array

    public:
        Array(int size) {
            this->size = size; // Set size as size
            length = 0; // Set length as zero
            A = new int [size]; // Declare int pointer as array 
        }

        void Create(int length) {
            if (this->size < length) {
                cout << "Too large" << endl;
                abort();
            }
            this->length = length // Set length
            cout << "Enter the array elements: " << endl;
            for (int i = 0; i < length; i++) {
                cout << "Array element: " << i << " = " << flush;
                cin >> A[i]; // Set elements
            }
        }

        void Display() {
            for (int i = 0; i < length; i++) {
                cout << A[i] << " ";
            }
        }

        ~Array() {
            delete[] A;
            cout << "Array destroyed" << endl;
        }
};

int main() {
    int size = 10; // Declare size here
    Array arr(size); // Declare Array with a size, size
    int length = 11; // Declare length here
    arr.Create(length); // Create it and give it values
    arr.Display(); // Display
    return 0;
    // Array destroyed
}
```

A note, for `~Array`, that is run whenever the variable goes out scope. In this case, we just delete the pointer.

### `Append` and `Insert`

For `Append(x)`:

```cpp
void Append(int x) {
    if (length < size) {
        A[length++] = x; // Increase length and set
    }
}
```

If we're not at max capacity, we can append.

For `Insert(index, x)`:

```cpp
void Insert(int index, int x) {
    if (index >= 0 && index <= length) {
        for (int i = length; i > index; i--) {
            A[i] = A[i-1];
        }
        A[index]=x;
        length++;
    }
}
```

Here we just loop over everything, and set everything back one point to the right of the index we are trying to insert at.

### `Delete`

```cpp
int Delete(int index) {
    if (index >= 0 && index < length) {
        int x = A[index];
        for (i = index; i < length - 1; i++) {
            A[i] = A[i+1]; // 
        }
        length--;
        return x; // Return deleted element
    }
    return 0;
}
```

This is all pretty self explanatory.

### `LinearSearch` and `BinarySearch`

For `LinearSearch(key)`:

```cpp
class Array {
    private:
        int* A; // integer pointer
        int size; // size of the array
        int length; // length of the number of elements in the array
        void swap(int *x, int *y) {
            int temp;
            temp = *x;
            *x = *y;
            *y = temp;   
        }
    // ...
    int LinearSearch(int key, bool do_swap) {
        for (int i = 0; i < length; i++) {
            if (key == A[i]) { // If we have a match
                if (do_swap == true) { // Do we swap found index with 0?
                    swap(&A[i], &A[0]);
                }
                return i; // Return the index
            }
        }
        return -1; // If we don't find anything
    }
```

The idea behind `do_swap` is that if we are searching for an element, we might search for it again. If we have an unsorted array, it can be adventageous to just swap as we might search for the value again. A linear search has a time complexity of $O(n)$.

For `BinarySearch(key)`:

```cpp
int BinarySearch(int key) {
    int l, mid, h;
    l = 0; // lowest value
    h = length; // highest value
    while (l <= h) {
        mid = (l + h) / 2; // new middle
        if (key == A[mid]) { // if middle is match, return mid
            return mid;
        } else if (key < A[mid]) {  // if our key is below middle value,
            h = mid - 1;            // decrement highest
        } else {
            l = mid + 1;            // if our key is above middle value
        }                           // increment lowest 
    }
    return -1;
}
```

For this to work, the array has to be sorted. A binary search has a time complexity of $O(\log_2 n)$

### `Get`, `Set`, `Max`, and `Min`

For `Get(index)`:

```cpp
int Get(int index) {
    if (index >= 0 && index < length) { // if index exists
        return A[index];
    }
    return -1;
}
```

For `Set(index, x)`

```cpp
void Set(int index, int x) {
    if (index >= 0 && index < length) { // if index exists
        A[index] = x;
    }
}
```

For `Max()`:

```cpp
int Max() {
    int max = A[0];       // largest value
    for (int i = 1; i < length; i++) {
        if (A[i] > max) { // first instance of max
            max = A[i];   // so first of any repeats
        }
    }
    return max;
}
```

For `Min()`:

```cpp
int Min() {
    int min = A[0];       // smallest value
    for (int i = 1; i < length; i++) {
        if (A[i] < min) { // first instance of min
            min = A[i];   // so first of any repeats
        }
    }
    return min;
}
```

### `Reverse`

```cpp
void Reverse() {
    int i, j;
    for (i = 0, j = length - 1; i < j; i++, j--) {
        swap(&A[i], &A[j]);
    }
}
```

This reverses the array, and its time complexity is $O(n)$.

### `isSorted`

```cpp
bool isSorted() {
    for (int i = 0; i < length - 1; i++) {
        if (A[i] > A[i + 1]) {
            return false;
        }
    }
    return true;
}
```

### `Merge`

```cpp
Array Merge(Array& B) {
    Array C(length + B.length);
    int i, j, k = 0;
    while (i < length && j < B.length) {
        if (A[i] < B.Get(j)) {
            C.Set(k++, A[i++]);
        } else {
            C.Set(k++, B.Get(j++));
        }
    }
    for (; i < length; i++) {
        C.Set(k++, A[i]);
    }
    for (; j < B.length; j++) {
        C.Set(k++, B.Get(j));
    }
    return C;
}
```

# Strings

## Introduction

The `char` is a data type that represents a character. It can take number values from -128 to 127, and each number represents an ASCII character. Strings can thus be constructed by "stringing" together characters. For instance:

```cpp
char name[10] = {'J', 'o', 'h', 'n'};
```

When analyzing this declaration, it becomes apparent we have a problem. This is because we are declaring an array with size 10, which means that:

```
[J] [o] [h] [n] [0] [0]     [0]
[0] [1] [2] [3] [4] [5] ... [10]
```

Each of these sections of the array technically could include a character. This means we need a specific character to denote the termination of a string, and this is known as the "Null" character, or `'\0'`. So this:

```cpp
char name[10] = {'J', 'o', 'h', 'n'};
```

is equivalent to this:

```cpp
char name[10] = {'J', 'o', 'h', 'n', '\0'};
```

## Length

To determine the length of a string, we loop over it until we find a `\0`:

```cpp
#include <iostream>
int main() {
    char S[] = "John";
    int i;
    for (i = 0; S[i] != '\0'; i++) {
    }
    std::cout << i << std::endl; // Prints 4
}
```

## Change Case

The ASCII Character code for capital A is 65, and the ASCII Character code for lowercase a is 97. Then, Z and z are 90 and 122, respectively. This means that the absolute value of the difference between the corresponding values of any two characters (A and a for example) is 32. We can use this to our advantage to change the case of a string:

```cpp
#include <iostream>
int main() {
    char S[] = "John";
    for (int i = 0; S[i] != '\0'; i++) {
        if (S[i] >= 'A' && S[i] <= 'Z') {
            S[i] += 32;
        } else if (S[i] >= 'a' && S[i] <= 'z') {
            S[i] -= 32;
        }
    }
    for (int i = 0; i < 5; i++) {
        std::cout << S[i];
    } // Prints jOHN
}
```

## Reversing a String

To reverse a string, we use the following method:

```cpp
#include <iostream>
int main() {
  char S[] = "John!";
  int i, j;
  char t;
  for (j = 0; S[j] != '\0'; j++) {
  }
  j--;
  for (i = 0; i < j; i++, j--) {
    t = S[i];
    S[i] = S[j];
    S[j] = t;
  }
  for (int i = 0; i < 6; i++) {
    std::cout << S[i];
  } // Prints !nhoJ
}
```

## Duplicates in a String

```cpp
#include <iostream>
int main() {
  char S[] = "finding";
  int H[26] = {}; // Set all 26 values to zero
  for (int i = 0; S[i] != '\0'; i++) {
    H[S[i] - 97] += 1;
  }
  for (int i = 0; i < 26; i++) {
    if (H[i] >= 1) {
      std::cout << (char)(i + 97) << " " << H[i] << std::endl;
    }
  }
}
```

# Matrices

## Diagonal Matrix

A Diagonal Matrix is like the following:

```
    1 2 3 4 ...
1 | a 0 0 0
2 | 0 b 0 0
3 | 0 0 c 0
4 | 0 0 0 d
...
```

Which can be defined as $M[i, j] = 0 \text{ if } i \ne j$

This matrix will be the framework for later types of matrixs:

```cpp
#include <iostream>
class Matrix {
    private:
        int *A;
        int n;

    public:
        Matrix() {
            n = 2;
            A = new int [2];
        }

        Matrix(int n) {
            this->n = n;
            A = new int [n];
        }

        void Set(int i, int j, int x) {
            if (i == j) {
                A[i - 1] = x;
            }
        }

        int Get(int i, int j) {
            if (i == j) {
                return A[i - 1];
            }
            return 0;
        }

        void Display() {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (i == j) {
                        std::cout << A[i] << " ";
                    } else {
                        std::cout << "0 ";
                    }
                }
                std::cout << std::endl;
            }
        }

        ~Matrix() {
            delete [] A;
        }
};

int main() {
    int size = 5;
    Matrix diagonal(size);

    for(int i = 1; i <= size; i++) {
        for(int j = 1; j <= size; j++) {
            diagonal.Set(i,j,i);
        }
    }

    diagonal.Display();
}
```

Returns:

```
1 0 0 0 0
0 2 0 0 0
0 0 3 0 0
0 0 0 4 0
0 0 0 0 5
```

## Lower Triangle Matrix

A Lower Triangle Matrix is like the following:

```
    1 2 3 4 ...
1 | a 0 0 0
2 | b c 0 0
3 | d e f 0
4 | g h i j
...
```

Which can be defined as:
$M[i, j] = 0 \text{ if } i < j$

$M[i, j] \ne 0 \text{ if } i \ge j$

When observing the space this matrix takes up, we can observe that each n row adds n amount of space, eg. 1 + 2 + 3, etc. etc. This means the number of non zero elements are give in $\frac{n(n+1)}{2}$, and the number of zero elements is given by $\frac{n(n-1)}{2}$.

Though this is the case, there are two methods to represent this as an array, the first is row major mapping:

```
A | 0 1 2 3 4 5 6 7 8 9 
    a b c d e f g h i j
```

This corresponds to the rows in the first diagram. So 0 is the first row, 1 and 2 is the second, 3-5 the third, and 6-9 the fourth.

The second method is column major mapping:

```
    1 2 3 4 ...
1 | a 0 0 0
2 | b e 0 0
3 | c f h 0
4 | d g i j
...
```

So looking at our array now, 0-4 represents the first column, 5-6 represents the second column, 7 and 8 the third, and 9 the fourth. 

Here is an implementation of Row Major mapping:

```cpp
#include <iostream>
class Triangle {
    private:
        int *A;
        int n;

    public:
        Triangle() {
            n = 2;
            A = new int [3];
        }

        Triangle(int n) {
            this->n = n;
            A = new int [n * (n + 1) / 2];
        }

        void Set(int i, int j, int x) {
            if (i >= j) {
                A[i * (i - 1) / 2 + j - 1] = x;
            }
        }

        int Get(int i, int j) {
            if (i >= j) {
                return A[i * (i - 1) / 2 + j - 1];
            }
            return 0;
        }

        void Display() {
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= n; j++) {
                    if (i >= j) {
                        std::cout << A[i * (i - 1) / 2 + j - 1] << " ";
                    } else {
                        std::cout << "0 ";
                    }
                }
                std::cout << std::endl;
            }
        }

        ~Triangle() {
            delete [] A;
        }
};

int main() {
    int size = 5;
    Triangle triangle(size);

    for(int i = 1; i <= size; i++) {
        for(int j = 1; j <= size; j++) {
            triangle.Set(i,j,i);
        }
    }

    triangle.Display();
}
```

Returns:

```
1 0 0 0 0 
2 2 0 0 0 
3 3 3 0 0 
4 4 4 4 0 
5 5 5 5 5
```

## Upper Triangle Matrix

An Upper Triangle Matrix is represented as:

```
    1 2 3 4 ...
1 | a b c d
2 | 0 e f g
3 | 0 0 h i
4 | 0 0 0 j
...
```

Which can be defined as:
$M[i, j] = 0 \text{ if } i > j$

$M[i, j] \ne 0 \text{ if } i \le j$

When observing the space this matrix takes up, we can observe that each n row adds n amount of space, eg. 1 + 2 + 3, etc. etc. This means the number of non zero elements are give in $\frac{n(n+1)}{2}$, and the number of zero elements is given by $\frac{n(n-1)}{2}$.

Like the Lower Triangle Matrix, there also exists a Column-Major Mapping, but we won't get into that as the concept is basically the same. The implementation of this matrix is the same as the last, just adjust lines 19, 25, and 24 from `i >= j` to `i <= j`.

## Symmetric Matrix

A Symmetric Matrix is represented as:

```
    1 2 3 4 ...
1 | a a a a
2 | a b b b
3 | a b c c
4 | a b c d
...
```

Which can be defined as:

$M[i,j] = M[j, i]$

This looks intimidating, but we already implemented this already, as if we notice, we can draw a diagonal line down the center, and anything to the right or to the bottom is already covered by the corresponding. Eg. we can represent this as either a Lower Triangle or an Upper Triangle, and just mirror it.

### Tridiagonal Matrix

A Tridiagonal Matrix is represented as:

```
    1 2 3 4 5 ...
1 | a b 0 0 0
2 | c d e 0 0
3 | 0 f g h 0
4 | 0 0 i j k
5 | 0 0 0 l m
...
```

Which can be defined as:

$M[i, j] \ne 0 \text{ if } |i - j| \le 1$

Here is an implementation:

```cpp
#include <iostream>
#include <cmath>

class Triangle {
    private:
        int *A;
        int n;

    public:
        Triangle() {
            n = 2;
            A = new int [6];
        }

        Triangle(int n) {
            this->n = n;
            A = new int [3 * n];
        }

        void Set(int i, int j, int x) {
            if (abs(i - j) <= 1) {
                A[3 * i + abs(i - j)] = x;
            }
        }

        int Get(int i, int j) {
            if (abs(i - j) <= 1) {
                return A[3 * i + abs(i - j)];
            }
            return 0;
        }

        void Display() {
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= n; j++) {
                    if (abs(i - j) <= 1) {
                        std::cout << A[3 * i + abs(i - j)] << " ";
                    } else {
                        std::cout << "0 ";
                    }
                }
                std::cout << std::endl;
            }
        }

        ~Triangle() {
            delete [] A;
        }
};

int main() {
    int size = 9;
    Triangle diagonal(size);
    for(int i = 1; i <= size; i++) {
        for(int j = 1; j <= size; j++) {
            diagonal.Set(i,j,i);
        }
    }

    diagonal.Display();
}
```

Result:

```
1 1 0 0 0 0 0 0 0 
2 2 2 0 0 0 0 0 0 
0 3 3 3 0 0 0 0 0 
0 0 4 4 4 0 0 0 0 
0 0 0 5 5 5 0 0 0 
0 0 0 0 6 6 6 0 0 
0 0 0 0 0 7 7 7 0 
0 0 0 0 0 0 8 8 8 
0 0 0 0 0 0 0 9 9
```

The formula for space is technically $3n -2$, but the space is basically ignorable so I just set it 3n.

## Sparse Matrix

A sparse matrix is a matrix where non-zero elements can be anywhere in the matrix, such as:

```
    1 2 3 4 5 ...
1 | a 0 0 0 0
2 | 0 0 b 0 c
3 | d 0 e 0 0
4 | 0 f 0 0 0
5 | 0 0 0 g 0
...
```

As we can see, the elements are dispersed about the matrix, with no pattern. As a result, we have to store our elements using coordinates, namely their i and j coordinates. As a result, we can define the class `Element` to facilitate this:

```cpp
class Element {
    public:
        int i;
        int j;
        int x;
};
```

Next, we need the actual Matrix, so we will use the class `Sparse`:

```cpp
class Sparse {
    private:
        int m; // Dimension
        int n; // Dimension
        int num; // Number of non-zero elements
        Element *ele; // Array of the elements.
    public:
        Sparse(int m, int n, int num) {
            this->m = m;
            this->n = n;
            this->num = num;
            ele = new Element[this->num];    
        }

        ~Sparse() {
            delete[] ele;
        }
}
```

Next, we need a way to set and get the matrix, for this we are going to use the `istream` and `ostream` operators.

```cpp
friend std::istream & operator >> (std::istream &is, Sparse &s) {
    std::cout << "Enter non-zero elements ";
    for(int i = 0; i < s.num; i++) {
        std::cin >> s.ele[i].i >> s.ele[i].j >> s.ele[i].x; // Loop over
    }                                      // number of elements, assign
    std::cout << std::endl;
    return is;
}

friend std::ostream & operator << (std::ostream &os, Sparse &s) {
    int k = 0; // Current element
    for (int i = 0; i < s.m; i++) { // Go over the m coordinate
        for (int j = 0; j < s.n; j++) { // Go over the n coordinate
            if (s.ele[k].i == i && s.ele[k].j == j) {
                std::cout << s.ele[k++].x << " "; // increment k
            }
            else {
                std::cout << "0 ";
            }
        }
        std::cout << std::endl;
    }
    return os;
}
```

Last but not least, lets add a method to allow addition of two sparse matrices. 

```cpp
Sparse operator+(Sparse &s) {
    if (m != s.m || n!=s.n) { // if the two arrays
        return Sparse(0, 0, 0); // dimensions do not match
    }
    Sparse *sum = new Sparse(m, n, num + s.num);

    int i, j, k;
    i = j = k = 0;
    while(i < num && j<s.num) {
        if (ele[i].i < s.ele[j].i) {
            sum->ele[k++] = ele[i++];
        } else if (ele[i].j > s.ele[j].j) {
            sum->ele[k++] = s.ele[j++];
        } else {
            sum->ele[k] = ele[i];
            sum->ele[k++].x = ele[i++].x + s.ele[j++].x;
        }
    }
    for(; i < num; i++) {
        sum->ele[k++] = ele[i];
    }
    for(; j < s.num; j++) {
        sum->ele[k++] = s.ele[j];
    }
    sum->num = k;
    return *sum;
}
```

Putting it all together:

```cpp
#include <iostream>
using namespace std;

class Element {
    public:
        int i;
        int j;
        int x;
};

class Sparse {
    private:
        int m; // Dimension
        int n; // Dimension
        int num; // Number of non-zero elements
        Element *ele; // Array of the elements.
    public:
        Sparse(int m, int n, int num) {
            this->m = m;
            this->n = n;
            this->num = num;
            ele = new Element[this->num];    
        }

        friend istream & operator >> (istream &is, Sparse &s) {
            cout << "Enter non-zero elements ";
            for(int i = 0; i < s.num; i++) {
                cin >> s.ele[i].i >> s.ele[i].j >> s.ele[i].x;
            }
            cout << endl;
            return is;
        }

        friend ostream & operator << (ostream &os, Sparse &s) {
            int k = 0; // Current element
            for (int i = 0; i < s.m; i++) { // Go over m coordinate
                for (int j = 0; j < s.n; j++) { // Go over n coordinate
                    if (s.ele[k].i == i && s.ele[k].j == j) {
                        cout << s.ele[k++].x << " "; // increment k
                    }
                    else {
                        cout << "0 ";
                    }
                }
                cout << endl;
            }
            return os;
        }

        Sparse operator+(Sparse &s) {
            if (m != s.m || n!=s.n) { // if the two arrays
                return Sparse(0, 0, 0); // dimensions do not match
            }
            Sparse *sum = new Sparse(m, n, num + s.num);

            int i, j, k;
            i = j = k = 0;
            while(i < num && j<s.num) {
                if (ele[i].i < s.ele[j].i) {
                    sum->ele[k++] = ele[i++];
                } else if (ele[i].j > s.ele[j].j) {
                    sum->ele[k++] = s.ele[j++];
                } else {
                    sum->ele[k] = ele[i];
                    sum->ele[k++].x = ele[i++].x + s.ele[j++].x;
                }
            }
            for(; i < num; i++) {
                sum->ele[k++] = ele[i];
            }
            for(; j < s.num; j++) {
                sum->ele[k++] = s.ele[j];
            }
            sum->num = k;
            return *sum;
        }

        ~Sparse() {
            delete[] ele;
        }
};

int main() {
    Sparse s1(5,5,5);
    Sparse s2(5, 5, 5);
    cin >> s1;
    cin >> s2;

    Sparse sum = s1 + s2;

    cout << "S1" << endl << s1;
    cout << "S2" << endl << s2;
    cout << "Sum" << endl << sum;
    return 0;
}
```

# Linked List

### Introduction

An array works off the principle of a bench. A benches seats are right next to each other, and they are of a fixed size. I can't call chairs that are 10 feet apart a bench, and I can't go up to a bench and extend or shrink it. Similarly, an array is defined as pieces of memory that are next to each other, and they are fixed in size. Linked List are a different way of creating collections of data. An array is formed like the following:

```cpp
// For the array:
char foo [5] = {'A', 'B', 'C', 'D', 'E'};

// It can be seen as consisting of three parts:
Index   |   0   1   2   3   4
Element |   A   B   C   D   E
Address |  200 204 208 212 214
```

Each index has a corresponding element, and each element corresponds to an address. A linked list is constructed like this:

```
[Element][Pointer] -> [Element 2][Pointer] -> ... -> [Element n][/0]
```

A linked list is constructed as a series of nodes, consisting of an element, and a pointer, pointing to the next node. This creates a list of links, until we reach the end node, which a NULL pointer.

### Writing

A Linked List can be represented as:

```cpp
class Node {
  public:
    int data; // The Node data
    Node* next; // Points to the next Node
};
```

The Node class contains the data and a pointer to another Node. We can work with the Linked List a little bit with just this:

```cpp
int main() {
    // Create an Array to transfer
    int A[] = {1, 2, 3, 4, 5};

    // Create the first Node
    Node* head = new Node; 

    // Initialize a temporary and last Node 
    Node* temp;
    Node* last;

    // Set the first Node
    head->data = A[0];
    head->next = nullptr;

    // Set the current last node to head
    last = head;

    // Create the Linked List
    for(int i = 1; i < sizeof(A)/sizeof(A[0]); i++) {
        // Create the temporary Node
        temp = new Node;

        // Populate temporary Node
        temp->data = A[i];
        temp->next = nullptr;

        // Set the current last's next pointer to temp,
        // then set last as temp.
        last->next = temp;
        last = temp;
    }

    // Display
    // Create a pointer to head
    Node* p = head;

    while(p != nullptr) { // Stop whenever we hit null ptr
        std::cout << p->data << " -> " << std::flush; // print current p
        p = p->next; // Move p forward
    }

    return 0;
}
```

This outputs:

```
1 -> 2 -> 3 -> 4 -> 5 -> 
```

Another way to display a linked list is with a recursive function:

```cpp
void RDisplay(Node* p) {
    if (p != nullptr) {
        std::cout << p->data << " ";
        RDisplay(p->next);
    }
}
```

These notes don't use a Class implementation of Linked List, instead passing the linked list into each one. This was helpful when I was learning how Linked Lists work, but ideally, for C++ use a class instead.

### Counting Nodes

Counting Nodes is pretty similar to Display, we just loop and count until we reach the end:

```cpp
int Count(Node* head) {
    Node* p = head;
    int num = 0;
    while (p != nullptr) {
        num++;
        p = p->next;
    }
    return num;
}
```

As you can see, we just loop over it until we reach the null pointer, with each iteration we are just increasing the `num` integer.

#### Recursive Implementation of `Count`

We can also count Nodes recursively:

```cpp
int RCount(Node* p) {
    if (p == nullptr) {
        return 0;
    }
    return RCount(p->next) + 1;
}
```

### Sum of all Elements

Just like counting, sum is pretty similar, just we have to access the data as well:

```cpp
int Sum(Node* head) {
    Node* p = head;
    int sum = 0;
    while (p != nullptr) {
        sum += p->data;
        p = p->next;
    }
    return sum;
}
```

#### Recursive Implementation of `Sum`

We can also sum the Nodes recursively:

```cpp
int RSum(Node* p) {
    if (p == nullptr) {
        return 0;
    }
    return RSum(p->next) + p->data;
}
```

### Max of Elements

Just like counting, max is pretty similar:

```cpp
int Max(Node* head) {
    Node* p = head;
    int max = 0;
    while (p != nullptr) {
        if (p->data > max) {
            max = p->data;
        }
    }
    return max;
}
```

### Searching

A linked list is a linear search only:

```cpp
Node* Search(Node* p, int key) {
    while(p != nullptr) {
        if (key == p->data) {
            return p;
        }
        p = p->next;
    }
    return NULL;
}
```

### Inserting

An insert for a linked list is pretty simple:

```cpp
Node* Insert(Node* head, int index, int x) {
    if(index <0 || index > Count(head)) {
        return NULL;
    }
    Node *p=head;
    Node *t;
    t = new Node;
    t->data = x;
    t->next = NULL;

    if (index == 0) {
        t->next = head;
        head = t;
    } else {
        for(int i=0;i<index-1;i++) {
            p = p->next;
        }
        t->next = p->next;
        p->next = t;
    }
    return head;
}
```

If we are out of bounds, we return null. We define two new node objects, one which is equal to the head node, and another which is a fresh node. In the case that we are inserting at the 0th index, we just set the `t->next` value to head, and then set head equal to `t`. If not, we loop over `p`, incrementing everything right ward `index - 1` number of times. Afterwards, we set `t->next` equal to `p->next`, and then set `p->next` to equal `t`. This places `t` in between, right where we want it to be.

### Check If Linked List Loops

So a linked list consists of Nodes as we have seen, but what if a pointer from a node points to another node within itself, in other words it forms a looping linear linked list:

```
                       V---------------------------------------------
[Element][Pointer] -> [Element 2][Pointer] -> [Element n][Pointer] -^
```

In this way, it loops back around. Well, we can detect this using two pointers that increment over the list. One increments by one step, and the other by two. If they meet again, then the linked list must loop:

```cpp
bool isLoop(Node* head) {
    Node* p;
    Node* q;
    p = head;
    q = head;

    do {
        p = p->next;
        q = q->next;
        q = q ? q->next:q;
    } while (p && q && p != q);

    if (p == q) {
        return true;
    }
    return false;
}
```

## Doubly Linked List

A Linked List has one pointer, pointing to the next node. A Doubly Linked List is a Linked List with two pointers, one pointing to the next node and the second pointing to the node before it. To begin, lets modify our `Node` object:

```cpp
class Node {
    public:
        Node* prev;
        int data;
        Node* next;
};
```

As we can see, we added a new variable called `prev`, which as you can guess, points to the previous element. Unlike our Linked List, we are also going to code a class for this to make things easier to develop, now that we have an understanding of the Linked List:

```cpp
class DoublyLinkedList {
    private:
        Node* head; // Our head node
    public:
        DoublyLinkedList() {
            head = new Node;
            head->prev = nullptr;
            head->data = 0;
            head->next = nullptr;
        }

        DoublyLinkedList(int *A, int n) {
            head = new Node;
            head->prev = nullptr;
            head->data = A[0];
            head->next = nullptr;
            Node* tail = head;

            for(int i = 1; i < n; i++) {
                Node* t = new Node;
                t->prev = tail;
                t->data = A[i];
                t->next = tail->next;
                tail->next = t;
                tail = t;
            }
        }

        ~DoublyLinkedList() {
            Node* p = head;
            while (head) {
                head = head->next;
                delete p;
                p = head;
            }
        }
};
```

Next we can code our main function:

```cpp
int main() {
    int A[] = {1, 2, 3, 4, 5};
    DoublyLinkedList dll(A, 5);
    return 0;
}
```

We need to add a display function, and we will basically recycle our old code from the Single Linked List:

```cpp
using namespace std;
#include <iostream>
// ...
friend ostream & operator << (ostream &os, DoublyLinkedList &dll) {
    Node* p = dll.head;
    while(p != nullptr) { 
        cout << p->data << " -> " << flush;
        p = p->next;
    }
    cout << endl;
    return os;
}
```

### Inserting

The insert for a doubly linked list is very similar to the normal linked list, just we also have to point to the previous element.

```cpp
int Length() {
    int length = 0;
    Node* p = head;
    while (p != nullptr) {
        length++;
        p = p->next;
    }
    return length;
}

void Insert(int index, int value) {
    if (index < 0 || index > Length()) {
        return;
    }

    Node* t = new Node;
    t->data = value;

    if (index == 0) {
        t->prev = nullptr;
        t->next = head;
        head->prev = t;
        head = t;
    } else {
        Node* p = head;
        for (int i = 0; i < index - 1; i ++) {
            p = p->next;
        }

        t->prev = p;
        t->next = p->next;
        if (p->next) {
            p->next->prev = t;
        }
        p->next = t;
    }
}
```

### Deleting

Much like a normal linked list, the same principle applies, but we have to account for two pointers now:

```cpp
int Delete(int index) {
    int x = -1;
    Node* p = head;

    if (index < 0 || index > Length()) {
        return x;
    }

    if (index == 1) {
        head = head->next;
        if (head) {
            head->prev = nullptr;
        }
        x = p->data;
        delete p;
    } else {
        for (int i=0; i<index-1; i++) {
            p = p->next;
        }
        p->prev->next = p->next;
        if (p->next) {
            p->next->prev = p->prev;
        }
        x = p->data;
        delete p;
    }
    return x;
}
```

# Stack

The stack is a way of representing Data, and it operates on the LIFO principle. The last in is the first to be pulled out. A recursion uses a stack, but this is handled by a compiler. It is known that every recursion can be converted to an interative algorithm and vise-versa, but some recursive algorithm once conerted to an iterative proccess need a programmer designed stack. A stack consists of two parts of data:

1. Space for storing elements

2. Top pointer

And the following operations:

1. `push(x)`

2. `pop()`

3. `peak(index)`

4. `stackTop()`

5. `isEmpty()`

6. `isFull()`

Let's look at some implementations of the stack.

## Implementation with Array

For this implementation, we have 3 pieces of data, the actual array, a pointer for the top most element, and the size of the array.

```cpp
class Stack {
    private:
        int size;
        int top;
        int* S;
    public:
        Stack(int size) {
            this->size = size;
            top = -1;
            S = new int[size];
        }

        ~Stack() {
            delete[] S;
        }
};
```

The question arrises, though, when we push a value to the stack, do we push from the left or the right. Well, if we pushed from the left, eg. push to 0, and then the old 0 becomes 1, and then the old 1 becomes 2, etc. etc., our time complexity becomes $O(n)$, but if we know the top most value, so if push from the right, our time complexity is $O(1)$.

### `isFull` and `isEmpty`

```cpp
bool isFull() {
    return (top == size - 1);
}

bool isEmpty() {
    return (top == -1);
}
```

The operations are all $O(1)$, and this is because of our `top` and `size` variables.

### `peak`

```cpp
int peak(int index) {
    int x = -1;
    if (top - index + 1 < 0 || top - index + 1 == size) {
        cout << "Invalid Position!" << endl;
    } else {
        x = S[top - index + 1];
    }
    return x;
}
```

### `push` and `pop`

```cpp
void push(int x) {
    if (isFull()) {
        cout << "Stack Overflow!" << endl;
    } else {
        top++;
        S[top] = x;
    }
}
```

```cpp
int pop() {
    int x = 1;
    if (isEmpty()) {
        cout << "Stack Underflow!" << endl;
    } else {
        x = S[top];
        top--;
    }

}
```

### Display the Stack

```cpp
friend ostream & operator << (ostream &os, Stack &s) {
    for (int i = s.top; i >= 0; i--) {
        cout << s.S[i] << " | " << flush;
    }
    cout << endl;
    return os;
}
```

## `stackTop`

```cpp
int stackTop() {
    if (isEmpty()) {
        return -1;
    }
    return S[top];
}
```

## Implementation with Linked List

The advantage of a linked list over an array is that the stack isn't a fixed size on creation, and instead we can dynamically increase or decrease it with the linked list. Due to the nature of linked lists, this implementation requires less Class variables:

```cpp
class Node {
    public:
        int data;
        Node* next;
};


class Stack {
    private:
        Node* top;
    public:
        Stack() {
            top = nullptr;
        }

        ~Stack() {
            Node* p = top;
            while (top) {
                top = top->next;
                delete p;
                p = top;
            }
        }
};
```

### `isFull` and `isEmpty`

```cpp
int isFull() {
    Node* t = new Node;
    int r = t ? 1 : 0;
    delete t;
    return r;
}

int isEmpty() {
    return top ? 0 : 1;
}
```

### `stackTop`

```cpp
int Stack::stackTop() {
    if (top) {
        return top->data;
    }
    return -1;
}
```

### `peek`

```cpp
int peek(int index) {
    if (isEmpty()) {
        return -1;
    } else {
        Node* p = top;

        for (int i = 0; p != nullptr && i < index - 1; i++) {
            p = p->next;
        }

        if (p != nullptr) {
            return p->data;
        } else {
            return -1;
        }
    }
} 
```

### `push` and `pop`

```cpp
void push(int x) {
    Node* t = new Node;
    if (t == nullptr) {
        cout << "Stack Overflow!" << endl;
    } else {
        t->data = x;
        t->next = top;
        top = t;
    }
}

int pop() {
    Node* p;
    int x = -1;
    if (top == nullptr) {
        cout << "Stack Underflow!" << endl;
    } else {
        p = top;
        x = p->data;
        top = top->next;
        delete p;
    }
    return x;
}
```

## Applications of Stack

### Parenthesis Matching

Imagine we have the expression $(a(a+b) \times (c-d+e))$, how we can determine if the expression has all matching parenthesis, or in other words, if the parenthesis are closed. To do this, lets build off of our Array implementation of the stack:

```cpp
bool isClosed(char* expression) {
    // We didn't implement a Stack class for the array
    // But just assume that it operates like the Linked List one
    Stack stack((int)strlen(exp));

    for (int i = 0; i < strlen(exp); i++) {
        // We push every '(' to the stack
        if (exp[i] == '(') {
            stack.push(exp[i]);
        // We pop everytime there is a '(' in the array
        } else if (exp[i] == ')') {
            // ) + Stack is empty is already a no go
            if (stack.isEmpty()) {
                return false;
            } else {
                stack.pop();
            }
        }

    }
}
```

# Queues

The stack works off of the LIFO principle, a queue works off of the FIFO principle. As a result, everything that is going into the data strucutre enters from one end and then exits from the other. This is incontrast to the stack, where everything enters and exists from the same end. A queue consists of the following parts of data:

1. Space for storing elements

2. Front for deletion

And consists of the following methods:

1. `enqueue(x)`

2. `dequeue()`

3. `isEmpty()`

4. `isFull()`

5. `first()`

6. `last()`

## Queue using Single Pointer

Imagine a queue with an array such as:

```
Q [0][1][2][3][4][5]
Rear = -1
```

Where rear points to the newest element. So:

```
Q [A][B][C][D][4][5]
Rear = 3
```

In this case, our rear most element is D, so Rear is set to 3. The issue is when we want to dequeue, or take out the newest element. Our newest element is A, so when we pull out A, B has to take A's spot, and C has to take B's spot, etc. etc. This means that every time we dequeue, the time complexity is $O(n)$. This is not very good, and can be improved by using two pointers.

## Queue Using Two Pointers

Imagine we have the same queue as earlier but this time with an additional pointer:

```
Q [0][1][2][3][4][5]
Front = Rear = -1
```

Now, lets look at the same example:

```
Q [A][B][C][D][4][5]
Front = -1
Rear = 3
```

Insert is still $O(1)$, but what about dequeuing? Well lets say we want to take out A. Once we take out A, we just increment the Front pointer. This shows us where the front is, and as a result we don't have to move everything over. This makes the dequeue process also $O(1)$! 

So, when looking at this structure, the queue is empty when the front and the rear are equal to each other, and it is full when the rear is equal to size - 1.

## Implementing with Array

Creating the class:

```cpp
#include <iostream>
class Queue {
    private:
        int size;
        int front;
        int rear;
        int* Q;
    public:
        Queue(int size) {
            this->size = size;
            front = -1;
            rear = -1;
            Q = new int [size];
        }

        ~Queue() {
            delete [] Q;
        }
}
```

Display:

```cpp
friend std::ostream & operator << (std::ostream &os, Queue &q) {
    for (int i = q->front + 1; i <= q->rear; i++) {
        std::cout << q->Q[i] << std::flush;
        if (i < q->rear) {
            std::cout << " <- " << std::flush;
        }
    }
    return os;
}
```

### `isEmpty` and `isFull`

```cpp
bool isEmpty() {
    if (front == rear) {
        return true;
    }
    return false;
}

bool isFull() {
    if (rear == size - 1) {
        return true;
    }
    return false;
}
```

### `enqueue` and `dequeue`

```cpp
void enqueue(int x) {
    if (isFull()) {
        std::cout << "Queue Overflow" << std::endl;
    } else {
        rear++;
        Q[rear] = x;
    }
}

int dequeue() {
    int x = -1;
    if (isEmpty()) {
        std::cout << "Queue Underflow" << std::endl;
    } else {
        front++;
        x = Q[front];
    }
    return x;
}
```

### Problems with Array Queue

This current implementation is cool and all, but it~~~~ sucks. Very bad. This is because over time, the queue just outright fails. If you notice, the front and rear pointer just keep moving further and further to the right. This results in the queue over time failing. So we want to be able to use all of the space in the array effectively, and not let the queue die. We have two ways of approaching this:

1. Resetting Pointers

2. Circular Queue

The Circular Queue is the best way of approaching the issue, so we will look at that.

### Circular Queue with Array

The Circular Queue works of the same principle as the two pointer array queue, but it is really a more intelligent implementation. Our new implementation will initially look like this:

```cpp
Q [0][1][2][3][4][5]
Front = Rear = 0
```

Now, the Front and the Rear equal 0. When we start to populate, the array looks like this:

```cpp
Q [0][A][B][C][D][E]
Front = 0
Rear = 5
```

Now, we can see that the Front pointer is at 0, and the Rear pointer is at 5, which is E. Now, when we dequeue, we increment front by 1 and then return Q[front], so it'd return A. In the old implementation, if we wanted to queue an element, it'd say the queue is full, now what we do? Well we just include an element at 0 and set rear to 0! We can't have rear and front on the same point though, because that'd mean the queue is empty, so with this system, the queue can store size - 1 elements. Let's take a look at the implementation.

As before, the initial class looks identical:

```cpp
#include <iostream>
class CircularQueue {
    private:
        int size;
        int front;
        int rear;
        int* Q;
    public:
        CircularQueue(int size) {
            this->size = size;
            front = -1;
            rear = -1;
            Q = new int [size];
        }

        ~CircularQueue() {
            delete [] Q;
        }
};
```

```cpp
friend std::ostream & operator << (std::ostream &os, CircularQueue &q) {
    int i = q.front + 1;
    do {
        std::cout << q.Q[i] << std::flush;
        if (i < q.rear) {
            std::cout << " <- " << std::flush;
        }
        i = (i + 1) % q.size;
    } while (i != (q->rear + 1) % q->size);
    return os;
}
```

#### `isEmpty` and `isFull`

```cpp
bool isEmpty() {
    if (front == rear) {
        return true;
    }
    return false;
}

bool isFull() {
    if ((rear + 1) % size == front) {
        return true;
    }
    return false;
}
```

### `enqueue` and `dequeue`

```cpp
void enqueue(int x) {
    if (isFull()) {
        std::cout << "Queue Overflow" << std::endl;
    } else {
        rear = (rear + 1) % size;
        Q[rear] = x;
    }
}

int dequeue() {
    int x = -1;
    if (isEmpty()) {
        std::cout << "Queue Underflow" << std::endl;
    } else {
        front = (front + 1) % size;
        x = Q[front];
    }
    return x;
}
```

## Implementing with Linked List

A queue can be implemented fairly easily with a Linked List. Given a linked list like the following:

```
[1]->[2]->[3]->[4]->
```

We can use a pointer on 1 to be the front, and a pointer on 4 to be the rear. Usually with a linked list, we only have one pointer that stores the first value in the list, but with a second pointer we can add to the linked list easier in constant time.

Creating the class:

```cpp
#include <iostream>

class Node{
    public:
        int data;
        Node* next;
    };

class Queue{
    private:
        Node* front;
        Node* rear;
    public:
        Queue() {
            front = nullptr;
            rear = nullptr;
        }

        ~Queue() {
            Node* p = front;

            while (front) {
                front = front->next;
                delete p;
                p = front;
            }
        }
```

Display:

```cpp
friend std::ostream & operator << (std::ostream &os, Queue &q) {
    Node* p = q->front;
    while (p) {
        std::cout << p->data << std::flush;
        p = p->next;
        if (p != nullptr) {
            std::cout << " <- " << std::flush;
        }
    }
    std::cout << std::endl;
    return os;
}
```

### `isEmpty`

```cpp
bool isEmpty() {
    if (front == nullptr) {
        return true;
    }
    return false;
}
```

### `enqueue` and `dequeue`

```cpp
void enqueue(int x) {
    Node* t = new Node;
    if (t == nullptr) {
        std::cout << "Queue Overflow" << std::endl;
    } else {
        t->data = x;
        t->next = nullptr;
        if (front == nullptr) {
            front = t;
            rear = t;
        } else {
            rear->next = t;
            rear = t;
        }
    }
}

int dequeue() {
    int x = -1;
    Node* p;
    if (isEmpty()) {
        std::cout << "Queue Underflow" << std::endl;
    } else {
        p = front;
        front = front->next;
        x = p->data;
        delete p;
    }
    return x;
}
```

# Trees

Let's go over some tree terminology

```
                          [A]
         [B]                            [C]
[D]                [E]          [F]              [G]
[H]            [I]    [J]    [K]   [L]           [M]
```

This is a tree, what we call the **root** is A. The root note is made of disjoined subsets, for instance the B subset and the C subset, and then within the B subset, there is the D subset and the E subset. B is a **parent** of D and E, and D and E are a **parent** of B. D and E are **siblings**, B and C are siblings. **Descendents** are a set of nodes such that they can be reached by another Node. D, E, H, I, and J are all descendents of B. Inversely, an **ancestor** is the line of nodes reaching back the root, for instance the ancestors of I are E, B, and A. It is the direct line of ancestory. The **degree** of a node is the number of children it has, the degree of A is 2, the degree of B is 2, the degree of D is 1, and the degree of H is 0. **Leaf Nodes** are nodes where the degree is 0, such as H, I, J, K, etc. **Internal Nodes** are nodes where the degree is greater than 0, such as B, C, D, E, F, and G. The **depth** of a node is the number of edges from the node to the tree's root node. A root node will have a depth of 0. So A's depth is 0, B's depth is 1, E's depth is 2, and J's depth is 3. The **height** of a tree would be the height of its root node, which is equal to the depth of the deepest node. So the height of A is equal to 3. Height doesn't perfectly decrease though, for instance if we introduced another node to A named "Y" with a child node of "Z," A's height would still equal 3, but Y's height would be 1. Something to keep in mind. The **level** of a node is where it is relative to the others, so A is at level 1, B at level 2, D at level 3, etc. etc. 

## Binary Tree

A binary tree must have a degree of 2, eg. every node can have, at maximum, 2 children. This allows us to do things like:

```
              [A]
     [B]               [C]
[D]       [E]     [F]       [G]
```

Because of this two node setup, we can easily refer to each node as either the **left child** and the **right child**. A binary tree is **full** when the height of the tree would increase if we were to add an extra node. The tree above is full, the height is 2, and adding any extra nodes would result in an height increasing by one. 

### Catalan Number

The different combinations of binary trees that can be generated with a set of unlabeled nodes is called the **Catalan number**, where $n$ is our node:

$\displaystyle C_n = \frac{1}{n+1}(\begin{smallmatrix}2n \\ n\end{smallmatrix}) = \frac{(2n)!}{(n+1)!n!}= \prod_{k=2}^n \frac{n+k}{k}$

So, when the $n$ nodes is equal to 1, the Catalan number is 1, when it is 2, the Catalan number is 2, when it is 3, the Catalan number is 5, etc. etc. The number of trees generated with max height is equal to $2^{n-1}$. What about with labeled nodes? Well we just build off of our formula, where the number of individual combinations with labeled nodes is $C_n \times n!$

### Height vs. Nodes

When given a height for a binary tree, what is the minimum and maximum number of nodes there can be? The minimum number of nodes is quite easy to find, for height $h$, minimum nodes is $n=h+1$. Maximum number of nodes is $n=2^{h+1}-1$. The minimum height is solving for h in the maximum number of nodes formula, so for the number of nodes $n$, the minimum height is $h=\log_2(n+1)-1$, and the maximum height is solving for h in the minimum number of nodes formula, so for the number of nodes $n$, the maximum height is $h=n-1$.

### Determining no. Leaf Nodes

The number of leaf nodes/external nodes is $\text{deg}(0)=\text{deg}(2)+1$

### Strict Binary Tree

A Strict Binary Tree, also known as a proper binary tree or complete binary tree, is a binary tree where the degree of each node is either 0 or 2, never 1.

#### Height vs. Nodes

The minimum number of nodes for a strict binary tree for height $h$ is $n=2h+1$, and max is the same as a non-strict node, $n=2^{h+1}+1$. The mimimum height formula is the same, it is $h=\log_2(n+1)-1$. The maximum height formula is different for a strict binary tree, it is $h=\frac{n-1}{2}$.

#### Determining no. Leaf Nodes

The number of leaf nodes/external nodes for a Strict Binary Tree is $\text{deg}(0)=\text{deg}(2)+1$

### Tree Traversals

In a linear data structure, data can be traversed in two ways, front to back, or back to front. For a non-linear data structure, like a tree, there are a lot more options at play as to how we can traverse the data structure. In this way, we will look over four methods to traverse the following trees:

1.

```
    [A]
[B]     [C]
```

2.

```
    [A]
[B]
```

3.

```
    [A]
        [B]
```

#### Preorder

Preorder is defined as:

1. Visit the current Node
2. Pre(Left Child)
3. Preorder(Right Child)

So for the first tree, `Preorder(A)` would return A, B, C. For the second tree, `Preorder(A)` would return A, B. For the third tree, `Preorder(A)` would return A, B.

#### Inorder

Inorder is defined as:

1. Inorder(Left Child)
2. Visit the current Node
3. Inorder(Right Child)

So for the first tree, `Inorder(A)` would return B, A, C. For the second tree, `Inorder(A)` would return B, A. For the third tree, `Inorder(A)` would return A, B.

#### Postorder

Postorder is defined as:

1. Postorder(Left Child)
2. Postorder(Right Child)
3. Visit the current Node

So for the first tree, `Postorder(A)` would return B, C, A. For the second tree, `Postorder(A)` would return B, A. For the third tree, `Postorder(A)` would return B, A.

#### Levelorder

Levelorder is definde as:

1. Visit the current level

So for the first tree, `Levelorder(A)` would return A, B, C. For the second tree, `Levelorder(A)` would return A, B. For the third tree, `Levelorder(A)` would return A, B.

### Representing Binary Tree

#### Array Representation

Given a binary tree such as the following:

```
                  [A]
      [B]                     [C]
[D]          [E]        [F]          [G]
```

We can feed this data into an array like the following:

```
T | A B C D E F G
    1 2 3 4 5 6 7
```

You're probably saying: "Coleton, Arrays start at Index 0 why the heck did you put 1 as the first element." Well, you'll see. This representation means the following:

| Element | Index | LChild | RChild |
| ------- | ----- | ------ | ------ |
| A       | 1     | 2      | 3      |
| B       | 2     | 4      | 5      |
| C       | 3     | 6      | 7      |
|         | i     | 2i     | 2i+1   |

This pattern showcases the usefulness of starting with 1. You can also determine the parent fast, because the parent is $\frac{i}{2}$. This concept is important for another concept, called completeness. The tree above is complete, but what about this tree:

```
           [A]
    [B]          [C]
[D]                   [E]
```

An array representation of this would look like:

```
T | 1 2 3 4 5 6 7
    A B C D - - E
```

Notice that there are spaces between D and E? Any space in an array representation of the tree means that the tree is not complete. This is a practical definition of a non-complete tree. A textbook definition of completeness is a tree such that the tree is full (left and right children for every node) at h - 1, and all nodes at h are filled left to right, and if it stops, no other nodes are present, such as this tree:

```
               [A]
     [B]                 [C]
[D]       [E]       [F]
```

Here, the height is 2, so at 1, the nodes are filled completely, and at the last level, the nodes are filled left to right, with no breaks. Notice that the right child of C is not present, the tree is still complete with it.

#### Linked Representation

A linked representation of a Binary Tree can be like this:

```cpp
class Node {
    public:
        Node *lchild;
        int data;
        Node *rchild;  
};
```

#### Creating Binary Tree

This implementation uses the Queue. Instead of rewriting our current Queue implementation to support the `Node` class, we will just use the built in `queue` in C++. To begin, lets setup the Tree Class:

```cpp
#include <queue>
#include <iostream>

using namepsace std;

class Node {
  public:
    Node *lchild;
    int data;
    Node *rchild;
};

class Tree {
  public:
    Node *root;

  Tree() {
    root = nullptr;
  }

};

Next, we need to implement a method to create a Binary Tree:

```cpp
CreateTree() {
  Node* p;
  Node* t;
  int x;
  queue<Node*> q;

  // Set the root data and then put it in the queue.
  root = new Node;
  cout << "Enter root data: " << flush;
  cin >> x;
  root->data = x;
  root->lchild = nullptr;
  root->rchild = nullptr;
  q.emplace(root);

  while (!q.empty()) {
    p = q.front();
    q.pop();

    cout << "Enter left child data of " << p->data << ": " << flush;
    cin >> x;
    if (x != -1) {
      t = new Node;
      t->data = x;
      t->lchild = nullptr;
      t->rchild = nullptr;
      p->lchild = t;
      q.emplace(t);
    }

    cout << "Enter right child data of " << p->data << ": " << flush;
    cin >> x;
    if (x != -1) {
      t = new Node;
      t->data = x;
      t->lchild = nullptr;
      t->rchild = nullptr;
      p->rchild = t;
      q.emplace(t);
    }
  }
}
```

Next, we code the traversals, the traversals implementations are pretty similar to how they are described above.

##### `Preorder`

```cpp
void Preorder(Node *p) {
  if (p) {
    cout << p->data << ", " << flush;
    Preorder(p->lchild);
    Preorder(p->rchild);
  }
}
```

##### `Postorder`

```cpp
void Postorder(Node *p) {
  if (p) {
    Postorder(p->lchild);
    Postorder(p->rchild);
    cout << p->data << ", " << flush;
  }
}
```

##### `Inorder`

```cpp
void Inorder(Node *p) {
  if (p) {
    Inorder(p->lchild);
    cout << p->data << ", " << flush;
    Inorder(p->rchild);
  }
}
```

##### `Levelorder`

```cpp
void Levelorder(Node *p) {
  queue<Node*> q;
  cout << root->data << ", " << flush;
  q.emplace(root);

  while (! q.empty()) {
    p = q.front();
    q.pop();

    if (p->lchild) {
      cout << p->lchild->data << ", " << flush;
      q.emplace(p->lchild);
    }

    if (p->rchild) {
      cout << p->rchild->data << ", " << flush;
      q.emplace(p->rchild);
    }
  }
}
```

##### `Height`

int Height(Node *p) {
  int l = 0;
  int r = 0;
  if (p == nullptr) {
    return 0;
  }

  l = Height(p->lchild);
  r = Height(p->rchild);

  if (l > r) {
    return l + 1;
  } else {
    return r + 1;
  }
}

## n-ary tree

An n-ary tree is a tree where the degree of any node is at maximum $n$, eg. a 3-ary tree can have {0, 1, 2, 3} degrees.

### Strict N-ary tree

A strict n-ary tree is a tree where the degree of any node is either {0, n}. 

#### Height vs. Nodes

For a given n-ary tree (where $n$ is given as $m$) and height, the minimum number of nodes $n$ is $n = mh+1$. The maximum number of nodes $n$ is $n=\frac{m^{h+1}-1}{m-1}$. Given the number of nodes $n$, the minimum height is $h=\log_m[n(m-1)+1]-1$, and the maximum height is $h=\frac{n-1}{m}$.

## Search Trees

### Binary Search Tree

```
              [30]
    [15]               [50]
[10]    [20]       [40]    [60]     
```

This is an example of a Binary Search Tree. Notice that to the left of each node, the value is less than the right. Notice the following:

1. No duplicates
2. Inorder traversal would give a sorted list of the elements, least to greatest.

#### Implementation

```cpp
#include <iostream>

using namespace std;

class Node{
  public:
    Node* lchild;
    int data;
    Node* rchild;
};

class BST{
  private:
    Node* root;
  public:
    // todo
};
```

##### `Insert`

```cpp
void Insert(int key) {
  Node* t = root;
  Node* p;
  Node* r;

  // root is empty
  if (root == nullptr) {
    p = new Node;
    p->data = key;
    p->lchild = nullptr;
    p->rchild = nullptr;
    root = p;
    return;
  }

  while(t != nullptr) {
    r = t;
    if (key < t->data) {
      t = t->lchild;
    } else if (key > t->data) {
      t = t->rchild;
    } else {
      return;
    }
  }

  // Now t points at NULL and r points at insert location
  p = new Node;
  p->data = key;
  p->lchild = nullptr;
  p->rchild = nullptr;

  if (key < r->data) {
    r->lchild = p;
  } else {
    r->rchild = p;
  }
}
```

##### `Inorder`

```cpp
void Inorder(Node* p) {
  if (p) {
    Inorder(p->lchild);
    cout << p->data << ", " << flush;
    Inorder(p->rchild);
  }
}
```

##### `Search`

```cpp
Node* Search(int key) {
  Node* t = root;
  while (t != nullptr) {
    if (key == t->data) {
      return t;
    } else if (key < t->data) {
      t = t->lchild;
    } else {
      t = t->rchild;
    }
  }
  return nullptr;
}
```

##### Recursive `Insert` and `Search`

```cpp
Node* rInsert(Node *p, int key) {
  Node* t;
  if (p == nullptr) {
    t = new Node;
    t->data = key;
    t->lchild = nullptr;
    t->rchild = nullptr;
    return t;
  }

  if (key < p->data) {
    p->lchild = rInsert(p->lchild, key);
  } else if (key > p->data) {
    p->rchild = rInsert(p->rchild, key);
  }
  return p;  // key == p->data?
}

Node* rSearch(Node *p, int key) {
  if (p == nullptr) {
    return nullptr;
  }

  if (key == p->data) {
    return p;
  } else if (key < p->data) {
    return rSearch(p->lchild, key);
  } else {
    return rSearch(p->rchild, key);
  }
}
```

##### `Delete`

```cpp
Node* Delete(Node *p, int key) {
  Node* q;

  if (p == nullptr) {
    return nullptr;
  }

  if (p->lchild == nullptr && p->rchild == nullptr) {
    if (p == root) {
      root = nullptr;
    }
    delete p;
    return nullptr;
  }

  if (key < p->data) {
    p->lchild = Delete(p->lchild, key);
  } else if (key > p->data) {
    p->rchild = Delete(p->rchild, key);
  } else {
    if (Height(p->lchild) > Height(p->rchild)) {
      q = InPre(p->lchild);
      p->data = q->data;
      p->lchild = Delete(p->lchild, q->data);
    } else {
      q = InSucc(p->rchild);
      p->data = q->data;
      p->rchild = Delete(p->rchild, q->data);
    }
  }
  return p;
}

Node* InPre(Node *p) {
  while (p && p->rchild != nullptr) {
    p = p->rchild;
  }
  return p;
}

Node* InSucc(Node *p) {
  while (p && p->lchild != nullptr) {
    p = p->lchild;
  }
  return p;
}
```

##### Create From Preorder

```cpp
void createFromPreorder(int *pre, int n) {
  // Create root node
  int i = 0;
  root = new Node;
  root->data = pre[i++];
  root->lchild = nullptr;
  root->rchild = nullptr;

  // Iterative steps
  Node* t;
  Node* p = root;
  stack<Node*> stk;

  while (i < n) {
    // Left child case
    if (pre[i] < p->data) {
      t = new Node;
      t->data = pre[i++];
      t->lchild = nullptr;
      t->rchild = nullptr;
      p->lchild = t;
      stk.push(p);
      p = t;
    } else {
      // Right child cases
      if (pre[i] > p->data && pre[i] < stk.empty() ? 32767 : stk.top()->data) {
        t = new Node;
        t->data = pre[i++];
        t->lchild = nullptr;
        t->rchild = nullptr;
        p->rchild = t;
        p = t;
      } else {
        p = stk.top();
        stk.pop();
      }
    }
  }
}
```

#### Drawbacks of Binary Search Tree

A drawback of a standard Binary Search Tree is the fact that they can't control their own height. Ideally, the time complexity to search the tree is $O(\log n)$, but at worst, the time complexity is $O(n)$. This is what the use of an AVL tree is. It forces the height to be more efficient.

### AVL Tree

#### Balance Factor

A balance factor of a tree is equal to the height of the left sub tree minus the height of the right subtree, or $bf = hl - hr$. A balanced node is equal to {-1, 0, 1}, or $bf = |hf - hr| \le 1$. If the |bf| at any node is greater than 1, it is imbalanced. Let's first learn to calculate balance factor.

```
            [A]
    [B]           [C]
[D]     [E]   [F]   
```

The left child height of A is 2, and the right child height of A is 2, so 2 - 2 = 0, so the BF for A is 0. The left child height of B is 1, and the right child height B is 1, so 1 - 1 = 0, so the BF for B is 0. The left child height of C is 1, and the right child height of C is 0, so 1 - 0 = 1, so the BF for C is 1. D, E, and F have no child nodes, so their BF is 0.

```
           [A]
     [B]         [C]
[D]                   [E]
```

The left child height of A is 2, and the right child height of A is 2, so 2 - 2 = 0, so the BF for A is 0. The left child height of B is 1, and the right child height of B is 0, so 1 - 0 = 1, so the BF for B is 1. The left child height of C is 0, and the right child height of C is 1, so 0 - 1 = -1, so the BF for C is -1. D and E have no child nodes, so their BF is 0.

```
            [A]
        [B]     [C]
    [D]
[E]
```

The left child height of A is 3, and the right child height of A is 1, so 3 - 1 = 2, so the BF for A is 2. The left child height of B is 2, and the right child height of B is 0, so 2 - 0 = 2, so the BF for B is 2. The left child height of D is 1, and the right child height of D is 0, so 1 - 0 = 1, so the BF for D is 1. C and E have no child nodes, so their BF is 0.

```
            [A]
        [B]     [C]
    [D]
        [E]
    [F]
```

The left child height of A is 4, and the right child height of A is 1, so 4 - 1 = 3, so the BF for A is 3. The left child height of B is 3, and the right child height of B is 0, so the BF for B is 3. The left child height of D is 0, and the right child height of D is 2, so the BF for D is -2. The left child height of E is 1, and the right child of E is 0, so the BF for E is 1. C and F have no child nodes, so their BF is 0.

#### Rotation

So this principle of balance begs the question, after we insert, we want our AVL Tree to remain balanaced. What method ensures balanace? This is where the idea of rotation comes into play. There are 4 types of rotation:

1. LL Rotation
2. RR Rotation
3. LR Rotation
4. RL Rotation

We will go over the steps for all types of rotation. Note that rotation is done with 3 nodes only. The LL and RR rotations are single rotation, and LR and RL are double rotation.

##### LL

1. Initial Creation

```
      [30]
[20]
```

2. After Inserting

Let's say we insert 10:

```
          [30]
     [20]
[10]
```

Our BF is now 2, which makes this AVL tree invalid as it is imbalanced. Notice the position, it is Left-Left: LL.

3. Rotation

So we now have our tree, how do we perform the rotation? Imagine holding your finger on 30, and then pulling on the tree like it is a string. Thus the tree looks like this:

```
     [20]
[10]      [30]
```

Now, the BF for each node is 0. 

##### RR

1. Initial Creation

```
[10]
      [20]
```

2. After Inserting

Let's say we insert 30:

```
[10]
      [20]
            [30]
```

Our BF is now -2, which makes this AVL tree invalid as it is imbalanced. Notice the position, it is Right-Right: RR.

3. Rotation

So we now have our tree, lets perform the rotation. For this one, we shift it counterclockwise:

```
     [20]
[10]      [30]
```

###### LR Rotation

1. Initial Creation

```
      [30]
[10]
```

2. After Inserting

Let's say we insert 20:

```
      [30]
[10]
      [20]
```

Our BF is now 2, which make this AVL tree invalid as it is imbalanced. Notice the position, it is Left-Right: LR.

3. Rotation

```
          [30]
     [20]
[10]
```

```
      [20]
[10]        [30]
```

If we notice, this rotation was a two step process, first we rotated it into a LL position, then performed a LL rotation.

##### RL

1. Initial Creation

```
[10]
     [30]
```

2. After Inserting

Let's say we insert 20:

```
[10]
     [30]
[20]
```

Our BF is now -2, which makes this AVL tree invalid as it is imbalanced. Notice the position, it is Right-Left: RL.

3. Rotation

```
[10]
     [30]
          [20]
```

```
      [20]
[10]        [30]
```

If we notice, this rotation was a two step process, first we rotated it into a RR position, then performed a RR rotation.

##### General Form For Rotation

Something that can be hard to determine is what rotation should be used, especially if we are using this in an algorithm. Something of note is that any rotation is just with 3 nodes. Nodes can have children, but when we are analyzing a node that is unbalanced, we only balance it using 2 other nodes. It's positions are important for the rotation, but determining this rotation can be hard to determine. The general idea is once we insert, we don't care where the node went past 3 nodes. Eg. if we insert a node, and it goes left, then right, then left, then left again, we don't care at all about the last two lefts, just the first two directions, left and right. In this case, on the node that has become unbalanced, we perform a LR Rotation.

#### Implementation

```cpp
#include <iostream>
using namespace std;

class Node {
  public:
    Node* lchild;
    int data;
    Node* rchild;
    int height; // Add height variable
};

class AVL {
  public:
    Node* root;
    AVL() { root = nullptr; }
};
```

The AVL class is very similar to the normal Binary Tree class, just with some modifications.

##### `NodeHeight`

```cpp
int NodeHeight(Node *p) {
  int hl;
  int hr;

  hl = (p && p->lchild) ? p->lchild->height : 0;
  hr = (p && p->rchild) ? p->rchild->height : 0;

  return hl > hr ? hl + 1 : hr + 1;
}
```

##### Rotations

###### `RR`

```cpp
Node* LLRotation(Node *p) {
  Node* pl = p->lchild;
  Node* plr = pl->rchild;

  pl->rchild = p;
  p->lchild = plr;

  // Update height
  p->height = NodeHeight(p);
  pl->height = NodeHeight(pl);

  // Update root
  if (root == p) {
    root = pl;
  }
  return pl;
}
```

###### `LL`

```cpp
Node* RRRotation(Node *p) {
  Node* pr = p->rchild;
  Node* prl = pr->lchild;

  pr->lchild = p;
  p->rchild = prl;

  // Update height
  p->height = NodeHeight(p);
  pr->height = NodeHeight(pr);

  // Update root
  if (root == p) {
    root = pr;
  }
  return pr;
}
```

###### `LR`

```cpp
Node* LRRotation(Node *p) {
  Node* pl = p->lchild;
  Node* plr = pl->rchild;

  pl->rchild = plr->lchild;
  p->lchild = plr->rchild;

  plr->lchild = pl;
  plr->rchild = p;

  // Update height
  pl->height = NodeHeight(pl);
  p->height = NodeHeight(p);
  plr->height = NodeHeight(plr);

  // Update root
  if (p == root) {
    root = plr;
  }
  return plr;
}
```

###### `RL`

```cpp
Node* AVL::RLRotation(Node *p) {
  Node* pr = p->rchild;
  Node* prl = pr->lchild;

  pr->lchild = prl->rchild;
  p->rchild = prl->lchild;

  prl->rchild = pr;
  prl->lchild = p;

  // Update height
  pr->height = NodeHeight(pr);
  p->height = NodeHeight(p);
  prl->height = NodeHeight(prl);

  // Update root
  if (root == p) {
    root = prl;
  }
  return prl;
}
```

###### `Insert`

```cpp
Node* rInsert(Node *p, int key) {
  Node* t;
  if (p == nullptr) {
    t = new Node;
    t->data = key;
    t->lchild = nullptr;
    t->rchild = nullptr;
    t->height = 1;  // Starting height from 1 onwards instead of 0
    return t;
  }

  // Determine if it is supposed to be at the left or right
  if (key < p->data) {
    p->lchild = rInsert(p->lchild, key);
  } else if (key > p->data) {
    p->rchild = rInsert(p->rchild, key);
  }

  // Update height
  p->height = NodeHeight(p);

  // Balance Factor and Rotation
  if (BalanceFactor(p) == 2 && BalanceFactor(p->lchild) == 1) {
    return LLRotation(p);
  } else if (BalanceFactor(p) == 2 && BalanceFactor(p->lchild) == -1) {
    return LRRotation(p);
  } else if (BalanceFactor(p) == -2 && BalanceFactor(p->rchild) == -1) {
    return RRRotation(p);
  } else if (BalanceFactor(p) == -2 && BalanceFactor(p->rchild) == 1) {
    return RLRotation(p);
  }

  return p;
}
```

##### Display

```cpp
void Inorder(Node *p) {
  if (p) {
    Inorder(p->lchild);
    cout << p->data << ", " << flush;
    Inorder(p->rchild);
  }
}
```

##### `Delete`

```cpp
Node* InPre(Node *p) {
  while (p && p->rchild != nullptr) {
    p = p->rchild;
  }
  return p;
}

Node* InSucc(Node *p) {
  while (p && p->lchild != nullptr) {
    p = p->lchild;
  }
  return p;
}

Node* Delete(Node *p, int key) {
    if (p == nullptr) {
        return nullptr;
    }

    if (p->lchild == nullptr && p->rchild == nullptr) {
        if (p == root) {
            root = nullptr;
        }
        delete p;
        return nullptr;
    }

    if (key < p->data) {
        p->lchild = Delete(p->lchild, key);
    } else if (key > p->data) {
        p->rchild = Delete(p->rchild, key);
    } else {
        Node* q;
        if (NodeHeight(p->lchild) > NodeHeight(p->rchild)) {
            q = InPre(p->lchild);
            p->data = q->data;
            p->lchild = Delete(p->lchild, q->data);
        } else {
            q = InSucc(p->rchild);
            p->data = q->data;
            p->rchild = Delete(p->rchild, q->data);
        }
    }

    // Update height
    p->height = NodeHeight(p);

    // Balance Factor and Rotation
    if (BalanceFactor(p) == 2 && BalanceFactor(p->lchild) == 1) {  // L1 Rotation
        return LLRotation(p);
    } else if (BalanceFactor(p) == 2 && BalanceFactor(p->lchild) == -1) {  // L-1 Rotation
        return LRRotation(p);
    } else if (BalanceFactor(p) == -2 && BalanceFactor(p->rchild) == -1) {  // R-1 Rotation
        return RRRotation(p);
    } else if (BalanceFactor(p) == -2 && BalanceFactor(p->rchild) == 1) {  // R1 Rotation
        return RLRotation(p);
    } else if (BalanceFactor(p) == 2 && BalanceFactor(p->lchild) == 0) {  // L0 Rotation
        return LLRotation(p);
    } else if (BalanceFactor(p) == -2 && BalanceFactor(p->rchild) == 0) {  // R0 Rotation
        return RRRotation(p);
    }

    return p;
}
```

### Binary Heap

A binary heap is a binary tree where duplicates are allowed. Further more, there are two types of binary heaps, a max heap and a min heap. In a max heap, it means that each element is greater than or equal to its children. Obviously, the min heap means that each element is less than or equal to its children. Binary heaps are almost always represented as arrays, and they are complete trees. In other words, there are no gaps in the array, and ecah level is filled left to right. This is an example of a max heap:

```
            [30]
    [20]            [15]
[5]      [10]  [12]      [6]
```

As you can see, each node's value is greater than or equal to the children, eg. 30 >= 20 & 15. Here is an example of a min heap:

```
              [5]
     [15]            [12]
[20]      [25]  [30]      [18]
```

The opposite fact is true here, where each node's value is less than or equal to the childre, eg. 5 <= 15 & 12. the max heap is the most used form of binary heap. Let's look at the binary representation of the max heap.

```
B | 30 20 15 5  10 12 6
    1  2  3  4  5  6  7
```

Recall that a Node is at Index I, thus its left child is at 2i and its right child is at 2i+1. 

#### Insertion

A heap is cool, but because it has to stay complete, there can't be any gaps in the array. Imagine we have the above array, and we want to insert the value 40. What do we do? Well, we just insert at the end of our array.

```
B | 30 20 15 5  10 12 6  40
    1  2  3  4  5  6  7  8
```

This is nice and easy, but there is one crucial problem, this makes 40 a child of 5. It cannot be a child of 5, that doesn't work. How do we go about remedying this problem? Well, we compare 40 with its parents, if it is greater than the parent element, we swap the parent with 40, lets see how this operation would take place:

40 > 5, Swap:

```
B | 30 20 15 40 10 12 6  5
    1  2  3  4  5  6  7  8
```

40 > 20, Swap:

```
B | 30 40 15 20 10 12 6  5
    1  2  3  4  5  6  7  8
```

40 > 30, Swap:

```
B | 40 30 15 20 10 12 6  5
    1  2  3  4  5  6  7  8
```

Now the tree looks like:

```
               [40]
        [30]         [15]
    [20]    [10] [12]    [6]
[5]
```

#### Implementation with Array

##### `Insert`

```cpp
void Insert(int A[], int n) {
  int i = n;
  int temp = A[n];
  // Instead of using if statements, we use a short hand if..else statement.
  while (i > 0 && temp > A[i % 2 == 0 ? (i / 2) - 1 : i / 2]) {
    A[i] = A[i % 2 == 0 ? (i / 2) - 1 : i / 2];
    i = i % 2 == 0 ? (i / 2) - 1 : i / 2;
  }
  A[i] = temp;
}
```

##### `CreateHeap`

```cpp
void CreateHeap(int A[], int n) {
  for (int i = 0; i < n; i++) {
    Insert(A, i);
  }
}
```

##### `Delete`

Something of note about `Delete`, is that it also sorts the heap. Basically, when we delete, we are always removing the top element by swapping it with the last index in the heap array. Afterwards, we do the insert logic, basically moving the swapped value to its proper place in the heap. Repeated deletions push the max value further and further down the array, moving each one out of the scope of the array, but also sorted. This is useful, as it basically creates a priority queue, which we will explore later.

```cpp
void swap(int A[], int i, int j) {
  int temp = A[i];
  A[i] = A[j];
  A[j] = temp;
}

int Delete(int A[], int n) {
  int x = A[0];  // Max element
  A[0] = A[n - 1];

  int i = 0;
  int j = 2 * i + 1;

  while (j < n - 1) {
    // Compare left and right children, greater
    // value gets priority.
    if (A[j] < A[j + 1]) {
      j = j+1;
    }

    // Compare parent and largest child
    // if our current value is less than the child,
    // we swap, else we are where we should be and we break
    if (A[i] < A[j]) {
      swap(A, i, j);
      i = j;
      j = 2 * i + 1;
    } else {
      break;
    }
  }
  return x;
}

##### `Heapify`
When we consider what `Insert` and `Delete` are really doing, they are both making adjustments to the tree, just insert is going leaf to root, and delete is going root to leaf. The method for creating a heap uses similar principles, and its time complexity is $O(n \log n)$. Heapify is a method to create a binary heap tree that is faster. Instead of going left to right, heapify works right to left, and instead of working from root to leaf, it works leaf to root, which is a lot more efficient, possessing a time complexity of $O(n)$.

```cpp
void Heapify(int A[], int n) {
  // # of leaf elements: (n+1)/2, index of last leaf element's parent = (n/2)-1
  for (int i=(n/2)-1; i>=0; i--) {

    int j = 2 * i + 1;  // Left child for current i

    while(j < n-1) {
      // Compare left and right children of current i
      if (A[j] < A[j+1]) {
        j = j+1;
      }

      // Compare parent and largest child
      if (A[i] < A[j]) {
        swap(A, i, j);
        i = j;
        j = 2 * i + 1;
      } else {
        break;
      }
    }
  }
}
```

#### Implementation with Vector

##### `Insert`

```cpp
#include <iostream>
#include <vector>

using namespace std;

void Insert(vector<int>& vec, int key) {
    // Insert key at the end
    auto i = vec.size();
    vec.emplace_back(key);

    // Rearrange elements: O(log n)
    while (i > 0 && key > vec[i % 2 == 0 ? (i / 2) - 1 : i / 2]) {
        vec[i] = vec[i % 2 == 0 ? (i / 2) - 1 : i / 2];
        i = i % 2 == 0 ? (i / 2) - 1 : i / 2;
    }
    vec[i] = key;
}
```

##### `CreateHeap`

Takes an array of values and puts them into a vector

```cpp
void CreateHeap(vector<int>& vec, int A[], int n) {
    // O(n log n)
    for (int i = 0; i < n; i++) {
        Insert(vec, A[i]);
    }
}
```

##### `Print`

To display the binary heap:

```cpp
template <class T>
void Print(T& vec, int n, char c) {
    cout << c << ": [" << flush;
    for (int i = 0; i < n; i++) {
        cout << vec[i] << flush;
        if (i < n - 1) {
            cout << ", " << flush;
        }
    }
    cout << "]" << endl;
}
```

#### Heap As a Priority Queue

Due to the very nature of the binary heap, whenever we insert into it, the largest or smallest value takes precedence. This allows us to build a priority queue. Insert is $O\log n$ and Delete is $O(\log n)$. This makes a binary heap the best structure for a priority queue.

# Sorting

The definition of sorting is pretty easy to understand, it is an algorithm that sorts data. Some sorts are better for certain applications. The analysis of a sort will be based on this criteria to determine its situational efficiency:

1. Number of comparisons
2. Number of swaps
3. Adaptive
4. Stable
5. Extra Memory

## General Overview

### Comparison Based Sorts

#### $O(n^2)$

1. Bubble Sort
2. Insertion Sort
3. Selection Sort

#### $O(n \log n)$

1. Heap Sort
2. Merge Sort
3. Quick Sort
4. Tree Sort

#### $O(n^{\frac{3}{4}})$

1. Shell Sort

### Index Based Sorts

#### $O(n)$

1. Count Sort
2. Bucket/Bin Sort
3. Radix Sort

## Stable

Stable sorting algorithms preserve the relative order of equal elements. For example, imgaine I have a list of student names with corresponding grades. Currently, the list is sorted alphabetically, but imagine I want to sort numerically. A stable sorting algorithm would not change the relative order of duplicates, thus a student with a first name A with a score of say 80 would be ahead of a student with a first name B with a score of 80. The use of a stable algorithm is that it makes it more efficient when there are duplicate cases, as we don't have to sort by another key when a duplicate is present.

## Adaptive

Adaptive sorting algorithms take advantage of existing order in its inputs, and this advantage makes it faster by not trying to reorder if it is already ordered. Bubble Sort and Insertion Sort are examples of adaptive sorting algorithms.

## Synopsis and Implementation of Each Sort

### Bubble Sort

#### Synopsis

Bubble sort is the most intuitive sorting algorithm, it basically just passes over a list of elements, comparing the first element with every other element, and then does the same thing for the second, third, fourth, etc.

#### Implementation

```cpp
void BubbleSort(int A[], int n) {
  int flag = 0;
  for (int i = 0; i < n - 1; i++) {
    for (int j = 0; j < n - 1- i; j++) {
      if (A[j] > A[j + 1]) {
        swap(&A[j], &A[j + 1]);
        flag = 1;
      }
    }
    if (flag == 0) {
      return;
    }
  }
}
```

##### `Print`

It can be assumed that this print method will be included with every implementation from here onwards:

```cpp
#include <iostream>

using namespace std;

template <class T>
void Print(T& vec, int n, string s) {
  cout << s << ": [" << flush;
  for (int i = 0; i < n; i++) {
    cout << vec[i] << flush;
    if (i < n - 1) {
      cout << ", " << flush;
    }
  }
  cout << "]" << endl;
}
```

##### `swap`

It can be assumed that this swpa method will be included with every implementation from here onwards (when required):

```cpp
void swap(int* x, int* y) {
  int temp = *x;
  *x = *y;
  *y = temp;
}
```

### Insertion Sort

#### Synopsis

Insertion is a pretty basic principle, given the sorted array below:

```
A | 2   4   8   16  32
    0   1   2   3   4
```

We want to insert the value `9`. To do this, we'd logically have to shift values rightward, but we can't shift every element at once. The easiest way to do this is the following:

Is 9 > 32? No. Shift rightward.

```
A | 2   4   8   16      32
    0   1   2   3   4   5
```

Is 9 > 16? No. Shift rightward.

```
A | 2   4   8       16  32
    0   1   2   3   4   5
```

Is 9 > 8? Yes. Place at empty:

```
A | 2   4   8   9   16  32
    0   1   2   3   4   5
```

In this way, we are only shifting the elements we need at any point, all in one scan. This principle of shifting with each insert is how insert sort works. Given an unsorted array:

```
A | 8   2   12  4   6   20
    0   1   2   3   4   5
```

Each step in an insertion sort requires breaking the array into seperate parts. First step is breaking off the 0 index, which is sorted by definition as it is only one element. Second step is adding an extra spot, and doing an insertion:

Is 2 > 8? No. Shift rightward.

```
I | 2   8
    0   1

A |    [2]  12  4   6   20
    0   1   2   3   4   5
```

Break off next element, 12:

Is 12 > 8? Yes. Place at empty.

```
I | 2   8   12
    0   1   2

A |       [12]  4   6   20
    0   1   2   3   4   5
```

Break off next element, 4:

Is 4 > 12? No. Shift rightward. 

```
I | 2   8       12  
    0   1   2   3

A |            [4]  6   20
    0   1   2   3   4   5
```

Is 4 > 8? No. Shift rightward.

```
I | 2       8   12  
    0   1   2   3

A |            [4]  6   20
    0   1   2   3   4   5
```

Is 4 > 2? Yes. Place at empty.

```
I | 2   4   8   12  
    0   1   2   3

A |            [4]  6   20
    0   1   2   3   4   5
```

We continue this proces until the very end.

#### Implementation

```cpp
void InsertionSort(int A[], int n) {
  for (int i = 1; i < n; i++) {
    int j = i - 1;
    int x = A[i];
    while (j > -1 && A[j] > x) {
      A[j + 1] = A[j];
      j--;
    }
    A[j + 1] = x;
  }
}
```

### Bubble Sort vs. Insertion Sort

| Comparisons | Bubble Sort | Insertion Sort |
| ----------- | ----------- | -------------- |
| Min Comp    | $O(n)$      | $O(n)$         |
| Max Comp    | $O(n^2)$    | $O(n^2)$       |
| Min Swap    | $O(1)$      | $O(1)$         |
| Max Swap    | $O(n^2)$    | $O(n^2)$       |
| Adaptive    | Yes         | Yes            |
| Stable      | Yes         | Yes            |
| Linked List | No          | Yes            |
| k passes    | Yes         | No             |

### Selection Sort

#### Synopsis

Selection sort utilizes three variables, `i` which denotes current position, `k` which denotes next smallest value, and `j` which denotes current index being scanned. When `j` goes outside index, the pass is complete. Each pass stores the minimum value, and swaps it with the current index. Let's see this in action:

```
A | 8 6 3 2 5 4
    0 1 2 3 4 5
```

i = 0, scan for smallest value:

```
i = 0
k = 3
j = 6

Swap:

A | 2 6 3 8 5 4
    0 1 2 3 4 5
```

i = 1, scan for smallest value:

```
i = 1
k = 2
j = 6

Swap:

A | 2 3 6 8 5 4
    0 1 2 3 4 5
```

i = 2, scan for smalled value

```
i = 2
k = 5
j = 6

Swap:

A | 2 3 4 8 5 6
    0 1 2 3 4 5
```

We continue this process until the list is sorted. Selection sort is neither adaptive or stable, but it has a low memory footprint and works exceptionally well on small sets of data.

#### Implementation

```cpp
void SelectionSort(int A[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int j;
        int k;
        for (j = k = i; j < n; j++) {
            if (A[j] < A[k]) {
                k = j;
            }
        }
        swap(&A[i], &A[k]);
    }
}
```

### Quick Sort

#### Synopsis

Quick Sort can be confusing, but this is because the sort has a lot of steps that aren't intuitive. But, once you understand the steps, it becomes rather easy. To begin, let's look at this array:

```
A | 50  70  60  90  40  80  10  20  30
    0   1   2   3   4   5   6   7   8
```

To begin, set the first element as the pivot element. The idea behind quicksort is that we determine a place that is sorted, so each value left of the pivot is less than or equal to the pivot, and eveything to the right of the pivot is greater than or equal to the pivot. So, `i` looks for everything greater than to the pivot, and `j` looks for everything less than or equal to the pivot. So i starts at 0, and j starts at length of array:

1. ```
   // First element greater than 50 is 70 at 1:
   i = 1
   ```

// First element less than or equal to 50 is 30 at 8:
j = 8

Swap:
A | 50  30  60  90  40  80  10  20  70
    0   1   2   3   4   5   6   7   8

```
2.
```

// Next element greater than 50 is 60 at 2:
i = 2

// Next element less than or equal to 50 is 20 at 7:
j = 8

Swap:
A | 50  30  20  90  40  80  10  60  70
    0   1   2   3   4   5   6   7   8

```
3.
```

// Next element greater than 50 is 90 at 3:
i = 3

// Next element less than or equal to 50 is 10 at 6:
j = 6

Swap:
A | 50  30  20  10  40  80  90  60  70
    0   1   2   3   4   5   6   7   8

```
4.
```

// Next element greater than 50 is 80 at 5:
i = 5

// Next element less than or equal to 50 is 40 at 4:
j = 4

j < i, swap pivot with j:
A | 40  30  20  10  50  80  90  60  70
    0   1   2   3   4   5   6   7   8

```
Now that we have swapped pivot with j, we are in a position where pivot is sorted. Everything to the left of 50 is less than or equal to 50, and everything to the right 50 is greater than or equal to 50. This position is called the partitioning position. And with it, we can apply, recursively, quick sort to the left and quick sort to the right. If the list is already sorted, Quick Sort is at worst time, which is $O(n^2)$. The average and best case time complexity is $O(n\log n)$

#### Implementation

##### Pivot First
```cpp
int partition(int A[], int low, int high) {
  int pivot = A[low];
  int i = low + 1;
  int j = high;

  while (true) {
    while (i <= j && A[i] <= pivot) {
      i++;
    }
    while (A[j] >= pivot && j >= i) {
      j--;
    }
    if (j < i) {
      break;
    } else {
      swap(&A[i], &A[j]);
    }
  }
  swap(&A[low], &A[j]);
  return j;
}

void QuickSort(int A[], int low, int high) {
  if (low < high) {
    int p = partition(A, low, high);
    QuickSort(A, low, p - 1);
    QuickSort(A, p + 1, high);
  }
}
```

##### Pivot Last

```cpp
int partitionLast(int A[], int low, int high) {
  int pivot = A[high];
  int i = low - 1;
  for (int j = low; j <= high - 1; j++) {
    if (A[j] < pivot) {
      i++;
      swap(&A[i], &A[j]);
    }
  }
  swap(&A[i + 1], &A[high]);
  return i + 1;
}

void QuickSortLast(int A[], int low, int high) {
  if (low < high) {
    int p = partitionLast(A, low, high);
    QuickSortLast(A, low, p - 1);
    QuickSortLast(A, p + 1, high);
  }
}
```

### Merge Sort

#### Synopsis

##### Ideas Behind Merging

Given two sorted arrays, we are going to incremement over each and merge, eg.:

```
n = 0
A | 1 5 12
    0 1 2

m = 0
B | 3 4 9 10
    0 1 2 3

New Array:
C | 
    0 1 2 3 4 5 6

n = 0
m = 0
A[n] = 1
B[m] = 3
A[n] < B[m]:
C | 1
    0 1 2 3 4 5 6
n++

n = 1
m = 0
A[n] = 5
B[m] = 3
B[m] < A[n]:
C | 1 3
    0 1 2 3 4 5 6
m++

n = 1
m = 1
A[n] = 5
B[m] = 4
B[m] < A[n]:
C | 1 3 4
    0 1 2 3 4 5 6
m++

n = 1
m = 2
A[n] = 5
B[m] = 9

A[n] < B[m]
C | 1 3 5
    0 1 2 3 4 5 6
n++

n = 2
m = 2
A[n] = 12 
B[m] = 9
B[m] < A[n]
C | 1 3 5 9
    0 1 2 3 4 5 6
m++

n = 2
m = 3
A[n] = 12
B[m] = 10
B[m] < A[n]
C | 1   3   5   9   10
    0   1   2   3   4
m++

n = 2
m = 4
A[n] = 12
B[m] Does Not Exist
C | 1   3   5   9   10    12
    0   1   2   3   4     5
```

###### Implementation of Merge Concepts

```cpp
void Merge(int x[], int y[], int z[], int m, int n) {
  int i = 0;
  int j = 0;
  int k = 0;

  // Copy least greatest element from each array at each index pair
  while (i < m && j < n) {
    if (x[i] < y[j]) {
      z[k++] = x[i++];
    } else {
      z[k++] = y[j++];
    }
  }

  // Only one of the following _Noreturn
  // Copy remaining items in x if present
  while (i < m) {
    z[k++] = x[i++];
  }

  // Copy remaining items in y if present
  while (j < n) {
    z[k++] = x[j++];
  }
}

void MergeSingle(int A[], int low, int mid, int high) {
  // Lowest Index
  int i = low;
  // Middle Index
  int j = mid + 1;
  // Highest Index
  int k = low;

  int B[high + 1];
  while (i <= mid && j <= high) {
    if (A[i] < A[j]) {
      B[k++] = A[i++];
    } else {
      B[k++] = A[j++];
    }
  }
  while (i <= mid) {
    B[k++] = A[i++];
  }
  while (j <= high) {
    B[k++] = A[j++];
  }
  for (int i=low; i<=high; i++) {
    A[i] = B[i];
  }
}
```

#### Implementation

##### Iterative Merge Sort

```cpp
void IterativeMergeSort(int A[], int n) {
  int p;
  for (p = 2; p <= n; p = p * 2) {
    for (int i = 0; i + p - 1 < n; i = i + p) {
      int low = i;
      int high = i + p - 1;
      int mid = (low + high) / 2;
      Merge(A, low, mid, high);
    }
  }
  if (p / 2 < n) {
    Merge(A, 0, p / 2 - 1, n - 1);
  }
}
```

##### Recursive Merge Sort

```cpp
void RecursiveMergeSort(int A[], int low, int high) {
  if (low < high) {
    // Calculate mid point
    int mid = low + (high - low) / 2;

    // Sort sub-lists
    RecursiveMergeSort(A, low, mid);
    RecursiveMergeSort(A, mid + 1, high);

    // Merge sorted sub-lists
    Merge(A, low, mid, high);
  }
}
```

### Count Sort

#### Synopsis

First, find the largest value in your array. Create an array where the last index is equal to that value, eg. a max value of 15 would be an array size 16. Initialize the array with zeros. This is important for what we are about to do. So with the given array, create another array with this directions:

```
A | 6   3   9   10  15  6   8   12  3   6
    0   1   2   3   4   5   6   7   8   9

15 is max value:
C | 0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
    0   1   2   3   4   5   6   7   8   9   10  11  12  13  14  15  
```

Next, scan the array and increment with each value, eg.:

```
A | 6   3   9   10  15  6   8   12  3   6
    0   1   2   3   4   5   6   7   8   9

C | 0   0   0   2   0   0   3   0   1   1   1   1   0   0   0   1
    0   1   2   3   4   5   6   7   8   9   10  11  12  13  14  15  
```

Notice, there are 3 6 values in our `A` array, and there is only one 8. We denote each count. Next, we clear the `A` array, and scan the `B` array, copying the number of times we see each value:

```
A | 3   3   6   6   6   8   9   10  12  15
    0   1   2   3   4   5   6   7   8   9
```

The time complexity for count sort is $O(n)$! But, the space complexity is large, being $O(k)$, where k is the largest value in our set. For small values, this sorting method is incredibly good, but for large sets, it can be very memory intensive.

#### Implementation

```cpp
int Max(int A[], int n) {
  int max = -32768;
  for (int i=0; i<n; i++) {
    if (A[i] > max) {
      max = A[i];
    }
  }
  return max;
}

void CountSort(int A[], int n) {
  int max = Max(A, n);

  // Create count array
  int* count = new int [max + 1];

  // Initialize count array with 0
  for (int i=0; i<max+1; i++) {
    count[i] = 0;
  }

  // Update count array values based on A values
  for (int i=0; i<n; i++) {
    count[A[i]]++;
  }

  // Update A with sorted elements
  int i = 0;
  int j = 0;
  while (j < max+1) {
    if (count[j] > 0) {
      A[i++] = j;
      count[j]--;
    } else {
      j++;
    }
  }

  // Delete heap memory
  delete [] count;
}
```

### Bucket Sort

#### Synopsis

Bucket Sort is very similar to Count Sort, especially with the initial step, where we create an array the size of the max step. Each value will be set to null. The type of array is a linked list, it is an array of linked lists. So the "buckets" are linked lists, so at L[6], where L is an array of linked lists, there is a linked list of every 6 element in the list.

#### Implementation

Include the nodes:

```cpp
int Delete(Node** ptrBins, int idx) {
  Node* p = ptrBins[idx];  // ptrBins[idx] is head ptr
  ptrBins[idx] = ptrBins[idx]->next;
  int x = p->value;
  delete p;
  return x;
}

void BinSort(int A[], int n) {
  int max = Max(A, n);

  // Create bins array
  Node** bins = new Node* [max + 1];

  // Initialize bins array with nullptr
  for (int i=0; i<max+1; i++) {
    bins[i] = nullptr;
  }

  // Update count array values based on A values
  for (int i=0; i<n; i++) {
    Insert(bins, A[i]);
  }

  // Update A with sorted elements
  int i = 0;
  int j = 0;
  while (i < max+1) {
    while (bins[i] != nullptr) {
      A[j++] = Delete(bins, i);
    }
    i++;
  }

  // Delete heap memory
  delete [] bins;
}
```

### Radix Sort

#### Synopsis

Radix sort also works on the bin principle, but instead of taking max value as the size, it uses the base. So for the decimal system, base 10, we have 10 bins, 0-9. So for value say, 278, it goes in bin 8. Well that is cool, but the issue is that this isn't sorted, well, drop everything and then extract. Set bins to null again, and then sort by second space, eg. 257 goes in the 5 bin. Do this again for each space, and you'll get a sorted array:

#### Implementation

```cpp
int getBinIndex(int x, int idx) {
  return (int)(x / pow(10, idx)) % 10;
}

void RadixSort(int A[], int n) {
  int max = Max(A, n);
  int nPass = countDigits(max);

  // Create bins array
  Node** bins = new Node* [10];

  // Initialize bins array with nullptr
  initializeBins(bins, 10);

  // Update bins and A for nPass times
  for (int pass=0; pass<nPass; pass++) {

    // Update bins based on A values
    for (int i=0; i<n; i++) {
      int binIdx = getBinIndex(A[i], pass);
      Insert(bins, A[i], binIdx);
    }

    // Update A with sorted elements from bin
    int i = 0;
    int j = 0;
    while (i < 10) {
      while (bins[i] != nullptr) {
        A[j++] = Delete(bins, i);
      }
      i++;
    }
    // Initialize bins with nullptr again
    initializeBins(bins, 10);
  }

  // Delete heap memory
  delete [] bins;
}
```

### Shell Sort

#### Synopsis

The grand finale, quite honestly this sort is definitely the weirdest, and probably the most complex. Basic principle is insert sort modified, where we form arrays based on gaps, eg.

```
A | 2   1   3   5   6
    0   1   2   3   4

Gap = 5 / 2 = 2

First gap set:

A | 2   1   3   5   6
    0   1   2   3   4
    *       *       *
[2, 3, 6]
```

We perform insertion sort on each set, looking at the first pair of each gap while increasing rightward.

#### Implementation

```cpp
void ShellSort(int A[], int n) {
  for (int gap = n / 2; gap >= 1; gap /= 2) {
    for (int j = gap; j < n; j++) {
      int temp = A[j];
      int i = j - gap;
      while (i >= 0 && A[i] > temp) {
        A[i + gap] = A[i];
        i = i - gap;
      }
      A[i + gap] = temp;
    }
  }
}
```

## Hashing

So far we have looked at two searching algorithms, the Linear Search with a time complexity of $O(n)$ and the Binary Search with a time complexity of $O(\log n)$. These algorithms aren't bad by any means, and in the case of Binary Search, relatively efficient. But, we can go further, we can do searching in $O(1)$. This is done with Hashing. 

### Ideal Hashing

Ideal Hashing is the most straightforward Hashing method. How it is done is that there is a one-to-one correspondence between key value and key location. So, imagine we have these set of keys:

[1, 12, 3, 7, 10, 15]

Then, the hashtable will look like this:

```
/   1   /   3   /   /   /   7   /   /   10  /   12
0   1   2   3   4   5   6   7   8   9   10  11  12
```

Where there isn't a value, it is null, otherwise the hashtable returns the value at that index. Thus, the mathematical representation for this hashtable is $h(x) = x$. This is cool but what if one of our keys is 100? 1000? That'd make so much wasted space. This is the largest drawback of ideal hashing, its memory footprint is massive.

### Modulus Hashing

Instead of just returning x, let's instead use the modulus operator. This means that the space taken up by the hashtable is 0-9, 10 spaces. The drawback is that 15 % 10 = 5, and 25 % 10 = 5, which means that if both of these elements are present, for instance, there would be a collision. It is not one-to-one, it is many-to-one. So we have to resolve these collisions.

### Open Hashing (Chaining)

Remember, the modulus hash function is $h(x) = x \bmod 10$, but we also are running into the problem of conficts. An intuitive idea is to use a linked list for conflicts, so we create an array of nodes, and each node contains a linked list of the elements. So for the 5, we can shovel any value that ends with 5, and if we wanted to search for 25, we can just search the linked list belonging to the 5th element. So, what is the time complexity? Well, first we have to determine what is called the loading factor. The loading factor $\lambda = \frac{n}{\text{size}}$. The size of the hastable is 10, so for example if we have 100 keys, then our loading factor $\lambda$ is equal to 10. The average successful search time complexity is $t = 1 + \frac{\lambda}{2}$. The average unsuccessful search time complexity is $t = 1 + \lambda$.

#### Implementation

```cpp
class Node{
  public:
    int data;
    Node* next;
};

class HashTable{
  public:
    Node** HT;
    HashTable() {
      HT = new Node* [10];
      for (int i = 0; i < 10; i++) {
        HT[i] = nullptr;
      }
    }

    int hash(int key) {
      return key % 10;
    }

    void Insert(int key) {
      int hIdx = hash(key);
      Node* t = new Node;
      t->data = key;
      t->next = nullptr;
      // Case: No nodes in the linked list
      if (HT[hIdx] == nullptr) {
        HT[hIdx] = t;
      } else {
        Node* p = HT[hIdx];
        Node *q=HT[hIdx];
        // Traverse to find insert position
        while (p && p->data < key) {
          q=p;
          p = p->next;
        }
        // Case: insert position is first
        if (q == HT[hIdx]) {
          t->next = HT[hIdx];
          HT[hIdx] = t;
        } else {
          t->next = q->next;
          q->next = t;
        }
      }
    }

    int Search(int key) {
      int hIdx = hash(key);
      Node* p = HT[hIdx];
      while (p) {
        if (p->data == key) {
          return p->data;
        }
        p = p->next;
      }
      return -1;
    }

    ~HashTable() {
      for (int i = 0; i < 10; i++) {
        Node* p = HT[i];
        while (HT[i]) {
          HT[i] = HT[i]->next;
          delete p;
          p = HT[i];
        }
      }
      delete [] HT;
    }
};
```

### Closed Hashing

Closed Hashing is the idea that the hashing doesn't take up any more memory than just the space set out for it. With chaining, we increase outside of the space of it. 

#### Linear Probing

Linear Probing is a way to solve the collisions in a finite space. To do this, we use our hash function $h(x) = x \bmod 10$, and we use a new function, $\h'(x) = (h(x) + f(i)) \bmod 10$, where $f(i) = i$. So for instance, we have the following hashtable:

```
H | 30  /   /   23  /   45  26  /   /   /
    0   1   2   3   4   5   6   7   8   9
```

We want to insert the value 25, but oh no we have a collision. Let's use $h'(x)$. $h'(x) = (h(25) + f(0)) \bmod 10 = (5 + 0) \bmod 10 = 5$. Well here, index 5 isn't available, so let's try again. $h'(x) = (h(25) + f(1)) \bmod 10 = (5 + 1) \bmod 10 = 6$. Well here, index 6 isn't available, so let's try again. $h'(x) = (h(25) + f(2)) \bmod 10 = (5 + 2) \bmod 10 = 7$. Well here, index 7 is available, so we insert our new key here.

##### Implementation

```cpp
#define SIZE 10

int Hash(int key) {
  return key % SIZE;
}

int LinearProbe(int H[], int key) {
  int idx = Hash(key);
  int i = 0;
  while (H[(idx + i) % SIZE] != 0) {
    i++;
  }
  return (idx + i) % SIZE;
}

void Insert(int H[], int key) {
  int idx = Hash(key);

  if (H[idx] != 0) {
    idx = LinearProbe(H, key);
  }
  H[idx] = key;
}

int Search(int H[], int key) {
  int idx = Hash(key);
  int i = 0;
  while (H[(idx + i) % SIZE] != key) {
    i++;
    if (H[(idx + i) % SIZE] == 0) {
      return -1;
    }
  }
  return (idx + i) % SIZE;
}
```

#### Quadratic Probing

Quadratic Probing is just like linear probing, but $h'(x)$ is redefined as $h'(x) = (h(x) + f(i)) \bmod 0$, where $f(i) = i^2$.

##### Implementation

```cpp
int Hash(int key) {
  return key % SIZE;
}

int QuadraticProbe(int H[], int key) {
  int idx = Hash(key);
  int i = 0;
  while (H[(idx+i * i) % SIZE] != 0) {
    i++;
  }
  return (idx + i * i) % SIZE;
}

void Insert(int H[], int key) {
  int idx = Hash(key);

  if (H[idx] != 0) {
    idx = QuadraticProbe(H, key);
  }
  H[idx] = key;
}

int Search(int H[], int key) {
  int idx = Hash(key);
  int i = 0;
  while (H[(idx + i * i) % SIZE] != key) {
    i++;
    if (H[(idx + i * i) % SIZE] == 0) {
      return -1;
    }
  }
  return (idx + i*i) % SIZE;
}
```

#### Double Hashing

Double Hashing uses two hash functions to try and fix conflicts. So, $h_1(x) = x \bmod 10$ and $h_2(x) = R - (x \bmod R)$, where $R$ is the nearest prime number of the size of our hashtable. So for a size of 10, $R = 7$, so $h_2(x) = 7 - (x \bmod 7)$. $h_2$ never returns 0 and it covers all of the indices. Now, $h'(x) = (h_1(x) + i * h_2(x)) \bmod 10$, where $i = 0, 1, 2...$. 

##### Implementation

```cpp
#define SIZE 10
#define PRIME 7

int Hash(int key) {
  return key % SIZE;
}

int PrimeHash(int key) {
  return PRIME - (key % PRIME);
}

int DoubleHash(int H[], int key) {
  int idx = Hash(key);
  int i = 0;
  while (H[(Hash(idx) + i * PrimeHash(idx)) % SIZE] != 0) {
    i++;
  }
  return (idx + i * PrimeHash(idx)) % SIZE;
}

void Insert(int H[], int key) {
  int idx = Hash(key);

  if (H[idx] != 0) {
    idx = DoubleHash(H, key);
  }
  H[idx] = key;
}

int Search(int H[], int key) {
  int idx = Hash(key);
  int i = 0;
  while (H[(Hash(idx) + i * PrimeHash(idx)) % SIZE] != key) {
    i++;
    if (H[(Hash(idx) + i * PrimeHash(idx)) % SIZE] == 0) {
      return -1;
    }
  }
  return (Hash(idx) + i * PrimeHash(idx)) % SIZE;
}
```
