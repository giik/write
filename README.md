# Table of Contents

TODO: Need to figure this out.

# Prologue

Collection of writings about stuff related to math, coding, and engineering.

# About C++

## Do Fold Expressions Shortcut?

It wasn't vey clear to me whether [fold
expressions](https://en.cppreference.com/w/cpp/language/fold) (introduced in
C++17) shortcut, _e.g.,_ when the fold's binary operator is **logical and** `&&`
or **logical or** `||`. They should be due to the fact that the operators `&&`
and `||` shortcut themselves, and, here is an example to demonstrate that yes,
fold expressions shortcut (also Compiler Explorer
[link](https://godbolt.org/z/36YfxEbGE)):

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

Also note: because of the sequence point requirement for the first (left)
operand of either `&&` or `||` the order of evaluation of the expressions is
always the same, left to right:

```c++
// left-fold requires that (E1 op E2) is evaluated first so the order is E1, E2,
// E3
(E1 op E2) op E3

// right fold requires that E1 is evaluated first so the order is E1, E2, E3
E1 op (E2 op E3)
```

# About Go

Nothing yet.


# MacOs Setup

How I setup my MacBook Pro M1 (13-inch, 2020), Apple Silicon, to work they way I
wanted it.

## Install Software

*  Install Xcode from the App Store;
   *  also install the command line tools.

*  Install [QLMarkdown](http://github.com/sbarex/QLMarkdown/releases) to be able
   to use the Apple [Quick
   Look](http://support.apple.com/guide/mac-help/view-and-edit-files-with-quick-look-mh14119/mac)
   feature to preview files, specifically `*.md` and `*.markdown` files as
   rendered markdown and not the source.  Works really well so far!

*  Install [MacPorts](http://www.macports.org) by downloading the package
   installer directly from http://www.macports.org/install.php, make sure to get
   the [Big Sur version
   v2.7.1](https://github.com/macports/macports-base/releases/download/v2.7.1/MacPorts-2.7.1-11-BigSur.pkg).

*  Use MacPorts to [install emacs](http://ports.macports.org/port/emacs/), I
   mostly use it command line mode.  It is installed in `/opt/local/bin/emacs`.
   *  Enable packages in emacs (see [MELPA](
      http://melpa.org/#/getting-started)), make sure to enable normal and
      stable versions; if only stable is enabled you will not see many packages
   * Install [markdown mode](http://jblevins.org/projects/markdown-mode/).
   * Install a few color themes.
   * Install the `clang-format` package so I can format C and C++ files.  It
     didn't work right out of the box because it could not find the
     `clang-format` binary so I had to figure out how to get this.  Downloaded
     [clang
     v12.0](http://github.com/llvm/llvm-project/releases/tag/llvmorg-12.0.0),
     then copied **just** `clang-format` to the MacPorts bin directory using
	 
	 ```
	 sudo cp ~/Downloads/clang+llvm-12.0.0-x86_64-apple-darwin/bin/clang-format /opt/local/bin
	 ```
	 
	 As expected, needed to approve running it in the `Security & Privacy`
     preferences.  TODO: this is still not fully functional, the formatting
     works on the command line but not in emacs, apparently some sort of config
     file needs to be generated.  Will try and follow these
     [instructions](https://emacs.stackexchange.com/questions/55635/how-can-i-set-up-clang-format-in-emacs).
   * Set up Authy (app from Twillio) for 2FA for Github.  A bit of a mess, but
     mostly worked.  Need to figure out how to cache the token in the keychain
     so I don't have to enter it every time I `git push`.

