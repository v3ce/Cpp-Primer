# Chapter 2. The Basics

## Exercise 2.1

> What are the differences between `int`, `long`, `long long`, and `short`? Between an unsigned and a signed type? Between a `float` and a `double`?

1. `int`, `long`, `long long`, `short`

| Type        | Minimum Size | Minimum Number Range  |
| ----------- | ------------ | --------------------- |
| `int`       | 16 bits      | [-2^{15}, 2^{15} - 1] |
| `long`      | 32 bits      | [-2^{31}, 2^{31} - 1] |
| `long long` | 64 bits      | [-2^{63}, 2^{63} - 1] |
| `short`     | 16 bits      | [-2^{15}, 2^{15} - 1] |

2.  unsigned and signed

- A signed type represents natural numbers.
- A unsigned type represents number >= 0.

3. `float` and `double`

| Type     | Minimum Size          |
| -------- | --------------------- |
| `float`  | 7 significant digits  |
| `double` | 16 significant digits |

## Exercise 2.2

> To calculate a mortgage payment, what types would you use for the rate, principal, and payment? Explain why you selected each type.

- rate (`double`): a floating number with 4 significant digits.
- principal (`double`): a positive integer less than 1 trillion (depends on how rich you are.)
- payment (`double`): a positive integer less than 1 trillion (depends on how rich you are.)

## Exercise 2.3

> What output will the following code produce?
>
> ```cpp
> unsigned u = 10, u2 = 42;
> std::cout << u2 - u << std::endl;
> std::cout << u - u2 << std::endl;
>
> int i = 10, i2 = 42;
> std::cout << i2 - i << std::endl;
> std::cout << i - i2 << std::endl;
>
> std::cout << i - u << std::endl;
> std::cout << u - i << std::endl;
> ```

```
32
4294967264
31
032
0
0
```

## Exercise 2.4

> Write a program to check whether your predictions were correct. If not, study this section until you understand what the problem is.

```cpp
#include <iostream>

int main() {
  unsigned u = 10, u2 = 42;
  std::cout << u2 - u << std::endl;
  std::cout << u - u2 << std::endl;

  int i = 11, i2 = 42;
  std::cout << i2 - i << std::endl;
  std::cout << i - i2 << std::endl;

  std::cout << i - u << std::endl;
  std::cout << u - i << std::endl;
}
```

## Exercise 2.5

> Determine the type of each of the following literals. Explain the differences among the literals in each of the four examples:
>
> (a) `'a'`, `L'a'`, `"a"`, `L"a"`
>
> (b) `10`, `10u`, `10L`, `10uL`, `012`, `0xC`
>
> (c) `3.14`, `3.14f`, `3.14L`
>
> (d) `10`, `10u`, `10.`, `10e-2`

(a)

| Literal | Meaning               | Type             |
| ------- | --------------------- | ---------------- |
| `'a'`   | character             | `char`           |
| `L'a'`  | wide character        | `wchar_t`        |
| `"a"`   | string                | `const char*`    |
| `L"a"`  | wide character string | `const wchar_t*` |

(b)

| Literal | Meaning                         | Type            |
| ------- | ------------------------------- | --------------- |
| `10`    | integer (decimal)               | `int`           |
| `10u`   | unsigned integer (decimal)      | `unsigned`      |
| `10L`   | long integer (decimal)          | `long`          |
| `10uL`  | unsigned long integer (decimal) | `unsigned long` |
| `012`   | integer (octal)                 | `int`           |
| `0xC`   | integer (hexadecimal)           | `int`           |

(c)

| Literal | Meaning        | Type          |
| ------- | -------------- | ------------- |
| `3.14`  | floating-point | `double`      |
| `3.14f` | floating-point | `float`       |
| `3.14L` | floating-point | `long double` |

(d)

| Literal | Meaning                    | Type       |
| ------- | -------------------------- | ---------- |
| `10`    | integer (decimal)          | `int`      |
| `10u`   | unsigned integer (decimal) | `unsigned` |
| `10.`   | floating-point             | `double`   |
| `10e-2` | floating-point             | `double`   |

