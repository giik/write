# Table of Contents
-----------------

- [Prologue](#prologue)
- [About C++](#about-c)
	- [Do Fold Expressions Shortcut?](#do-fold-expressions-shortcut)
- [About Go](#about-go)

-----------------

# Prologue
Collection of writings about stuff related to math, coding, and engineering.

# About C++

## Do Fold Expressions Shortcut?

It wasn't vey clear to me whether the [fold expressions](https://en.cppreference.com/w/cpp/language/fold) (introduced in C++17) shortcut, _e.g.,_ when the fold's binary operator is **logical and** `&&` or **logical or** `||`. It is a conclusion that also follows from the fact that `&&` and `||` shortcut and here is a little example to demonstrate that yes, fold expressions shortcut (also Compiler Explorer [link](https://godbolt.org/z/36YfxEbGE)):
```c++
#include <iostream>

bool g(int x) {
  std::cout << "g(" << x << ") is evaluated" << std::endl;
  return x % 2 == 0;
}

template <typename... Vs> bool all_even(Vs... vs) {
  return (... && g(vs));
}

int main() { return all_even(4, 7, 2, 0); }
```
Also of note: because of the sequence point requirement for the first (left) operand of either `&&` or `||` the order of evaluation of the expressions is always the same, left to right:
```c++
// left-fold requires that (E1 op E2) is evaluated first so the order is E1, E2, E3
(E1 op E2) op E3
// right-fold
E1 op (E2 op E3) requires that E1 is evaluated first so the order is E1, E2, E3
```

# About Go

Nothing yet.
