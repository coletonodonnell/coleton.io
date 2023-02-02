---
author: "Coleton O'Donnell"
title: "Data Structures and Algorithms Notes"
date: "2023-01-25"
description: "Notes from my DSA study, including UF's COP3530 with Professor Kapoor, Abdul Bari's Udemy Course, and 'Introduction to Algorithms' by Cormen & Leiserson."
tags: ["math", "algorithms", "computer science"]
math: true
---

# Introduction

**Pardon the dust, this is being rewritten.**

These notes are on the COP3530 Data Structures and Algorithm class with the excellent Professor Kapoor at the University of Florida as well as on [Abdul Bari's DSA Course on Udemy](https://www.udemy.com/course/datastructurescncpp). What I have learned from each has been compounded into one living document. If you are interested in Abdul Bari's course but want a bit of a taste for it, there is also a free YouTube version that is [consolidated](https://youtube.com/playlist?list=PLDN4rrl48XKpZkf03iYFl-O29szjTrs_O). Please note that these are **notes**, I can't stress this enough. These are written with prior knowledge in mind, and are basically useless if you aren't following along with a textbook or a course. They won't be teaching you well. These can act as a good reference for concepts and important explanations. Think of it as a TL;DR on things, but you're doing yourself a disservice if you even think of using these as your main source of info. For textbooks, check out the excellent [OpenDSA Book](https://opendsa-server.cs.vt.edu/ODSA/Books/Everything/html/index.html). If you prefer paper, check out ["Introduction to Algorithms"](https://en.wikipedia.org/wiki/Introduction_to_Algorithms) by Cormen & Leiserson and ["Data Structures and Algorithm Analysis in C++"](https://www.google.com/books/edition/Data_Structures_and_Algorithm_Analysis_i/toSQvgEACAAJ?hl=en) by Weiss.

## Definition of the Data Structure and the Algorithm

* What is a Data Structure?

  * A **data structure** can be defined as the arrangement of a collection of data items so that they can be utilized efficiently. It is all about data and the operations of the data.

* What is an Algorithm?

  * An **algorithm** can be defined as a procedure used for solving a problem or performing a computation. It is a finite set of instructions to execute a task. All algorithms have an input, an output, and are definite and unambiguous. This means that they always have the same output for a given input.

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

Performance for algorithms is defined in terms of **time** and **space.** These will be discussed later. Algorithm analysis is important for a few reasons. For one, it allows us to think critically about what we are creating, and as a result allows us to find the best solution to a problem. It also allows us to sell a product, if we can boast that our product is the best because of its performance, it'll sell more. Performant algorithms also cost less to run, it might seem negligible at first, but faster algorithms save time, and time is money. In some cases, a solution to an issue with certain data sets can take 30 seconds, or a year.


# How to Measure Performance?

It is great that we know the importance of performance, but what are some ways that we can truly understand performance in a meaningful way?

## Different Approaches of Measurement

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

![How to find time complexity of an algorithm?  Adrian Mejia Blog](https://coleton.io/post-images/algo/time-complexity-examples.png)
|:--:|
| *Sourced from [Adrian Mejia](https://adrianmejia.com/how-to-find-time-complexity-of-an-algorithm-code-big-o-notation/)* |

So if we return to the example in Approach 2, we note that $T(n) = 3n + 4$. How would we express the time complexity of this algorithm utilizing order of growth? This can be done with the **Big O** notation, which represents the **upper bound** of a function's growth rate. There are other notations that describe other aspects of a function, but for the sake of algorithm performance, Big O is usually what is considered. In this way, Big O notation represents the **worst case** of an algorithm. Let's look at how these notations are formally defined and how to use them to describe the performance of an algorithm.

## Asymptotic Analysis (Time Complexity)

Asymptotic Analysis (aka. asymptotics) is a mathematical method to describe the limiting behavior of functions. For instance, imagine we are considering a function $f(x) = x^2 + 3x$, as $x \rightarrow \infin$, the term $3x$ becomes more and more insignificant when compared to the term $x^2$. In this way, it is said that $f(x)$ is *asymptotically equivalent to $x^2$* as $x \rightarrow \infin$. In Computer Science, we are especially interested in asymptotic analysis because it allows us to analyze algorithms in a meaningful and quantifiable way.

### Notation

#### Big O

Let $T(n)$, $f(n)$ be functions. Therefore, $T(n) \in O(f(n))$ if there exists two positive constants $n_0$ and $M$ such that $T(n) \le Mf(n)$ for all $n \ge n_0$. Formally speaking, this is a more restrictive definition that is of most concern to us as Computer Scientists, but if you are interested in other definitions check out [the formal definition for Big O notation here.](https://en.wikipedia.org/wiki/Big_O_notation#Formal_definition) With this definition, a function $T(n) = n$ will yield $T(n) \in O(n!)$, but although true, isn't terribly useful. As a result, when figuring out the Big O of a function, it is best to figure out the tightest upper bound, so in the previous case, $T(n) \in O(n)$. Taking a look at our example from Approach 2, $T(n) = 3n+4$. When considering this, what should the value $M$ be? The easiest way to do this is to set $M$ to equal each of the integers in the function, so $M = 3 + 4 = 7$, and we set $n_0 = 0$. So, $3n+4 \le 7n$ for all $n > 1$, so $T(n) \in O(n)$. The function $f(n)$ always acts as an upper bound on performance, and $T(n)$ will grow no faster than the constant $M$ times $f(n)$.

#### Big Ω

Let $T(n), g(n)$ be functions. Therefore, $T(n) \in \Omega(g(n))$ if there exists two positive constants $n_0$ and $M$ such that $T(n) \ge Mg(n)$ for all $n \ge n_0$. Similar to Big O, this means that when $T(n) = n^3$, $T(n) \in \Omega(1)$, but that isn't useful. So, whenever you figure out the Big Ω of a function, find the tightest lower bound, so in the previous case, $T(n) \in \Omega(n^3)$. The function $g(n)$ always acts as a lower bound on growth rate of $T(n)$, and $T(n)$ will grow no slower than the constant $M$ times $g(n)$.

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

Lines 3 and 4 is $O(n)$ and lines 6 and 7 are $O(log_2 m)$, thus the time complexity for this algorithm is $O(n + log_2 m)$. Now, if we were told that $n$ and $m$ grow at the same rate, then $O(n + log_2 m) = O(n)$. This is because we drop the lowest order term whenever variables grow at the same rate, or they are identical variables.

### Cases

Algorithms that have a purpose that allows them to stop their process (e.g.. searching algorithms, they stop once they find what they are looking for) due to a condition have different cases. These are the best case, average case, and worst case. The best case is the lowest cost, average case is the average cost for all n, and worst case is the highest possible cost.

# Recursion

## Introduction

A small topic detour for a concept that is valuable to understand in a DSA class, which is recursion. There are a lot of different types of recursive functions, and understanding how they are used is important. Let's take a look at how recursion works and how we define it.

Given the function `fun(int n)`:

```cpp
int fun(int n) {
  if (n > 1)
  {
    return fun(n-1) * 2;
  } else
  {
    return n;
  }
}
```

We can see that the function consists of an if-else statement, where if the input is greater than 1, we return the value of the function `fun(n-1)*2`, and if not, we just return n. In this way, we can simplify the function to just be:

```cpp
int fun(int n) {
  if (n > 1)
  {
    return fun(n-1) * 2;
  }
  return n;
}
```

This is an example of a recursive function. A recursive function consists of two parts, an ascending portion and a descending portion. We ascend by returning values of the function, and descend once we reach our catch value, in this case it is once $n \le 1$. The algorithm returns $2^n$.

## Tail Recursion

Tail recursion is defined as recursion in which the last statement is the recursive call, for example:

```cpp
void fun(n) {
  if (n > 0)
  {
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
  if (n > 0)
  {
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
  if (n > 0)
  {
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
  if (n > 0)
  {
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
  if (n > 0)
  {
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
  if (<-->)
  {
    // Do stuff here
    // ...
    B(n-1);
  }
}
void B(int n) {
  if (<-->)
  {
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
  if (<-->)
  {
    // Do stuff here
    fun(fun(n-1));
  }
}
```

In this way, we evaluate the parameter of the recursive call first, then whatever that is, place it into that recursive call.

## Examples of Recursion

### Fibonacci Sequence

The Fibonacci Sequence is defined as $F_n = F_{n-1} + F_{n-2}$, where $F_0 = 0$ and $F_1 = 1$. We can use Tree Recursion to write an algorithm to calculate the sum of the sequence:

```cpp
int fib(int n) {
  if (n <= 1)
  {
    return n;
  }
  return fib(n-1) + fib(n-2);
}
```

### Sum of Natural Numbers

The sum of all natural numbers at point n, is equal to the sum of the natural numbers $(n-1)$, plus $n$. In other words, `sum(n) = sum(n-1)+n`

```cpp
int sum(int n) {
  if (n == 0)
  {
    return 0;
  }
  else
  {
    return sum(n - 1) + n;
  }
}
```

# Abstract Data Types and Linear Ordered Data Structures

## What is an Abstract Data Type?

An Abstract Data Type (ADT) is a Data Type where the operation is known, but the representation is not. A real life example is a book, a book is Abstract, but a Telephone Book is a representation. We will look at all of these Logical Data Structures as ADT first, so we can understand them, and then we can delve into how they work. This means that an Abstract Data Type acts as a mathematical or logical model of a way to store and organize data. They are basically a class of objects whose logical behavior is defined by a set of values and operations. We define the data and the operations, but we don't care about the implementation. This is the opposite of a concrete data type consists of its representation and its operation. The representation is what it actually is and how it is implemented. The operation portion is what can be done with the data. In other words, the representation is the technical details of a data type, and the operation is what we can actually do with it.

An example of an ADT is a list. A concrete data type (e.g.. implementation) of list is an array, linked list, vector, etc.

## Linear Ordered Data Structures

### List ADT

Core features:

* Ordered collection of data (e.g.. all elements have an ordered positive.)
* Linear Structure.
* Can have a size, it can grow and shrink.
* Can store any element type (i.e isn't limited to a single type of data.)

The list basically is just one value after another, e.g.. 1, 2, 3, 4, etc. It is linear, meaning it goes forwards and backwards.

Characteristics:

* Data

  * Items
  * Current number of items stored
  * Capacity, is it bounded to a maximum?

* Operations

  * Read, Write, and Remove elements.
  * Find an element.
  * Count the number of elements.
  * Traverse the list.

#### Array Implementation

##### Characteristics

* They have a fixed size
* Stores similar elements (store the same or similar types)
* Contiguous indices (e.g.. $0, 1, 2...n-1$)
* Elements are stored contiguously in memory.
* Allows for random access, given an indice you can access the element there (e.g.. `Array[n]`)

##### Operation Performance

| Placement | Add    | Remove |
|:---------:|:------:|:------:|
| Beginning | $O(n)$ | $O(n)$ |
| End       | $O(1)$ | $O(1)$ |
| Middle    | $O(n)$ | $O(n)$ |

To add or remove anything from the beginning, it requires shifting $n$ elements to the right, resulting in $O(n)$. Similar is true for the middle, but instead shifting all elements to the right of the indice being considered. This is still $O(n)$ because this indice grows with $n$. In the case of the end, it is constant because the size of the array is known, and this means that it is free to add and remove from the end of it (i.e. no shifts are required.)

* Benefits
  * Constant access time, `Array[i] = arr + (i * sizeOf(type))`.
  * Constant time for adding and removing elements from the end.
* Drawbacks
  * Expensive for adding and removing elements from the beginning or middle.

#### Singly Linked List Implementation

![Singly Linked List](https://coleton.io/post-images/algo/singlylinkedlist.png)
|:--:|
| *Sourced from [VisualGo](https://visualgo.net/en/list)* |

Each of these elements are called a **Node.** A Node contains an element and a pointer to another Node. This goes on and on until the pointer points to a `nullptr` (i.e. points to nothing.) An example Node object in C++ would look like this:

```cpp
#include <iostream>

template <typename T>
class Node
{
  public:
    Node* next;
    T data;
}
```

In this instance, a `Node` contains the pointer to the next `Node` as well as the `data` of some type `T`. This can be used like this:

```cpp
Node<int>* node_one = new Node<int>();
node_one->data = 10;
node_one->next = nullptr;
```

We can also design a constructor for `Node`:

```cpp
Node::Node(T data, Node* next)
{
  this->data = data;
  this->next = next;
}

int main()
{
  Node<int>* my_list = new Node<int>(10, nullptr);
  my_list = new Node<int>(20, my_list);
  my_list = new Node<int>(30, my_list);
}
```

Thus this list is represented as:

```text
30 -> 20 -> 10 -> /
```

In this case, the length of this list is one.

The `Node` class works great, but it is a bit verbose. In actuality, the list requires a lot more features than this, we are just describing everything manually. In this case, encapsulating `Node` by another class is much better.

```cpp
template <typename T>
struct Node
{
  T data;
  Node<T> *next;
}

template<typename T>
class List
{
  private:
    int size;
    Node<T> *head;
    Node<t> *tail;

  public:
    List()
    {
      size= 0;
      head = new Node<T>;
      tail = new Node<T>;
      head->next = tail;
    }

    void push_front(T element)
    {
      Node<T> *q = new Node<T>;
      q->data = element;
      q->next = head->next;
      head->next = q;
    }
}
```

With this example, our linked list contains two nodes, the `head` and the `tail`. In this implementation, these are **sentinel** nodes, which basically represent the path entry and the path terminator. Don't worry much about them. In this example, our `push_front` operation creates a new `Node` with `element`, and then changes the Node's `next` to be whatever the `head` is pointing to next. Then we change the `head` next to be our new Node `q`. To visualize this:

```text
Before calling push_front:
H -> T

After calling push_front:
H -> q -> T
```

Where `q` is our new node.

##### Characteristics

* Consists of Nodes
  * Data
  * Pointer to a following Node
* Stores similar elements (i.e. stores all of the same type.)
* Elements are linked in memory but are stored non-contiguously.
* Doesn't allow for random access

##### Operation Performance

* Add - PushFront(key), PushBack(key)
* Remove - PopFront, PopBack
* Get - TopFront, TopBack
* Find(key), Erase(key), Empty()
* AddBefore(Node, key), AddAfter(Node, key)

Performance of these operations

| $O(1)$            | $O(n)$           | $O(n)$ extended   |
| ----------------- | ---------------- | ----------------- |
| PushFront: $O(1)$ | PushBack: $O(n)$ | AddBefore: $O(n)$ |
| PopFront: $O(1)$  | PopBack: $O(n)$  | Find: $O(n)$      |
| TopFront: $O(1)$  | TopBack: $O(n)$  | Empty: $O(n)$     |
| AddAfter: $O(1)$  | Erase: $O(n)$    |                   |

* Benefits
  * Adding and Removing in front is way faster, $O(1)$
* Drawbacks
  * Expensive random access, $O(n)$
  * TopBack, PushBack, PopBack, and AddBefore are also very expensive
  * More expensive in terms of memory

##### Improving Singly Linked List with Tail

By adding a true `tail` pointer (eg. it points to the back most element.) You can improve the PushBack and the TopBack performance to be $O(1)$. This significantly increases the usefulness of the singly linked list immensely. The issue is that PopBack and AddBefore is $O(n)$. Is there anyway to improve this? There in fact is.

#### Doubly Linked List with Tail Implementation

![doubly linked list](https://coleton.io/post-images/algo/doublylinkedlist.png)
|:--:|
| *Sourced from [AskPython](https://www.askpython.com/python/examples/doubly-linked-list)* |

In this type of linked list, a Node contains a pointer to a previous element, the current data of some type, and the following elements. This means that from any Node, you can go forwards and backwards. This means that `Node` looks something like:

```cpp
template <typename T>
struct Node
{
  Node<T> *prev;
  T data;
  Node<T> *next;
}
```

Furthermore, this solves the issue of PushBack, PopBack, TopBack, and AddBefore, all of which are now $O(1)$ time complexity instead of $O(n)$. The trade off is that this implementation requires extra memory. This is because this list implementation has access to the tail. When we have access to the tail and the have a pointer in both directions, we can view the tail, append to the tail, and AddBefore the tail (as well as any Node.) Let's take a look at how some of this logic looks. Whenever we want to remove a value before the tail in this given doubly linked list:

```text
H -> 2 -> 3 -> T
  <-   <-   <-
```

Let's say we want to remove 3, in this case we'd access the tail value. We'd set `tail->prev->prev->next = tail`, and then set `tail->prev = tail->prev->prev`. We would also throw in a delete somewhere to make sure we are deleting the old node:

```text
H -> 2 -> T
  <-   <-
```

#### Circular Linked List

I won't go into these as they aren't exactly needed to be known in this class, but basic things should be understood. Just check out [this GeeksForGeeks article on Circular Singly Linked Lists](https://www.geeksforgeeks.org/circular-linked-list/) as well as [this one on Circular Doubly Linked List](https://www.geeksforgeeks.org/insertion-in-doubly-circular-linked-list/).

#### Array vs. Linked List

In terms of Space, there are two things, List size and Element size.
* List Size, in Linked List favor
  * In the array implementation, an estimate of the size when the list is created is required, and when this size is met, the array must be reallocated.
  * In the linked list implementation, the size is dynamic and can grow as needed.
* Element Size, in Array favor
  * In the array implementation, only the element is needed to be stored.
  * In the linked list implementation, it requires storage for the element as well as pointer(s).

In terms of Time, there are two things, access as well as adding and removing.
* Access, in Array favor
  * In the array implementation, values can be randomly accessed in constant time at any index.
  * In the linked list implementation, values must be accessed by traversing the list one element at a time.

* Adding and Removing, in Linked List favor
  * In the array implementation, it requires all elements to be moved whenever we add or remove from the array.
  * In the linked list implementation, insertion and removal is constant time if the iterator is where you need it to be.

#### STL Lists

The C++ Standard Template Library contains 4 major list implementations. The `Forward_list` which is Singly Linked List implementation. The `List` which is a doubly linked list implementation. The `Array` which is a fixed size list. Finally, `Vector`, which is a dynamic size list implementations. C++ offers all of these different List ADT implementation because they all have their pros and cons that are either the best option for an issue or the worst solution.

##### Iterators
```cpp
list<int> my_list(4, 100); // [100, 100, 100, 100]
my_list.push_front(200); // [200, 100, 100, 100, 100]
for (auto it = my_list.begin(); it != my_list.end(); ++it)
  cout << ' ' << *it; // Outputs: 200 100 100 100 100 
```

##### Merge Two Lists

Given two sorted lists, we can merge them together sorted:

```cpp
// listA and listB are two sorted lists
std::list<int> mergeLists(std::list<int> listA, std::list<int> listB)
{
  auto iterA = listA.begin();
  auto iterB = listB.begin();
  std::list<int> mergedList;
  int itemA = *iterA;
  int itemB = *iterB;

  while(iterA != listA.end() && iterB != listB.end())
  {
    if (itemA < itemB)
    {
      mergedList.push_back(itemA);
      iterA++;
      itemA = *iterA;
    }
    else
    {
      mergedList.push_back(itemB);
      iterB++;
      itemB = *iterB;
    }
  }

  // Only one of these run at max, which handles
  // if one list is larger than the other
  while (iterA != listA.end())
    mergedList.push_back(*iterA++);
  
  while (iterB != listB.end())
    mergedList.push_back(*iterB++);

  return mergedList;
}
```

### Stack ADT
A stack is a Last In First Out Structure, or LIFO. In other words, the last element in (most recent element placed in) is the first to come out. Think of it like a stack of plates.

Characteristics:

* Data
  * Items
  * Current number of items stored.
  * Top pointer (points to the top most element.)
* Operations
  * `push` - Inserts an element on the stack (from the top)
  * `pop` - Removes the element on the top of the stack
  * `peek` - Returns the element on the top of the stack
  * `size` - Returns the number of elements on the stack
  * `isEmpty` - Returns true if the stack is empty, false otherwise

#### Array Implementation

We can exploit the characteristics of an array to build a very good stack implementation. Note the following class:
```cpp
class StackArray
{
  private:
    const static int SIZE = 1024;
    int arr[SIZE];
    int top = -1;
  
  public:
    void push(int n)
    {
      arr[++top] = n;
    }

    int pop()
    {
      if (top != -1)
        return arr[top--];
      return -1;
    }

    int peek()
    {
      if (top != -1)
        return arr[top];
      return -1;
    }

    int size()
    {
      return top + 1;
    }

    bool isEmpty()
    {
      if (top == -1)
        return true;
      return false;
    }
};
```

##### Operation Performance

We utilize an array to store the values, and an integer to track the current position on the stack. Operations complexity is as follows:

| Operation   | Complexity |
|:-----------:|:----------:|
| `push()`    | $O(1)$     |
| `pop()`     | $O(1)$     |
| `peek()`    | $O(1)$     |
| `size()`    | $O(1)$     |
| `isEmpty()` | $O(1)$     |

As we can see, this implementation is very efficient. All the operations are constant time. The issue is that this implementation is of a fixed size at compile time. In the implementation above, the `SIZE` variable is a constant, and is set to $1024$. Of course, we can always raise this but this means that at compile time the stack size can't be increased or decreased in this implementation.

#### Linked List Implementation

The issue with the last implementation was that it didn't have a dynamic size. We can address this issue by using a linked list:

```cpp
class ListArray
{
  private:
    struct Node
    {
      int element;
      Node* next;
      Node(int n) { element = n; }
    };
    Node* top = nullptr;
    int count = 0;
  
  public:
    void push(int n)
    {
      Node* new_top = new Node(n);
      new_top->next = top;
      top = new_top;
      count++;
    }

    int pop()
    {
      if (top)
      {
        count--;
        int n = top->element;
        Node* temp = top;
        top = top->next;
        delete temp;
        return n;
      }
      return -1;
    }

    int peek()
    {
      if (top)
        return top->element;
      return -1;
    }

    int size()
    {
      return count;
    }

    bool isEmpty()
    {
      if (top)
        return false;
      return true;
    }
};
```

##### Operation Performance

Just like the array implementation, all of the operations are $O(1)$:

| Operation   | Complexity |
|:-----------:|:----------:|
| `push()`    | $O(1)$     |
| `pop()`     | $O(1)$     |
| `peek()`    | $O(1)$     |
| `size()`    | $O(1)$     |
| `isEmpty()` | $O(1)$     |

So what is the difference? Well we have a dynamically changing stack, instead of it being limited to a specific size, it can grow and shrink to our needs. The drawback is that this requires more memory to implement.

#### Stack STL

The STL `stack` offers the following methods, `push(g)`, `pop()`, `top()`, `size()`, and `empty()`, which follows the methods we have already outlined but with slightly different names. To create use the `stack` STL, we follow this form:

```cpp
#include <stack>

stack<type> my_stack; // create a stack with a type of "type"
```

Let's see what we can do with the stack:

##### Use Cases for Stack

###### Check if a String is a Palindrome
```cpp
#include <stack>
#include <string>

bool checkPalindrome(std::string s)
{
  std::stack<char> stk;

  if (s.length() < 2)
    return true;

  int midIndex = s.length() / 2;

  for (int i = 0; i < s.length() / 2; i++) // push first
    stk.push(s.at(i));                     // half of string

  if (s.length() % 2 != 0)                 // ignore middle
    midIndex += 1;                         // element if odd

  for (int i = midIndex; i < s.length(); i++)
  {                                        // iterate from middle
    if (stk.top() != s.at(i))              // check each half
      return false;                        // these don't match
    stk.pop();                             // move to next element
  }

  return true;
}
```

###### Parenthesis Matching

```cpp
#include <stack>
#include <string>

bool isClosed(std::string expression) {
  std::stack<bool> stk;

  for (char i: expression)
  {
    if (i == '(')      // push onto stack every time
      stk.push(true);  // an opening parenthesis is found
    else if (i == ')')
    {
      if (stk.empty()) // this means this is an orphaned 
        return false;  // closed parenthesis, immediately false
      else
        stk.pop();     // we found a parenthesis pair
    }
  }

  if (!stk.empty())    // orphaned opening parenthesis
    return false;

  return true;
}
```

### Queue ADT

Queues, unlike Stacks, are FIFO structures (First In First Out.) This means that the first element in is the first out. Queues operate in the same way as say a line works. 

Characteristics:

* Data
  * Items
  * Current number of items stored.
  * Front and back pointers.
* Operations
  * `enqueue` - Insert an element to the back of the queue.
  * `dequeue` - Remove an element from the front of the queue.
  * `size` - Return the number of elements stored.
  * `isEmpty` - Indicates whether or not elements are currently being stored.


#### Circular Array Implementation

Though it is possible to implement the queue with just a normal array, an issue arises which is known as the **rightward drift problem.** You can look into that on your own, but it makes a normal array implementation impossible. A normal array implementation would look something like this:

```cpp
class BadArrayQueue
{
  private:
    const static int SIZE = 1024;
    int arr[SIZE];
    int front = 0, back = 0;
  public:
    // ...
}
```

The solution is to use a circular array instead. A circular array uses the modulus operator to basically "overflow" into a loop so that as elements are queued and dequeued, they don't ruin the array.

```cpp
#include <iostream>

class CircularQueue
{
  private:
    int size;
    int stored = 0;
    int front;
    int rear;
    int* elements;

  public:
    CircularQueue(int size)
    {
      this->size = size;
      front = -1;
      rear = -1;
      elements = new int[size];
    }

    ~CircularQueue()
    {
      delete [] elements;
    }

    bool isEmpty()
    {
      if (front == rear)
      {
        return true;
      }
      return false;
    }

    bool isFull()
    {
      if ((rear + 1) % size == front)
      {
        return true;
      }
      return false;
    }

    int size()
    {
      return stored;
    }

    void enqueue(int x)
    {
      if (isFull())
      {
        std::cout << "Queue Overflow" << std::endl;
      } else {
        stored++;
        rear = (rear + 1) % size;
        elements[rear] = x;
      }
    }

    int dequeue()
    {
      int x = -1;
      if (isEmpty())
      {
        std::cout << "Queue Underflow" << std::endl;
      } else {
        stored--;
        front = (front + 1) % size;
        x = elements[front];
      }
      return x;
    }
};
```

##### Operation Performance

This better implementation of an array queue results in the following time complexity:

| Operation | Complexity |
|:---------:|:----------:|
| `enqueue` | $O(1)$     |
| `dequeue` | $O(1)$     |
| `size`    | $O(1)$     |
| `isEmpty` | $O(1)$     |

The benefit of this queue is that it takes up less space. The downside is that it has a fixed size.

#### Linked List Implementation

Instead of using a circular array, we can instead use a linked list. 

```cpp
class ListQueue
{
  private:
    struct Node
    {
      int data;
      Node* next;
      Node(int n)
      {
        data = n;
        next = nullptr;
      }
    };

    Node* front = nullptr;
    Node* back = nullptr;
    int count = 0;
  
  public:
    bool isEmpty()
    {
      if (front == nullptr && back == nullptr)
        return true;
      return false;
    }

    int size()
    {
      return count;
    }

    void enqueue(int n)
    {
      count++;
      auto temp = new Node(n);
      if (front == nullptr)
      {
        front = temp;
        back = temp;
      }
      back->next = temp;
      back = temp;
    }

    int dequeue()
    {
      if (count == 0)
      {
        std::cout << "Queue is empty" << std::endl;
        return -1;
      }
      int temp = front->data;
      count--;
      if (front == back)
      {
        delete back;
        front = nullptr;
        back = nullptr;
        return temp;
      }
      Node* old_front = front;
      front = front->next;
      delete old_front;
      return temp;
    }
};
```

##### Operation Performance

This implementation similarly has the same time complexity:

| Operation | Complexity |
|:---------:|:----------:|
| `enqueue` | $O(1)$     |
| `dequeue` | $O(1)$     |
| `size`    | $O(1)$     |
| `isEmpty` | $O(1)$     |

The benefits is that this implementation avoids the static size issue of the circular queue, but that also means it requires more memory.

# Non-Linear Ordered Data Structures

## Trees

### Introduction to Tree-Based Data Structures

A tree is a rooted, directed, and acyclic in nature. In other words, it has a single root, each node has a single parent, and there are no cycles. 

![](https://coleton.io/post-images/algo/tree1.png)
|:--:|
| Tree 1 |

*Tree 1* is an example of a basic valid tree. The **root** of this tree is A, and each node has a single **parent**. B's parent is A, and C's parent is also A. In this way, B and C are referred to as **siblings**. The parent are the predecessor of a node, while children are the successor of a node. Tree's aren't necessarily limited to just two children though. For instance, look at the following tree:

![](https://coleton.io/post-images/algo/tree2.png)
|:--:|
| Tree 2 |

In the case of *Tree 2*, there is a single root, A, and A has three children B, C, and D. Every node has either a single parent or no parent.

![](https://coleton.io/post-images/algo/tree3.png)
|:--:|
| Tree 3 |

Dissecting *Tree 3*:
* E is the **grandparent** of A. 
* E's **ancestors** are B and A. B's ancestors is A only. 
* A's **descendants** is every node underneath it, so B, C, D, and E. B's descendants are E. C, D, and E have no descendants (nor children.) 
* C, D, and E are **leaf nodes** or **external nodes.** These are nodes that have no children. 
* B and A are **non-leaf nodes** or **internal nodes** because they possess children. 
* A possesses three **subtrees.** A subtree of a node is a tree whose root is a child of that node. So the three subtrees of A are B and E, C, and D. B possess one subtree, E. E, C, and D possess zero subtree.
* The **level** or **depth** of this tree is 2. The level of a node is the distance of that node from the root. The root, A, is on level zero. B, C, and D are on level one. E is on level two. To compute the level of a tree, where $n$ is a node:

  * $\text{if } n \text{ is root:}$
    * $\text{level}(n) = 0$
  * $\text{else:}$
    * $\text{level}(n) = \text{level(parent)} + 1$

* The **height** of a tree is the number of nodes in the longest path from the root node to a leaf node. In this case, the height of this tree is 3, as the longest path contains 3 nodes, A, B, and E. To compute the height of a tree:

  * $\text{if the tree has just a root}$
    * $\text{Height = 1}$
  * $\text{else:}$
    * $\text{Height} = \text{max(Height(children))} + 1$

There are quite a few use cases for trees, such as Family Tress, Decision/Logic Trees, File Systems, Expression Trees, and Searching Trees.

### N-Ary Trees

![](https://coleton.io/post-images/algo/tree4.png)
|:--:|
| Tree 4 |

* A tree with each node consisting of at maximum $n$ children.
* The tree has three properties:
  1. Single root.
  2. Each node has a single parent.
  3. No cycles.

In this example above, we see that the root A has $1..n$ children. So if $n = 3$, each node can have at max 3 children. 

### Binary Trees

![](https://coleton.io/post-images/algo/tree5.png)
|:--:|
| Tree 5 |

A binary tree is a tree with each node consisting of at most 2 children. In the above tree, *Tree 5*, notice that every node branches to at max 2 children. The root node, 30, as well as 4, branch off to two children, 40 branches to one element. 2, 5, and 53 branch off to zero children. 

#### Full Binary Tree

![](https://coleton.io/post-images/algo/tree6.png)
|:--:|
| Tree 6 |

*Tree 6* here is a **full** binary tree. That means that every node has either 2 children or 0 children.

#### Perfect Binary Tree
![](https://coleton.io/post-images/algo/tree7.png)
|:--:|
| Tree 7 |

*Tree 7* is a **perfect** binary tree. That means that given a height $h$ of the tree, the number of nodes contained is exactly $2^h - 1$. The height, $h$, of *Tree 6* and *Tree 7* is 3. The number of nodes contained in *Tree 6* is 5. The number of nodes contained in *Tree 7* is 7. Thus, for *Tree 6*:

$$2^h - 1 = 2^3 - 1 = 7 \ne 5$$

By this formula, a perfect binary tree node count for this height would be 7, but in the case of *Tree 6*, the count is 5 which means it is not a perfect binary tree. Looking at *Tree 7*:

$$2^h - 1 = 2^3 - 1 = 7 \equiv 7$$

Because our node count for *Tree 7* is 7, it is a perfect binary tree.

It should be noted that if a tree is perfect, it's height is $O(\log n)$, where $n$ is the number of nodes.

#### Complete Binary Tree

A **complete** binary tree is a tree which is perfect through levels $n - 1$, with some extra leaf nodes at level $n$ (height of the tree), all towards the left. In other words, for a tree, at level $n$ there should be nodes filling from the left to the right, but it doesn't need to fill all the way towards the right. To illustrate, *Tree 5* isn't a complete binary tree. This is because it goes from left to right on the bottom most level, 2, 4, and 53. To make it complete, 40 must have a left child. *Tree 6* is in fact a complete binary tree. This is because from left to right, it goes 2 and 4. 40 might not have any children, but there aren't any gaps between the siblings of the bottom level, thus making it complete. This means that *Tree 6* is both complete and full. A perfect binary tree like *Tree 7* is also complete and full. Every perfect binary tree is complete and full, but not every complete and full binary tree is a perfect binary tree.

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

This matrix will be the framework for later types of matrixes:

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

When observing the space this matrix takes up, we can observe that each n row adds n amount of space, e.g.. 1 + 2 + 3, etc. etc. This means the number of non zero elements are give in $\frac{n(n+1)}{2}$, and the number of zero elements is given by $\frac{n(n-1)}{2}$.

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

When observing the space this matrix takes up, we can observe that each n row adds n amount of space, e.g.. 1 + 2 + 3, etc. etc. This means the number of non zero elements are give in $\frac{n(n+1)}{2}$, and the number of zero elements is given by $\frac{n(n-1)}{2}$.

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

Stable sorting algorithms preserve the relative order of equal elements. For example, imagine I have a list of student names with corresponding grades. Currently, the list is sorted alphabetically, but imagine I want to sort numerically. A stable sorting algorithm would not change the relative order of duplicates, thus a student with a first name A with a score of say 80 would be ahead of a student with a first name B with a score of 80. The use of a stable algorithm is that it makes it more efficient when there are duplicate cases, as we don't have to sort by another key when a duplicate is present.

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

It can be assumed that this swap method will be included with every implementation from here onwards (when required):

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

Each step in an insertion sort requires breaking the array into separate parts. First step is breaking off the 0 index, which is sorted by definition as it is only one element. Second step is adding an extra spot, and doing an insertion:

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

We continue this process until the very end.

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

i = 2, scan for smallest value

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

To begin, set the first element as the pivot element. The idea behind quicksort is that we determine a place that is sorted, so each value left of the pivot is less than or equal to the pivot, and everything to the right of the pivot is greater than or equal to the pivot. So, `i` looks for everything greater than to the pivot, and `j` looks for everything less than or equal to the pivot. So i starts at 0, and j starts at length of array:

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

Given two sorted arrays, we are going to increment over each and merge, e.g.:

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

  // Only one of the following return
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

First, find the largest value in your array. Create an array where the last index is equal to that value, e.g.. a max value of 15 would be an array size 16. Initialize the array with zeros. This is important for what we are about to do. So with the given array, create another array with this directions:

```
A | 6   3   9   10  15  6   8   12  3   6
    0   1   2   3   4   5   6   7   8   9

15 is max value:
C | 0   0   0   0   0   0   0   0   0   0   0   0   0   0   0   0
    0   1   2   3   4   5   6   7   8   9   10  11  12  13  14  15
```

Next, scan the array and increment with each value, e.g:

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

Radix sort also works on the bin principle, but instead of taking max value as the size, it uses the base. So for the decimal system, base 10, we have 10 bins, 0-9. So for value say, 278, it goes in bin 8. Well that is cool, but the issue is that this isn't sorted, well, drop everything and then extract. Set bins to null again, and then sort by second space, e.g.. 257 goes in the 5 bin. Do this again for each space, and you'll get a sorted array:

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

The grand finale, quite honestly this sort is definitely the weirdest, and probably the most complex. Basic principle is insert sort modified, where we form arrays based on gaps, e.g.

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

Remember, the modulus hash function is $h(x) = x \bmod 10$, but we also are running into the problem of conflicts. An intuitive idea is to use a linked list for conflicts, so we create an array of nodes, and each node contains a linked list of the elements. So for the 5, we can shovel any value that ends with 5, and if we wanted to search for 25, we can just search the linked list belonging to the 5th element. So, what is the time complexity? Well, first we have to determine what is called the loading factor. The loading factor $\lambda = \frac{n}{\text{size}}$. The size of the hashtable is 10, so for example if we have 100 keys, then our loading factor $\lambda$ is equal to 10. The average successful search time complexity is $t = 1 + \frac{\lambda}{2}$. The average unsuccessful search time complexity is $t = 1 + \lambda$.

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