## Exercise 2.6

> What, if any, are the differences between the following definitions:
>
> ```cpp
> int month = 9, day = 7;
> int month = 09, day = 07;
> ```

The first definitions are decimals.

For the second definitions:

- `int month = 09` is invalid because octal doesn't have digit `9`.
- `day` is octal.

## Exercise 2.7

> What values do these literals represent? What type does each have?
>
> (a) `"Who goes with F\145rgus?\012"`
>
> (b) `3.14e1L`
>
> (c) `1024f`
>
> (d) `3.14L`

(a) "Who goes with Fergus?\012": `const char*`

(b) 31.4: `long double`

(c) error: invalid digit `'f'` in decimal constant

(d) 3.14: `long double`

## Exercise 2.8

> Using escape sequences, write a program to print 2M followed by a newline. Modify the program to print 2, then a tab, then an M, followed by a newline.

Use `\` followed by one, two, or three octal digits to illustrate the idea:

```cpp
#include <iostream>

int main() {
  std::cout << "\62\115\n" << std::endl;
  std::cout << "\62\t\115\n" << std::endl;
}
```

## Exercise 2.9

> Explain the following definitions. For those that are illegal, explain what's wrong and how to correct it.
>
> (a) `std::cin >> int input_value;`
>
> (b) `int i = { 3.14 };`
>
> (c) `double salary = wage = 9999.99;`
>
> (d) `int i = 3.14;`

(a) error: expected `'('` for function-style cast or type construction

```cpp
int input_value = 0;
std::cin >> input_value;
```

(b) error: type `'double'` cannot be narrowed to `'int'` in initializer list [-Wc++11-narrowing]

```cpp
double i = {3.14};
```

(c) error: use of undeclared identifier `'wage'`

```cpp
double wage;
double salary = wage = 9999.99;
```

(d) ok: but value will be truncated.

## Exercise 2.10

> What are the initial values, if any, of each of the following variables?
>
> ```cpp
> std::string global_str;
> int global_int;
> int main() {
>   int local_int;
>   std::string local_str;
> }
> ```

`global_str` and `local_str` are implicitly initialized to the empty string since it's defined by `string` class.
`global_int` is a built-in type variable outside any function body, so its value is initialized to zero.
`local_int` is a built-in type variable defined inside a function, so its value is uninitialized.

## Exercise 2.11

> Explain whether each of the following is a declaration or a definition:
>
> (a) `extern int ix = 1024;`
>
> (b) `int iy;`
>
> (c) `extern int iz;`

(a) definition

(b) definition

(b) declaration

## Exercise 2.12

> Which, if any, of the following names are invalid?
>
> (a) `int double = 3.14;`
> (b) `int _;`
> (c) `int catch-22;`
> (d) `int 1_or_2 = 1;`
> (e) `double Double = 3.14;`

(a), (c), and (d) are invalid

## Exercise 2.13

> What is the value of `j` in the following program?
>
> ```
> int i = 42;
> int main() {
>   int i = 100;
>   int j = i;
> }
> ```

`100`.

## Exercise 2.14

> Is the following program legal? If so, what values are printed?
>
> ```
> int i = 100, sum = 0;
> for (int i = 0; i != 10; ++i)
>   sum += i;
> std::cout << i << " " << sum << std::endl;
> ```

Legal. `100 45`.

## Exercise 2.15:

> Which of the following definitions, if any, are invalid? Why?
>
> (a) `int ival = 1.01;`
>
> (b) `int &rval1 = 1.01;`
>
> (c) `int &rval2 = ival;`
>
> (d) `int &rval3;`

(b) a reference can't be bound to a literal.

(d) a reference must be initialized.

## Exercise 2.16

> Which, if any, of the following assignments are invalid? If they are valid, explain what they do.
>
> ```cpp
> int i = 0, &r1 = i; double d = 0, &r2 = d;
> ```
>
> (a) `r2 = 3.14159;`
>
> (b) `r2 = r1;`
>
> (c) `i = r2;`
>
> (d) `r1 = d;`

(a) valid, same as `d = 3.14159`

(b) valid, automatically convert `int` to `double`.

(c) valid, same as `i = r2`, value will be truncated.

(d) valid, value will be truncated.

## Exercise 2.17

> What does the following code print?
>
> ```cpp
> int i, &ri = i;
> i = 5; ri = 10;
> std::cout << i << " " << ri << std::endl;
> ```

```
10 10
```

## Exercise 2.18

> Write code to change the value of a pointer. Write code to change the value to which the pointer points.

```cpp
int i = 1, j = 2;
int *p1 = &i, *p2 = p1;

