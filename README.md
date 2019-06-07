# Each: The Unexpressive Enumerable

## Learning Goal

* Use `each` to Work with an Array
* Explain why `each` is the least-expressive Enumerable

# Introduction

In the previous lesson you learned that many of the Enumerable family are
basically slight variations on `map` and `reduce`: `all?`, `any?`, etc.

But `map` and `reduce` are "child" Enumerables from the root Enumerable of them
all, `.each`. In this lesson we'll talk about `each`.

## Use `each` to Work with an Array

By now, you're so comfortable with Enumerables, you'll find `.each` follows the
pattern of the "Character of Enumerable Methods."

```ruby
oppressed_workers = ["Dopey", "Sneezy", "Happy", "Angry", "Doc", "Lemonjello", "Sleepy" ]
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

We've saved talking about `each` for last. Despite the fact that `each` most
simply expresses the "Character of Enumerable Methods," we're showing it _last_
because we to use it _least_. Why is that?

## Explain Why `each` is the Least-expressive Enumerable

We want to avoid `each` because it is the least-expressive Enumerable. It
communicates the _least_ to other programmers about what it is we're trying to
do.

By now you recognize that `map` means: "create a new `Array` after transforming
each element." You recognize that `reduce` means: "distill a value after
joining elements together."  These methods are _expressive_, their very nature
tells other programmers what you intended to happen.

But what does `each` mean? Programmers, including you, recognize that `map` has
a specific use, `reduce` has a specific use, `max` has a specific use. But
`each` is generic. Are we just printing things, or are we trying to distill to
a value, or are we trying to produce a transformed `Array`?

When we use `each` to do `map` things or `reduce` things we're not
_documenting_ what our intention was with regard to the collection. This makes
for code that's harder to understand and debug. Here's some code that uses
`each` instead of `reduce`.


```ruby
def sum_array(number_array)
  total = 0
  number_array.each{ |num| total += num }
  total
end
sum_array([1,2,3]) #=> 6
```

Sure, it works, but it doesn't _communicate_. We should always strive to have
code that communicates _first_ and works _second_.

## Identify Cases for `each`

The best time to use `each` is when you need to enumerate a collection but
aren't transforming data. It's also great to use when you're not quite sure
which Enumerable you want to use. The times when you're _not_ better off
`map`-ping or `reduce`-ing are few. The best use is to print out something to
the screen:

```ruby
oppressed_workers = ["Dopey", "Sneezy", "Happy", "Angry", "Doc", "Lemonjello", "Sleepy" ]
oppressed_workers.each do |oppressed_worker|
  puts "#{oppressed_worker.capitalize} wants to start a union!"
end
```

But on the other hand, you're probably just as good doing:

```ruby
oppressed_workers = ["Dopey", "Sneezy", "Happy", "Angry", "Doc", "Lemonjello", "Undercaffeinated" ]
angry_chants = oppressed_workers.map do |oppressed_worker|
  "#{oppressed_worker.capitalize} wants to start a union!"
end
p angry_chants

#=> ["Dopey wants to start a union!", "Sneezy wants to start a union!", "Happy wants to start a union!", "Angry wants to start a union!", "Doc wants to start a union!", "Lemonjello wants to start a union!", "Undercaffeinated wants to start a union!"]
```

## List `each` Variants

The `each` method has a few close cousins that follow the "Character of
Enumerable Methods." You want to _recognize_ them, but you needn't _memorize_
them. Consult the [Enumerables][enumdoc] documentation to see how the following
work:

* `each_cons`
* `each_entry`
* `each_slice`
* `each_with_index`
* `each_with_object` (a cousin of `reduce`)

## Conclusion

This concludes our discussion of `each`. It's the most flexible Enumerable, but
it's also the least expressive. When you aren't sure which way to go, you might
want to use it, but most of the time you really want to use `map` or `reduce`.



