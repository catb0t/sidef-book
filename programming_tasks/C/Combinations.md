[1]: http://rosettacode.org/wiki/Combinations

# [Combinations][1]

```ruby
func combine(n, set) {
 
    set.len || return [];
    n == 1  && return set.map{[_]};
 
    var (head, result);
    head   = set.shift;
    result = __FUNC__(n-1, [set...]);
 
    result.each { |subarray|
        subarray.prepend(head);
    };
 
    result + __FUNC__(n, set);
}
 
combine(3, 0..4).each {|row|
    say row.join(' ');
}
```