// change the value of a pointer
p1 = &j;

// change the value to which the pointer points
*p2 = j;
```

## Exercise 2.19

> Explain the key differences between pointers and references.

- A pointer is an object in its own right, while a reference is another name of an already existing object.
- A pointer need not be initialized at the time it is defined, whilc a reference must be initialized.
- A opinter can be assigned and copied and can point to several different objects over its lifetime, while a reference bounds to its initial object once initialized.

## Exercise 2.20

> What does the following program do?
>
> ```cpp
> int i = 42;
> int *p1 = &i;
> *p1 = *p1 * *p1;
> ```

Point `p1` to `i`. Change `i`'s value to `42 * 42 = 1764`.

## Exercise 2.21

> Explain each of the following definitions. Indicate whether any are illegal and, if so, why.
>
> ```
> int i = 0;
> ```
>
> (a) `double* dp = &i;`
>
> (b) `int *ip = i;`
>
> (c) `int *p = &i;`

(a) illegal, can't point to `int` type with a pointer of `double *` type.

(b) illegal, can't initialize a variable of type `int *` with an rvalue of type `int`

(c) legal.

## Exercise 2.22

> Assuming `p` is a pointer to `int`, explain the following code:
>
> ```cpp
> if (p) // ...
> if (*p) // ...
> ```

```cpp
if (p) // p is nullptr?
if (*p) // the value point by p is 0?
```

## Exercise 2.23

> Given a pointer `p`, can you determine whether `p` points to a valid object? If so, how? If not, why not?

No, you have to first make sure that the pointer `p` is valid, then you can determine whether `p` points to a valid object.

## Exercise 2.24

> Why is the initialization of `p` legal but that of `lp` illegal?
>
> ```cpp
> int i = 42;    void *p = &i;     long *lp = &i;”
> ```

`void *` can points to any type, while `long *` can only points to `long` type.

## Exercise 2.25

> Determine the types and values of each of the following variables.
>
> (a) `int* ip, i, &r = i;`
>
> (b) `int i, *ip = 0;`
>
> (c) `int* ip, ip2;`

(a) `ip` is a pointer to `int`, `i` is an `int`, `r` is a reference to `int i`.

(b) `i` is an `int`, `ip` is a null pointer.

(c) `ip` is a pointer to `int`, `ip2` is an `int`.

## Exercise 2.26

> Which of the following are legal? For those that are illegal, explain why.
>
> (a) `const int buf;`
>
> (b) `int cnt = 0;`
>
> (c) `const int sz = cnt;`
>
> (d) `++cnt; ++sz;`

(a) illegal, error: `buf` is uninitialized `const`

(b) legal.

(c) `legal`

(d) `++cnt` legal; `++sz` illegal, error: attempt to write to `const` object

## Exercise 2.27

> Which of the following initializations are legal? Explain why.
>
> (a) `int i = -1, &r = 0;`
>
> (b) `int *const p2 = &i2;`
>
> (c) `const int i = -1, &r = 0;`
>
> (d) `const int *const p3 = &i2;`
>
> (e) `const int *p1 = &i2;`
>
> (f) `const int &const r2;`
>
> (g) `const int i2 = i, &r = i;`

(a) illegal, `r` must refer to an object.

(b) legal.

(c) legal.

(d) legal.

(e) legal.

(f) illegal, a reference can't be `const`.

(g) legal.

## Exercise 2.28

> Explain the following definitions. Identify any that are illegal.
>
> (a) `int i, *const cp;`
>
> (b) `int *p1, *const p2;`
>
> (c) `const int ic, &r = ic;`
>
> (d) `const int *const p3;`
>
> (e) `const int *p;`

(a) illegal, `cp` must be initialize.

(b) illegal, `p2` must be initialize.

(c) illegal, `ic` must be initialize.

(d) illegal, `p3` must be initialize.

(e) legal, `p` is a pointer to `const int`.

## Exercise 2.29

> Using the variables in the previous exercise, which of the following assignments are legal? Explain why.
>
> (a) `i = ic;`
>
> (b) `p1 = p3;`
>
> (c) `p1 = &ic;`
>
> (d) `p3 = &ic;`
>
> (e) `p2 = p1;`
>
> (f) `ic = *p3;`

(a) legal.

(b) illegal, `p` is a plain pointer, while `p3` points to a `const int`.

(c) illegal, `p` is a plain pointer, while `ic` is a `const int`.

(d) illegal, `p3` is a `const` pointer.

(e) illegal, `p2` is a `const` pointer.

(f) illegal, `ic` is a `const int`.

## Exercise 2.30

> For each of the following declarations indicate whether the object being declared has top-level or low-level const.
>
> ```cpp
> const int v2 = 0;    int v1 = v2;
> int *p1 = &v1, &r1 = v1;
> const int *p2 = &v2, *const p3 = &i, &r2 = v2;
> ```

- `v2`: top-level
- `v1`: none
- `p1`: none
- `r1`: none
- `p2`: lower-level
- `p3`: lower-level and top-level
- `r2`: lower-level

## Exercise 2.31

> Given the declarations in the previous exercise determine whether the following assignments are legal. Explain how the top-level or low-level const applies in each case.
>
> ```cpp
> r1 = v2;
> p1 = p2;    p2 = p1;
> p1 = p3;    p2 = p3;
> ```

```cpp
r1 = v2;  // illegal, can't bind an ordinary `int &` to a `const int` object
p1 = p2;  // illegal, p2 has a lower-level `const` but p1 doesn't
p2 = p1;  // legal
p1 = p3;  // illegal, p3 has a lower-level `const` but p1 doesn't
p2 = p3;  // legal
```

## Exercise 2.32

> Is the following code legal or not? If not, how might you make it legal?
>
> ```cpp
> int null = 0, *p = null;
> ```

illegal.

```cpp
int null = 0, *p = &null;
```

## Exercise 2.33

> Using the variable definitions from this section, determine what happens in each of these assignments:
>
> ```cpp
> a = 42;   b = 42;   c = 42;
> d = 42;   e = 42;   g = 42;
> ```

```cpp
a = 42;  // legal, assign 42 to a
b = 42;  // legal, assign 42 to b
c = 42;  // legal, assign 42 to c
d = 42;  // illegal, d is an `int *`, can do `*d = 42;`
e = 42;  // illegal, e is a `const int *`, can do `e = &c;`
g = 42;  // illegal, g is a `const int &` that's bound to ci
```

## Exercise 2.34

> Write a program containing the variables and assignments from the previous exercise. Print the variables before and after the assignments to check whether your predictions in the previous exercise were correct. If not, study the examples until you can convince yourself you know what led you to the wrong conclusion.

```cpp
#include <iostream>

