 # Code Along: Manipulating Nested Hashes

## Objectives

1. Iterate through a nested hash
2. Modify the correct element in a nested hash

## Why Nested Hashes Matter

So much of what we do in programming involves storing data in hashes. Often the
hashes that we will encounter will have more than one level. As we get into the
web, this will become abundantly clear. To build programs in the future, we'll
absolutely need to get comfortable working with hashes. Let's get started!

## Code Along Exercise

Fork and clone this lab. You'll be coding your solution in `lib/contacts.rb`.
You'll be manipulating the following `Hash`:

```ruby
contacts = {
  "Jon Snow" => {
    name: "Jon",
    email: "jon_snow@thewall.we",
    favorite_ice_cream_flavors: ["chocolate", "vanilla"]
  },
  "Freddy Mercury" => {
    name: "Freddy",
    email: "freddy@mercury.com",
    favorite_ice_cream_flavors: ["strawberry", "cookie dough", "mint chip"]
  }
}
```

Your good buddy Freddy Mercury has recently developed a strawberry allergy! You
need to delete `"strawberry"` from his list of favorite ice cream flavors in the
`remove_strawberry` method.

Iterate over the `contacts` hash and when you reach the key
`:favorite_ice_cream_flavors`, remove `"strawberry"` from the Array of Freddy's
favorite ice cream flavors.

There are at least two ways you can accomplish this, and for this codealong,
we'll work with the second way.

  1. You can directly iterate over the hash that is the value of the `"Freddy
Mercury"` key by calling an enumerator method in `contacts["Freddy Mercury"]`.

  2. You can set a conditional to iterate through the hash for `Freddy Mercury` only and when you reach the appropriate level,
check to see if the key `==` ("is equal to") `:favorite_ice_cream_flavors`. If
it does, check to see if that array contains `"strawberry"`. If it does, then
delete it from the `Array`.

#### Step 1: Iterate over the first level

Inside the `remove_strawberry` method, let's take our first dive into the
contacts `Hash`. Then we'll use `binding.pry` to see where we are.

We are going to first iterate over the top level of the `Hash` where the keys
should be the person and the values should be a `Hash`  of details about the
person.

**Note on variable naming:** This process will be remarkably easier if you name
your variables to accurately reflect the data they represent. For now, when the
value we're iterating over is another hash, we will explicitly add a `_hash` to
the end of the variable name (E.G. `contact_details_hash` below).

```ruby
contacts.each do |person, contact_details_hash|
  binding.pry
end
```

In the terminal, let's hit the `pry` by running `learn`, and check
that our defined variables (`person` and `contact_details_hash`) match our
expectations.

```bash
> person
=> "Jon Snow"

> contact_details_hash
=> {:name=>"Jon", :email=>"jon_snow@thewall.we", :favorite_ice_cream_flavors=>["chocolate", "vanilla"]}
```

Excellent! They do!

Type `exit` while in pry to continue (a second `pry` will trigger since we have
_two_ contacts). Running `learn` will also display a test, which we haven't
passed just yet.

You can also run `ruby lib/contacts.rb` in the terminal - instead of displaying the
the test results, this will reach the `binding.pry`.

#### Step 2. Iterate over the second level

```ruby
contacts.each do |person, contact_details_hash|
  if person == "Freddy Mercury"
    contact_details_hash.each do |attribute, data|
      binding.pry
    end
  end
end
```

Again, let's jump into our `binding.pry` using `learn`. You should see:

```bash
> attribute
=> :name

> data
=> "Jon"
```

#### Step 3. Locate the element we're looking for

```ruby
contacts.each do |person, contact_details_hash|
  if person == "Freddy Mercury"
    contact_details_hash.each do |attribute, data|
      if attribute == :favorite_ice_cream_flavors
        binding.pry
      end
    end
  end
end
```

What is `data` when we hit the binding? If it's unclear, let's go into our
binding.

#### Step 4. Update the hash

Lastly, we will use `delete_if` to iterate through the ice cream array and
remove any element that matches "strawberry". `delete_if` will iterate through
the hash and delete the key/value pair if the block returns `true`. [Learn more
about it in the ruby docs.][rubydocs].

```ruby
contacts.each do |person, contact_details_hash|
  if person == "Freddy Mercury"
    contact_details_hash.each do |attribute, data|
      if attribute == :favorite_ice_cream_flavors
        data.delete_if {|ice_cream| ice_cream == "strawberry"}
      end
    end
  end
end
```

```ruby
def remove_strawberry(contacts)
  contacts.each do |person, contact_details_hash|
    if person == "Freddy Mercury"
      contact_details_hash.each do |attribute, data|
        if attribute == :favorite_ice_cream_flavors
          data.delete_if {|ice_cream| ice_cream == "strawberry"}
        end
      end
    end
  end
end
```

Congrats! You made it. Test that your method works by running `ruby
bin/contacts` in the terminal. It should output the hash without strawberry ice
cream. Also, be sure to run the specs to make sure they pass.

[rubydocs]: https://docs.ruby-lang.org/en/2.0.0/Hash.html#method-i-delete_if

<a href='https://learn.co/lessons/nested-hash-iteration-code-along' data-visibility='hidden'>View this lesson on Learn.co</a>
