# Looping with Arrays

## Learning Goals

- Use `Array`s to loop a specific number of times
- Access each element in an `Array` programmatically

## Introduction

With an understanding of `Array`s and `Hash`es, it is time to start putting
them to work. Finding out simple things like the size of the `Array` or whether
it contains the `String` `"Byron"` is useful, but only in a small way.

We will learn now how to loop through the elements of an `Array`.

## Hard-Coding Array Output

Let's consider a simple `pets` example.

```ruby
pets = ["Dog", "Cat", "Fish", "Bird"]
```

Say we wanted to output each element in the `pets` `Array`. We could write:

```ruby
puts pets[0] #=> Dog
puts pets[1] #=> Cat
puts pets[2] #=> Fish
puts pets[3] #=> Bird
```

This works, but it is what programmers refer to as _hard-coded_. Hard-code is
code that is fixed in place. The above statements all rely on the assumption
that the `pets` `Array` is going to be _four_ elements long.

But what if we added a new pet at index `4`, say, a hamster?  We go ahead and
add "Hamster" to our `Array` using the "shovel" operator:

```ruby
pets << "Hamster"
```

Unless we add the following code, we won't see it.

```ruby
puts pets[4] #=> Hamster
```

Obviously, this is not idea. We want to loop through "everything in the `pets`
`Array`, however long it is." By using a loop we can do this.

## Abstracting Array Output

A very basic example would be a while loop with a counter:

```ruby
counter = 0
pets = ["Dog", "Cat", "Fish", "Bird", "Hamster"]

while pets[counter] do
  puts pets[counter]
  counter += 1
end
```

The above code outputs:

```text
Dog
Cat
Fish
Bird
Hamster
```

So what is happening here? Remember that Ruby considers `nil` to be a _falsy_
value. If we step through this loop, we can see why this works.

1. When the Ruby interpreter first gets to the `while` loop, `counter` is equal
to `0`, so `pets[0]` returns `"Dog"`. Because `"Dog"` is a _truthy_ value, the
loop executes and `pets[0]` is output to the terminal. Then, `counter` is
incremented by `1`.

2. When the first loop completes, Ruby checks the condition for the `while` loop
again. This time, `counter` is equal to `1`. `pets[1]` returns `"Cat"`, causing
the loop to execute again, outputting `pets[1]` and incrementing `counter`.

3. On the third, fourth and fifth loops, the same things occurs. `pets[2]`
returns `"Fish"`, `pets[3]` returns `"Bird"`, and `pets[4]` returns `"Hamster"`.
All three are then output to the terminal.

4. On the last loop, `counter` is incremented to `5`. However, there is no sixth
element in the `Array`, so `pets[5]` returns `nil`. This stops the `while` loop.

With this set up, no matter how long or short the `pets` `Array` is, the loop will
output each element! We've built a _pet printer_ that works no matter how many
pets are in our `pets` `Array`!

We could go further than this, though, by placing our `while` loop in a method.
Instead of just a pet printer, we can turn this code into an all purpose
_element printer:_

```ruby
def output_array_elements(array)
  counter = 0

  while array[counter] do
    puts array[counter]
    counter += 1
  end
end
```

Now, we could still use this for pets and get the same results:

```ruby
pets = ["Dog", "Cat", "Fish", "Bird", "Hamster"]
output_array_elements(pets)
```

But we could also use `output_array_elements` with all kinds of `Array`s!

```ruby
output_array_elements(["hello", "how are you?", "goodbye!"])
```

The above code would produce:

```text
hello
how are you?
goodbye!
```

## Looping Using the Array Length Method

An common alternative to the previous example is to utilize the methods built in
to the Ruby `Array` class. Specifically, in these situations, we want to loop
as many times are there are elements. To find out how many elements are in an
`Array`, we can use the `length` method:

```ruby
array = ["Spring", "Summer", "Fall", "Winter"]
array.length
#=> 4
```

> **Note:** Ruby `Array`s also have methods called `size` and `count` that all
perform the same function - return the number of elements in the `Array`.

Now that we can get the length, we would want to structure our loop so that
we compare the value of `counter` with this length value. Updating the method
from the previous section, this might look something like:

```ruby
def output_array_elements(array)
  counter = 0

  while counter < array.length do
    puts array[counter]
    counter += 1
  end
end
```

As long as `counter` is less than the return value of `array.length`, the loop
will execute.

## Iteration

Using a loop to access each element in an `Array` is very common in programming
and is referred to as _iteration_. We _iterate_ over each element, in these
examples, printing out the values. In other examples, we might want to iterate
over an `Array` and update each element's value. If the values were numbers, we
could do things like _sum_ all the values together using while loops and basic
iteration.

## Conclusion

Loops are a powerful tool for working with `Array`s. With just a small amount of
code, we perform operations on every element in an `Array`, regardless of how
many elements there are!

## Resources

- [`while` loops][while]

[while]: https://ruby-doc.org/core-2.5.0/doc/syntax/control_expressions_rdoc.html#label-while+Loop