int main() {
  int i = 0, &r = i;
  auto a = r;  // a is an int (r is an alias for i, which has type int)

  const int ci = i, &cr = ci;
  auto b = ci;   // b is an int (top-level const in ci is dropped)
  auto c = cr;   // c is an int (cr is an alias for ci whose const is top-level)
  auto d = &i;   // d is an int* (& ofan int objectis int*)
  auto e = &ci;  // e is const int* (& of a const object is low-level const)

  const auto f = ci;  // deduced type of ci is int; f has type const int
  auto& g = ci;       // g is a const int& that is bound to ci

  a = 42;
  b = 42;
  c = 42;
  *d = 42;
  e = &c;
  return 0;
}
```

## Exercise 2.35

> Determine the types deduced in each of the following definitions. Once you've figured out the types, write a program to see whether you were correct.
>
> ```cpp
> const int i = 42;
> auto j = i; const auto &k = i; auto *p = &i;
> const auto j2 = i, &k2 = i;
> ```

- `j` is an `int`
- `k` is a `const int &`
- `p` is a pointer to `const int`
- `j2` is a `const int`
- `k2` is a `const int &`

```cpp
#include <iostream>

// print i := int
// print PKi := pointer to const int
template <typename T>
void printType(const char* name, T t) {
  std::cout << name << " is " << typeid(t).name() << "\n";
}

