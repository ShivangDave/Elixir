#### Objectives
- Functional Programming
- Immutable State
- Data transformation using functions
- Get things done!

#### Introduction
- We can make the functions run in parallel. Elixir has a way to pass messages between them. It is simple but powerful.
- These are not same old processes or threads. Potentially, we can run millions of them on a single machine and have hundreds of machines incorporating.
- This power comes at a price!!! Very different from object oriented programming. So you gots to unlearn stuff.

- `iex`: Interactive Elixir (Similar to `irb` in ruby)
- Exit: `ctrl + c -> a + Enter` OR `ctrl + g -> q + Enter` to quit `iex`.
- Help:
  - `h(...)` logs help and support information (IEx.Helpers).
  - `i ...` Another informative helper
- Input / Output: `IO module` performs common IO. Ex: `IO.puts "Hello"`
- Customizing: `h IEx.configure`
- File Extensions:
  - `.ex`: Intended to be compiled into byte code and then run.
  - `.exs`: More like scripting languages. Interpreted at the source level.
  - Typically, application files will have `.ex` extension and test files will have `.exs` because we don't need to keep compiled versions of test.
- Running code:
  - `elixir <file_name>`
  - `iex > c "<file_name>"` - Return value for `c` function is a list of modules in the source file.
- Import files: `import_file` let's you import files and makes local variables available in `iex` session.
- Elixir convention: Use two-column indentation and spaces (not tabs)

- Think differently!
  - OO isn't the only way to design code.
  - Functional programming doesn't need to be complex or mathematical
  - Bases of programming are NOT: `assignments, if statements & loops`
  - Concurrency doesn't need `locks, semaphores, monitors, etc...`
  - Processes aren't always expensive.
  - Metaprogramming isn't just something tacked onto a language.
  - Programming should be fun.
