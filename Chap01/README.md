# Chapter 1. Getting Started

## Exercise 1.1

> Review the documentation for your compiler and determine what file naming convention it uses. Compile and run the `main` program from page 2.

[GCC Coding Conventions](https://gcc.gnu.org/codingconventions.html)

## Exercise 1.2

> Change the program to return `-1`. A return value of `-1` is often treated as an indicator that the program failed. Recompile and rerun your program to see how your system treats a failure indicator from `main`.

- `main.cpp`

```cpp
int main() {
  return -1;
}
```

```bash
$ g++ -o main main.cpp
$ ./main
$ echo $?
255 # exit takes only integer args in the range 0 - 255
```

## Exercise 1.3

> Write a program to print `Hello, World` on the standard output.

```cpp
#include <iostream>

int main() {
  std::cout << "Hello, World" << std::endl;
}
```

## Exercise 1.4

> Our program used the addition operator, `+`, to add two numbers. Write a program that uses the multiplication operator, `*`, to print the product instead.

```cpp
#include <iostream>

int main() {
  std::cout << "Enter two numbers:" << std::endl;
  int v1 = 0, v2 = 0;
  std::cin >> v1 >> v2;
  std::cout << "The product of " << v1 << " and " << v2 << " is " << v1 * v2
            << std::endl;
  return 0;
}
```

## Exercise 1.5

> We wrote the output in one large statement. Rewrite the program to use a separate statement to print each operand.

```cpp
#include <iostream>

int main() {
  std::cout << "Enter two numbers:";
  std::cout << std::endl;
  int v1 = 0, v2 = 0;
  std::cin >> v1 >> v2;
  std::cout << "The product of ";
  std::cout << v1;
  std::cout << " and ";
  std::cout << v2;
  std::cout << " is ";
  std::cout << v1 * v2;
  std::cout << std::endl;
  return 0;
}
```

## Exercise 1.6

> Explain whether the following program fragment is legal.
>
> ```cpp
> std::cout << "The sum of " << v1;
>           << " and " << v2;
>           << " is " << v1 + v2 << std::endl;
> ```
>
> If the program is legal, what does it do? If the program is not legal, why not? How would you fix it?

It's illegal.

```
error: expected expression
  << " and " << v2 << " is " << v1 * v2 << std::endl;
  ^
1 error generated.
```

Removing semicolons after v1 and v2 solves the problem.

## Exercise 1.7

> Compile a program that has incorrectly nested comments.

```cpp
/*
 * comment pairs /*   */ cannot nest.
 * ''cannot nest'' is considered source code,
 * as is the rest of the program
 */
int main() {
  return 0;
}
```

```
main.cpp:2:19: warning: '/*' within block comment [-Wcomment]
 * comment pairs /*   */ cannot nest.
                 ^
main.cpp:2:30: error: unknown type name 'cannot'
 * comment pairs /*   */ cannot nest.
                         ^
main.cpp:2:41: error: expected ';' after top level declarator
 * comment pairs /*   */ cannot nest.
                                    ^
                                    ;
main.cpp:3:4: warning: empty character constant [-Winvalid-pp-token]
 * ''cannot nest'' is considered source code,
   ^
main.cpp:3:17: warning: empty character constant [-Winvalid-pp-token]
 * ''cannot nest'' is considered source code,
                ^
3 warnings and 2 errors generated.
```

## Exercise 1.8

> Indicate which, if any, of the following output statements are legal:
>
> ```
> std::cout << "/*";
> std::cout << "*/";
> std::cout << /* "*/" */;
> std::cout << /*  "*/" /* "/*"  */;
> ```
>
> After you've predicted what will happen, test your answers by compiling a program with each of these statements. Correct any errors you encounter."

```
main.cpp:6:22: warning: missing terminating '"' character [-Winvalid-pp-token]
  std::cout << /* "*/" */;
                     ^
main.cpp:6:22: error: expected expression
1 warning and 1 error generated.
```

Corrected:

```cpp
std::cout << /* "*/" */";
```

Output:

```
/**/ */ /* %
```

## Exercise 1.9

> Write a program that uses a `while` to sum the numbers from 50 to 100.

```cpp
#include <iostream>

int main() {
  int sum = 0, val = 50;
  while (val < 101) {
    sum += val;
    ++val;
  }
  std::cout << "Sum of 50 to 100 inclusive is " << sum << std::endl;
  return 0;
}
```

## Exercise 1.10

> In addition to the `++` operator that adds `1` to its operand, there is a decrement operator (`--`) that subtracts `1`. Use the decrement operator to write a `while` that prints the numbers from ten down to zero.

```cpp
#include <iostream>

int main() {
  int i = 10;
  while (i >= 0) {
    std::cout << i << " ";
    --i;
  }
  return 0;
}
```

## Exercise 1.11

> Write a program that prompts the user for two integers. Print each number in the range specified by those two integers.

```cpp
#include <iostream>

int main() {
  int l = 0, r = 0;
  std::cout << "Please input two integers: ";
  std::cin >> l >> r;
  int val = l;
  while (val <= r) {
    std::cout << val << " ";
    ++val;
  }
  return 0;
}
```

## Exercise 1.12

> What does the following `for` loop do? What is the final value of `sum`?
>
> ```cpp
> int sum = 0;
> for (int i = -100; i <= 100; ++i)
>   sum += i;
> ```

The loop sums -100 to 100 inclusively.

## Exercise 1.13

> Rewrite the first two exercises from § 1.4.1 (p. 13) using `for` loops.

[Exercise 1.9](#exercise-19)

```cpp
#include <iostream>

int main() {
  int sum = 0;
  for (int i = 50; i < 101; ++i)
    sum += i;
  std::cout << "Sum of 50 to 100 inclusive is " << sum << std::endl;
  return 0;
}
```

[Exercise 1.10](#exercise-110)

```cpp
#include <iostream>

int main() {
  for (int i = 10; i >= 0; --i)
    std::cout << i << " ";
  return 0;
}
```

## Exercise 1.14

> Compare and contrast the loops that used a `for` with those using a `while`. Are there advantages or disadvantages to using either form?

It depends. With proper use, `for` might have a better readability than `while`. While `while` always evaluate the condition first, and sometimes we like this.

Eventually, `for` does the same thing with `while` with structured code.

We can always do

```cpp
for (; condition;) {
  // statements
}
```

to mock

```cpp
while (condition) {
  // statements
}
```

## Exercise 1.15

> Write programs that contain the common errors discussed in the box on page 16. Familiarize yourself with the messages the compiler generates.”

Copy the code in the book and compile it.

## Exercise 1.16

> Write your own version of a program that prints the sum of a set of integers read from `cin`.

```cpp
#include <iostream>

int main() {
  int sum = 0;
  for (int i; std::cin >> i; sum += i)
    ;
  std::cout << sum << std::endl;
}
```

## Exercise 1.17

> What happens in the program presented in this section if the input values are all equal? What if there are no duplicated values?

- All equal: print a single line with the count of input value.
- No duplicated values: print a new line for each new input value when you enter end-of-file (control-d in UNIX systems and control-z in Windows).

## Exercise 1.18

> Compile and run the program from this section giving it only equal values as input. Run it again giving it values in which no number is repeated.

Compile and run the following program.

```cpp
#include <iostream>

int main() {
  // currVal is the number we're counting; we'll read new values into val
  int currVal = 0, val = 0;
  // read first number and ensure that we have data to process
  if (std::cin >> currVal) {
    int cnt = 1;
    // store the count for the current value we're processing
    while (std::cin >> val) {  // read the remaining numbers
      if (val == currVal)      // if the values are the same
        ++cnt;
      // add 1 to cnt
      else {  // otherwise, print the count for the previous value
        std::cout << currVal << " occurs " << cnt << " times" << std::endl;
        currVal = val;
        // remember the new value
        cnt = 1;
        // reset the counter
      }
    }
    // while loop ends here
    // remember to print the count for the last value in the file
    std::cout << currVal << " occurs " << cnt << " times" << std::endl;
  }  // outermost if statement ends here
  return 0;
}
```

## Exercise 1.19

> Revise the program you wrote for the exercises in § 1.4.1 (p. 13) that printed a range of numbers so that it handles input in which the first number is smaller than the second.

```cpp
#include <iostream>

int main() {
  int small = 0, big = 0;
  std::cout << "Please input two integers: ";
  std::cin >> small >> big;
  if (small > big) {
    int temp = small;
    small = big;
    big = temp;
  }
  int val = small;
  while (val <= big) {
    std::cout << val << " ";
    ++val;
  }
  return 0;
}
```

## Exercise 1.20

> http://www.informit.com/title/0321714113 contains a copy of `Sales_item.h` in the Chapter 1 code directory. Copy that file to your working directory. Use it to write a program that reads a set of book sales transactions, writing each transaction to the standard output.

```cpp
#include <iostream>

#include "Sales_item.h"

int main() {
  Sales_item item;
  while (std::cin >> item)
    std::cout << item << std::endl;
  return 0;
}
```

To compile: `g++ main.cpp -std=c++11`.

## Exercise 1.21

> Write a program that reads two `Sales_item` objects that have the same ISBN and produces their sum.

```cpp
#include <iostream>

#include "Sales_item.h"

int main() {
  Sales_item item1, item2;
  while (std::cin >> item1 >> item2) {
    if (item1.isbn() == item2.isbn()) {
      std::cout << item1 + item2;
    }
  }
  return 0;
}
```

## Exercise 1.22

> Write a program that reads several transactions for the same ISBN. Write the sum of all the transactions that were read.

```cpp
#include <iostream>

#include "Sales_item.h"

int main() {
  Sales_item sum, item;
  if (std::cin >> sum) {
    while (std::cin >> item) {
      if (sum.isbn() == item.isbn()) {
        sum += item;
      }
    }
    std::cout << sum << std::endl;
  }
  return 0;
}
```

## Exercise 1.23

> Write a program that reads several transactions and counts how many transactions occur for each ISBN.

```cpp
#include <iostream>

#include "Sales_item.h"

int main() {
  Sales_item item;
  // read the first item
  std::cin >> item;
  std::string isbn = item.isbn();
  int count = 1;
  while (std::cin >> item) {
    if (item.isbn() == isbn) {
      ++count;
    } else {
      std::cout << "ISBN " << isbn << ": " << count << std::endl;
      isbn = item.isbn();
      count = 1;
    }
  }
  std::cout << "ISBN " << isbn << ": " << count << std::endl;
  return 0;
}
```

## Exercise 1.24

> Test the previous program by giving multiple transactions representing multiple ISBNs. The records for each ISBN should be grouped together.

- `test_input`

```
23 1 15.0
23 2 10.0
23 3 5.0
20 2 10.0
20 2 30.0
```

```bash
$ g++ -o main main.cpp
$ ./main <test_input
ISBN 23: 3
ISBN 20: 2
```

## Exercise 1.25

> Using the `Sales_item.h` header from the Web site, compile and execute the bookstore program presented in this section.