int main() {
  const int i = 42;
  auto j = i;
  const auto& k = i;
  auto* p = &i;
  const auto j2 = i, &k2 = i;

  printType("j", j);
  printType("k", k);
  printType("p", p);
  printType("j2", j2);
  printType("k2", k2);
  return 0;
}
```

## Exercise 2.36

> In the following code, determine the type of each variable and the value each variable has when the code finishes:
>
> ```cpp
> int a = 3, b = 4;
> decltype(a) c = a;
> decltype((b)) d = a;
> ++c;
> ++d;
> ```

- `a` is an `int` with value `4`
- `b` is an `int` with value `4`
- `c` is an `int` with value `4`
- `d` is an `int &` with value `4`

## Exercise 2.37

> Assignment is an example of an expression that yields a reference type. The type is a reference to the type of the left-hand operand. That is, if `i` is an `int`, then the type of the expression `i = x` is `int&`. Using that knowledge, determine the type and value of each variable in this code:
>
> ```cpp
> int a = 3, b = 4;
> decltype(a) c = a;
> decltype(a = b) d = a;
> ```

- `a` is an `int` with value `3`
- `b` is an `int` with value `4`
- `c` is an `int` with value `3`
- `d` is an `int &` with value `3`

## Exercise 2.38

> Describe the differences in type deduction between `decltype` and `auto`. Give an example of an expression where `auto` and `decltype` will deduce the same type and an example where they will deduce differing types.

The way `decltype` handles top-level `const` and references differs subtly from the way `auto` does. When the expression to which we apply `decltype` is a variable, `decltype` returns the type of that variable, including top-level `const` and references:

```cpp
int i = 0, &r = i;

// same
auto a = i;         // a has type int
decltype(i) b = i;  // b has type int

// different
auto c = r;         // c has type int
decltype(r) d = r;  // d has type int &
```

## Exercise 2.39

> Compile the following program to see what happens when you forget the semicolon after a class definition. Remember the message for future reference.
>
> ```cpp
> struct Foo { /* empty   */ } // Note: no semicolon
> int main() {
>   return 0;
> }
> ```

```
main.cpp:1:32: error: expected ';' after struct
struct Foo { /* empty   */ } // Note: no semicolon
                            ^
                            ;
1 error generated.
```

## Exercise 2.40

> Write your own version of the `Sales_data` class.

```cpp
struct Sales_data {
  std::string bookNo;
  unsigned units_sold = 0;
  double revenue = 0.0;
  double price = 0.0;
};
```

## Exercise 2.41

> Use your `Sales_data` class to rewrite the exercises in § 1.5.1 (p. 22), § 1.5.2 (p. 24), and § 1.6 (p. 25). For now, you should define your `Sales_data` class in the same file as your `main` function.

## Exercise 2.42

> Write your own version of the `Sales_data.h` header and use it to rewrite the exercise from § 2.6.2 (p. 76).
