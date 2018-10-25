[1]: https://rosettacode.org/wiki/Cheryl's_Birthday

# [Cheryl's Birthday][1]

```ruby
struct Date(day, month)
 
var dates = [
    Date(15, "May"),
    Date(16, "May"),
    Date(19, "May"),
    Date(17, "June"),
    Date(18, "June"),
    Date(14, "July"),
    Date(16, "July"),
    Date(14, "August"),
    Date(15, "August"),
    Date(17, "August")
]
 
var filtered = dates.grep {
    dates.grep {
        dates.map{ .day }.count(.day) == 1
    }.map{ .month }.count(.month) != 1
}
 
var birthday = filtered.grep {
    filtered.map{ .day }.count(.day) == 1
}.group_by{ .month }.values.first_by { .len == 1 }[0]
 
say "Cheryl's birthday is #{birthday.month} #{birthday.day}."
```

#### Output:
```
Cheryl's birthday is July 16.
```