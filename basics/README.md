# Elixir Basics
Let's go over some data types that elixir supports. 

#### **Built In Types**
- Value types:
    - Arbitrary-sized Integers
    - Floating-point Numbers
    - Atoms
    - Ranges
    - Regular Expressions (RegEx) 
    > `Ranges` & `RegEx` isn't value type technically. Under the hood they're structures. 

- System types:
    - PIDs and ports
    - References

- Collection types:
    - Tuples
    - List
    - Maps
    - Binaries

- Functions

This list doesn't include things like `String` and `Structures`. Elixir does support em. But they are derived from basic (Fundamental) types listed above. `Functions`, `String` and `Structures` are important. Hence, they'll be discussed in detail.

#### **Value Types**
- Integers:
    - Can be written in `decimal` (1234), `hexa-decimal` (0xcafe), `octal` (0o765) and `binary` (0b1010)
    - Decimal numbers may contain `_`, they are usually used to separate three digits in a large number. i.e.  `1_000_000`
    - No fixed limits on the size of integers.
    ```elixir
        > factorial(10000)
        # 28462596809170545189... so on for 35640 more digits
    ```

- Floating-Point Numbers:
    - There must be atleast one digit before and after the decimal point when writing floating point numbers. i.e. `1,0`, `0.2456`, `0.314159e1`, `314159.0e-5`
    - Floats are `IEEE 754` double precision, giving em `16` digits of accuracy and a maximum exponent of around `10^308` 

- Atoms:
    - Atoms are constants that represent something's name.
    - Like symbols in `Ruby`
    - We can also create atoms that contains arbitrary characters.
    - i.e. `:joe`, `:is_something?`, `:var@3`, `:==`, `:<>`
    - **Atom's name is its value**
    - We'll use atoms alot to tag values.

- Ranges:
    - `start..end` => where start and end are integers

- RegEx: 
    - 