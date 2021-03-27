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
    - Elixir has regex literals, written as `~r{regexp}` or `~r{regexp}opts`.
    - Considerably more flexible! Additionally, can choose any `nonalphanumeric characters` as delimiters.
    - We can also specify one or more single chars options following a regexp literal. 
    
    > | Opt | Meaning |
    > | - | - |
    > | f |  Force the pattern to start to match on the first line of a multiline string.|
    > | i | Make matches case insensitive |
    > | m | If the string to be matched contains multiple lines, ^ and $ match the start and end of these lines. \A and \z continue to match the beginning or end of the string |
    > | s | Allow. to match any newline characters. |
    > | U | Normally, modifiers like * and + are greedy, matching as much as possible. The U modifier makes them ungreedy, matching as little as possible. |
    > | u | Enable unicode-specific patterns like \p |
    > | x | Enable extended mode - ignore whitespace and comments (`#` to end of line) |

    - e.g.
    ```elixir
        > Regex.run ~r{[aeiou]}, "caterpillar"
        "a"

        > Regex.scan ~r{[aeiou]}, "caterpillar"
        [["a"], ["e"], ["i"], ["a"]]

        > Regex.split ~r{[aeiou]}, "caterpillar"
        ["c","t","rp","ll","r"]

        > Regex.replace ~r{[aeiou]}, "caterpillar", "*"
        "c*t*rp*ll*r"
    ```

#### **System Types**
These types reflect resources in the underlying `Erlang VM`.

- PIDs and Ports:
    - PID is a reference to a local or remote process
    - Port is a reference to a resource (typically external to the application) that you'll be reading or writing 
    - PID of the current process is available by calling `self`. A new PID is created when you spawn a new process.

- References:
    - Function `make_ref` creates a globally unique reference.
    - It is unique

#### **Collection Types**
Elixir collections can hold values of any type (including other collections).

- Tuples:
    - A tuple is an ordered collection of values. 
    - Once created a tuple cannot be modified.
    - i.e.
        ```elixir
            > { 1, 2 }
            > { :ok, 42, "next" }
            > { :error, :enoent }
        ```
    - A typical elixir tuple has `two` to `four` elements.
    - If you need more then we can use `maps` or `structs`.
    - Can be used in pattern matching too.
    - i.e.
        ```elixir
            > { status, count, action } = { :ok, 42, "next" }
            { :ok, 42, "next" }
            > status
            :ok
            > count
            42
            > action
            "next"
        ```

    - It is comon for functions to return a tuple where the first element is atom `:ok` if there were no errors.
    - i.e.
        ```elixir
            > { status, file } = File.open("somefile.exs")
            { :ok, #PID<x.x.x> }
            # A PID is how we access the contents
        ``` 
    - Usually we write code assuming success:
        ```exlixir
            > { :ok, file } = File.open("somefile.exs") # File that exists
            { :ok, #PID<x.x.x> }
            > { :ok, file } = File.open("newkopkaf.exs") # File that doesn't exist
            ** (MatchError) .... # return value is { :error. :enoent }
            # `enoent` is Unix-speak for "file doesn't exist"
        ```

- Lists:
