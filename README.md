# Looping with Arrays

## Learning Goals

- Use arrays to loop a specific number of times
- Access each element in an array programmatically

## Introduction

Arrays are often used to hold collections of related values. However, the power of 
arrays is made much clearer when we can _work_ with all the data they contain. 

So far, we've learned how to add and remove values from arrays, as well as
access and change specific values. It is time to start putting arrays to work. So
far, we've been working on arrays that we can see ahead of time.

```ruby
pets = ["Dog", "Cat", "Fish", "Bird"]
```

Above, we can see what elements are present and what order they are in. However,
as we build more complex projects, we will start to run into situations where
we have to handle an array that we _don't_ know the contents of or how many
elements there actually are inside!

We need to take a programmatic approach to this. We previously brought up the
concept of abstracting code - that is, writing code that moves away from
concrete details in favor of a reusable, generalized process.

In this lesson, we're going to discuss one of the most common ways to handle
arrays abstractly - we will be using _loops_ to access their elements.

## Hard-Coding Array Output

Let's consider the `pets` example a little further.

```ruby
pets = ["Dog", "Cat", "Fish", "Bird"]
```

Say we wanted to output each element in the `pets` array. We could write:

```ruby
puts pets[0] #=> Dog
puts pets[1] #=> Cat
puts pets[2] #=> Fish
puts pets[3] #=> Bird
```

This works, but it is what programmers refer to as _hard-coded_. Hard-code is
code that is fixed in place. The above statements all rely on the assumption
that the `pets` array is going to be _four_ elements long. If we modified the
`pets` array, say we want to add an additional pet, the hamster. We go ahead and
add "Hamster" to our array:

```ruby
pets << "Hamster"
```

But now, if we want to output hamster, we _also_ have to add an additional `puts`
statement:

```ruby
puts pets[4] #=> Hamster
```

Without this addition, `Hamster` would never be output to the terminal. Every
change we make to the `pets` array would require an additional modification to
our code. In a complex program, this can quickly become a major headache.

By using a loop, however, we can abstract away the need for additional
modifications.

## Abstracting Array Output

Given our `pets` array, it would be great to simply say "for every element in
this array, output the element to the terminal." This way, even if the array
changed, we'd always output each and every element.

With loops, we can do this! A very basic example would be a while loop with a
counter:

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
element in the array, so `pets[5]` returns `nil`. This stops the `while` loop.

With this set up, no matter how long or short the `pets` array is, the loop will
output each element! We've built a _pet printer_ that works no matter how many
pets are in our `pets` array!

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

But we could also use `output_array_elements` with all kinds of arrays!

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
array, we can use the `length` method:

```ruby
array = ["Spring", "Summer", "Fall", "Winter"]
array.length
#=> 4
```

> **Note:** Ruby arrays also have methods called `size` and `count` that all
perform the same function - return the number of elements in the array.

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

Using a loop to access each element in an array is very common in programming and 
is generally referred to as _iteration_. We _iterate_ over each element, in these
examples, printing out the values. In other examples, we might want to iterate
over an array and update each element's value. If the values were numbers, we could
do things like _sum_ all the values together using while loops and basic iteration.

## Conclusion

Loops are a powerful tool for working with arrays. With just a small amount of
code, we perform operations on every element in an array, regardless of how
many elements there are!

## Resources

- [`while` loops][while]

[while]: https://ruby-doc.org/core-2.5.0/doc/syntax/control_expressions_rdoc.html#label-while+Loop
