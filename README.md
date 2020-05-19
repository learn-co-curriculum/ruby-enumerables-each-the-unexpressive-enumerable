# Each: The Unexpressive Enumerable

## Learning Goal

* Use `each` to Work with an Array
* Explain why `each` is the least-expressive Enumerable

## Introduction

There are many Enumerable methods that do specific things. In the introduction
to this section, we stated that _usually_ an Enumerable performs work on a
collection and returns a new collection of results or aggregates the results
into a single value. There is one exception to this, and it happens to be the
root Enumerable of all other Enumerables - `each`. In this lesson, we'll talk
about `each` and how we use it.

## Use `each` to Work with an Array

The `each` method follows the pattern of all Enumerable methods - enumerate over
a collection and do some work with each element.

```ruby
chapter_titles = ["1. The Beginning", "2. The Middle", "3. The End"]
chapter_titles.each do |title|
  puts title
end #=>
# 1. The Beginning
# 2. The Middle
# 3. The End
```

The `each` method provides a block where we can access the individual
elements in an array. In the example above, `title` is equal to the
current array element. `each` visits every element and _yields_ to the block,
allowing us to do something with the element. Here, we're using `puts` to print
each element out.

## Explain Why `each` is the Least-Expressive Enumerable

We are teaching `each` early mainly for one reason - it is possible to use
`each` to recreate the behavior of all other Enumerables. For instance, we just
learned a bit about `count` in the previous lesson. We _could_ achieve the
behavior of `count` using `each` and a variable. The following two code snippets
achieve the same result:

```rb
[1,2,3,4].count do |num|
  num.even?
end
 # => 2
```

```rb
total = 0
[1,2,3,4].each do |num|
  if num.even?
    total += 1
  end
end
total
 # => 2
```

While both code snippets are valid, one is more _expressive_. `count`
communicates more to other programmers about what it is we're trying to do.

If you find yourself using `each` to collect data like we did above, there is
likely a better, more specific Enumerable built for the task. Sure, it works,
but it doesn't _communicate_. We should always strive to have code that
communicates _first_ and works _second_.

## Identify Cases for `each`

The best time to use `each` is when you need to enumerate a collection but
aren't transforming data. It's also a good starting place for when you're not
quite sure which Enumerable you want to use. The best use is to print out
something to the screen:

```ruby
oppressed_workers = ["dopey", "sneezy", "happy", "angry", "doc", "lemonjello", "sleepy" ]
oppressed_workers.each do |oppressed_worker|
   puts "#{oppressed_worker.capitalize} wants to start a union!"
end #=>
# Dopey wants to start a union!
# Sneezy wants to start a union!
# Happy wants to start a union!
# Angry wants to start a union!
# Doc wants to start a union!
# Lemonjello wants to start a union!
# Sleepy wants to start a union!
```

We aren't concerned with changing the original array, nor are we concerned with
what is returned in the block. Remember that with `count`, elements were counted
based on whether or not **the block returned a truthy value**. For `each`, nothing
needs to be returned in the block because `each` doesn't transform the data.

## List `each` Variants

The `each` method has a few close cousins that provide slight variations in
behavior. You want to _recognize_ them, but you needn't _memorize_ them. Consult
the [Enumerables][enumdoc] documentation to see how the following work:

* `each_cons`
* `each_entry`
* `each_slice`
* `each_with_index`
* `each_with_object` (a cousin of `reduce`)

## Conclusion

This concludes our discussion of `each`. It's the most flexible Enumerable, but
it's also the least expressive. When you aren't sure which way to go, you might
want to use it, but most of the time you really want to use `map` or `reduce`.
