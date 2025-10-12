<!-- :toc: macro -->
<!-- :toc-title: -->
<!-- :toclevels: 99 -->

# forward_circular_buffer <!-- omit from toc -->

> A header-only C++ 23 container providing a circular buffer where `begin()` points to the oldest written element and `end()` to the newest.

## Table of Contents <!-- omit from toc -->

* [General Information](#general-information)
* [Technologies Used](#technologies-used)
* [Features](#features)
* [Setup](#setup)
* [Usage](#usage)
* [Project Status](#project-status)
* [Room for Improvement](#room-for-improvement)
* [Acknowledgements](#acknowledgements)
* [License](#license)

## General Information

* `forward_circular_buffer` is a fixed-size circular buffer implementation using `std::array` as storage.
* Iteration order starts from the oldest element and proceeds forward to the newest.
* It provides contiguous-style iterators, random access, and STL-like semantics (`begin`, `end`, `rbegin`, etc.).

## Technologies Used

* C++ 23
* STL (`std::array`, `std::iterator`, `std::construct_at`, `std::destroy_at`)
* Custom runtime assertions via `stdfunc::assert`

## Features

* Fixed-capacity, compile-time sized circular buffer (N elements)
* Iteration order: oldest - newest
* `begin()`, `end()`, `rbegin()`, `rend()` with full iterator support
* STL-like interface (push_back, emplace_back, pop_back, front, back, clear, fill)
* Compile-time safety via concepts and assertions
* Works with trivially or non-trivially constructible types
* Header-only - no linking required

## Setup

There are no external dependencies other than the C++ 23 standard library and `stdfunc` for assertions.

To use it:

```cpp
#include "forward_circular_buffer.hpp"
```

See `config.sh` for what to include.

## Usage

```cpp
#include <print>

#include "forward_circular_buffer.hpp"

auto main() -> int {
    fcb::forwardCircularBuffer_t< int, 5 > l_buffer;

    l_buffer.push_back( 1 );
    l_buffer.push_back( 2 );
    l_buffer.push_back( 3 );

    for (auto _value : l_buffer) {
        std::print( "{} ", _value ); // Output: 1 2 3
    }

    l_buffer.pop_back(); // Removes 3
    l_buffer.push_back( 4 );
    l_buffer.push_back( 5 );

    for (auto _value : l_buffer) {
        std::print( "{} ", _value ); // Output: 1 2 4 5
    }

    return ( EXIT_SUCCESS );
}
```

`begin()` returns the oldest written element, and `end()` refers to current write position.
`front()` and `back()` give the oldest and most recently written elements respectively.

## Project Status

Project is: _in progress_.

## Room for Improvement

To do:

* Add `erase()` and `insert()` operations
* Implement `begin()`, `end()`

## Acknowledgements

* This project was based on `std::array` and `std::vector`.

## License

This project is open source and available under the
[GNU Affero General Public License v3.0](LICENSE).
