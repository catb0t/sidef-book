# Structures

A structure is essentially a class without methods, and can be used as a stricter alternative to hashes.

```ruby
struct Person {
    String name,
    Number age,
}

# Create a new person
var john = Person(name: "John Smith", age: 42);

# Change a value
john.name = "Dr. #{john.name}";

# Increment a value
john.age++;

say john.name;       #=> Dr. John Smith
say john.age;        #=> 43
```
