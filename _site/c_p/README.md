# Conventional Programming

Great language for Parallel Programming? A language first needs to be great at sequential programming to excel at Parallel Programming. Let's explore conventions that make Elixir so powerful.

#### Data types
- String
- Integer
- List (Similar to arrays)
- Map (Similar to object in JS / hash in Ruby)

#### Variable Assignment
  - Elixir looks for a way to make the value of the left side the same as the value of the right side.
  - `=` sign doesn't mean the same as before.
  - `=` sign doesn't mean assignment but means assertion.
  - It succeeds if Elixir can find a way of making the left-hand side equal to right-hand side.
  - `=` sign is called ***match operator*** in elixir.

    ```elixir
      > a = 1 # is true; because a is a variable
      > 1 = a # is true; because a is 1
      ...
      > 2 = a # is false && produces error
    ```
  - More complex Example
  ```elixir
    # Elixir bound the variable list to the list [1, 2, 3]
    > list = [1, 2, 3]
    > [a, b, c] = list
    > a
    1
    > b
    2
    > c
    3

    # [clear]
    > list = [1, 2, [3, 4, 5]]
    > [a, b, c] = list

    # [clear]
    > list = [1, 2, [3, 4]]
    > [a, 2, c] = list # still true; as literal 2 pattern matches to 2
    > [a, 1, c] = list # false; as literal 1 doesn't match value on the right

  ```
  - Elixir calls this process **pattern matching**

---

#### Exercise

```elixir

  # Which of the following will match?
  > a = [1,2,3] # Yes
  > a = 4 # Yes
  > 4 = a # Yes
  > [a,b] = [1,2,3] # No
  > a = [[1,2,3]] # Yes
  > [a] = [[1,2,3]] # Yes
  > [[a]] = [[1,2,3]] # No

```

---

#### Don't want to read a pattern match?
- If we didn't need to capture a value during the match, we can use the special variable `_`.
- This acts like a variable but immediately discards any value given to it in a pattern match.
- It is like a **wild card**

  ```elixir
    > [_, a, _] = [1, 3, 5]
  ```

---

#### Variables Bind Once (per match)
- Once a variable has been bound to a value in the matching process, it keeps the value for the remainder of the match.
```elixir
  > [a, a] = [1, 1] # works
  > a
  1
  > [b, b] = [1, 2] # Doesn't work
  ** (MatchError)
```

- However, variables can be bound to a new value in a later match.
```elixir
  > a = 1
  > a
  1
  > [1, a, 3] = [1, 2, 3] #Works
  > a
  2
```

- If you want to force elixir to use current value of the variable in a new pattern match, then use `^`. It is called **pin operator**
```elixir
  > a = 1
  1
  > a = 2
  2
  > ^a = 3
  ** (MatchError) # Because a is 2

  # This also works if variable is component of a pattern

  > a = 1
  > [^a, 2, 3] = [1, 2, 3] # Works
  ...
  > a = 2
  > [^a, 2] = [1, 2] # Doesn't work as a is 2
```

---

#### Exercise
  ```elixir

    > [a, b, a] = [1, 2, 3] # No
    > [a, b, a] = [1, 1, 2] # No
    > [a, b, a] = [1, 2, 1] # Yes

    # The variable a is bound to 2 for following.
    # a = 2
    > [a, b, a] = [1, 2, 3] # No
    > [a, b, a] = [1, 1, 2] # No
    > a = 1 # Yes
    > ^a = 2 # Yes because a is 2
    > ^a = 1 # No
    > ^a = 2 - a # No
  ```

---

### Another way of looking at the `=` sign
- You do not store the values in a variable anymore. You make an assertion.
- Just like in algebra. `x = a + 1`, You're not assigning value of `a + 1` to `x` but making an assertion that `x` & `a + 1` have the same value. If you know the value of `x` then you can work out `a + 1` and vice versa.
- This is different compared to imperative programming languages. Hence, we gotta unlearn what `=` means.
