# Immutability

Have you heard about Immutability in Functional Programming? No? I have (in JS). They say that in a functional program, data cannot be altered once created. It's true for the most part. And indeed, Elixir enforces it.

Let's learn why? (Spoilers: In JS, String and Numbers are immutable. Any guesses on what isn't immutable? If you guessed arrays* & objects, you'd be right!!) 
> Note: *arrays in JS are only mutable when we're changing value of an index. Not when we're setting the value of an array.

**Consider following examples:**

```elixir
    > count = 99
    > do_something_with(count)
    > print(count)
```

- For this snippet, it will print out `99` and should always print out `99`. We can definitely bind a new value to `count` variable but that doesn't change the fact that value `99` will always be `99`. 
- In programming languages some built in functions are destructive and some are non-destructive.

**Imagine writing code in an enviornment where something running in parallel can change that `99` to be something else.**
```elixir
    > count = 99
    > do_something_with(count) # Changes 99 to a 100
    > print(count) # outputs 100
```
- This way we can never really gurantee that our code produced the correct results.

**Consider this in JS world:**
```js
    const person = {}
    const addsNameToAnObj = (arg) => arg['name'] = "John"
    console.log(person) // => Should print out {}

    addsNameToAnObj(person)
    console.log(person) // => Prints out { name: "John" }

    ...

    const myList = []
    const updateItemInList = (list) => list[0] = "Doge to the moon 🌝"
    console.log(myList) // => Should print out []

    updateItemInList(myList) 
    console.log(myList) // => Prints out [ "Doge to the moon 🌝" ]
```
- These functions are changing the array and the object on execution. Now imagine this happening when our code is running in parallel. That a whole another level of anxiety. We don't need that stress in our life when writing super cool code.
- Hence, the immutability. In many languages, there's built-in support for both behaviors: Mutabilitiy and Immutability. And based on what we use, we can classify it as `Mutable Data` or `Immutable Data`.

**In elixir, all values are immutable.** Hence we call it, *drum rolls please* `Data`.
- Once a variable references a value such as `[1, 2, 3]`, it will always reference those same values (unless and until we rebind the variable).
- This also helps breathe a little when writing code that runs concurrently.
- But what if I want to manipulate elements in the array? Elixir will produce a copy of the original with new values. It also goes well with the idea that programming in elixir is about `data transformation`. i.e. When we update [1,2,3], we transform it to something new.

**But Simon, what about the performance?**
When we think about efficiency, elixir's approach doesn't make any sense at first. Think about how efficient or really inefficient it is to create a new copy of values every time we update it. Also, what about left overs? What are we going to do with those?

- **"Is copying data really inefficient?"**
    >
    > Short answer, No.
    > Since elixir knows that existing data is immutable, it can reuse it. Partially or as a whole.
    > 
    > Let's take a look at an example:
    >
    > ```elixir
    >   > list1 = [1, 2, 3]
    >   [1,2,3]
    >   > list2 = [ 4 | list1 ]
    >   [4, 1, 2, 3]
    > ```
    >
    > In Most languages, `list2` is built by creating new list containing value 4 -> copying `list1` values to `list2`.
    >
    > In Elixir, `list1` never changes. Hence, the new list is created by constructing a new list by using head of `4` and tails of `list1`. 

- **Still, what about the leftovers?**
    > Using a transformational language we often end up with values in our `heap` that we don't use anymore. In modern languages these values are recycled by a sophesticated (or not so when they impact performance) `Garbage Collectors`. 
    >
    > Cool thing about elixir is that we write code using lots and lots of `processes`. Each `process` has its own heap. `Data` in our application is divided into individual `heaps`. Compared to a single central `heap` for all the data this is actually really good.
    >
    > As a result of this, `Garbage Collector` actually runs faster. And, the kicker is that if the `process` is terminated before `heap` is full then we don't even need it to run. All of the data is going to be discarded anyways! HA! That's super cool.

**To summarize:** 
- Once we make our peace with `Immutable Data`, coding with it is super duper simple.
- Like me if you're coming straight from `JS` or `Ruby` land, think of data as a `constant` and all the methods that you call on it `non-destructive`.
- Oh and also *our daily reminder*, Elixir isn't Object oriented. So, calling methods may look a little different. Calling methods on objects is long gone. For example;
    ```elixir
        # In Elixir,
        > name = "ash"
        "ash"
        > uppercased_name = String.capitalize name
        "Ash"
        > name 
        "ash"
    ```

    ```js
        // In JS,
        const name = "ash"
        name.toUpperCase() // => "ASH"
        // We can call method on a String object because the language can understand it.
    ```
- In a functional language, we **always** transform the data. We don't change the original. The syntax will keep reminding us that.

## 🙏🏻 References
- [Programming Elixir 1.6]
    - My notes are pretty much paraphrased content from this book! 
    - It is definitely one of the great ones.

[Programming Elixir 1.6]: https://pragprog.com/titles/elixir16/programming-elixir-1-6/
