[1]: http://rosettacode.org/wiki/Arrays

# [Arrays][1]

```ruby
# create an empty array
var arr = [];
 
# push objects into the array
arr.append("a");        # => ['a']
arr.append(1,2,3);      # => ['a', 1, 2, 3]
 
# change an element inside the array
arr[2] = "b";           # => ['a', 1, 'b', 3]
 
# set the value at a specific index in the array (with autovivification)
arr[5] = "end";         # => ['a', 1, 'b', 3, nil, 'end']
 
# resize the array
arr.resizeTo(-1);       # => []
 
# slice assignment
arr[0..2] = 'a'..'c';   # => ['a', 'b', 'c']
 
# any change made to the slice is visible in the original array
var slice = arr[2, 1];  # slice => ['c', 'b']
slice[1] = 'bar';       # array => ['a', 'bar', 'c']
 
# indices as arrays
var indices = [0, -1];
arr[indices] = ["foo", "baz"];  # => ['foo', 'bar', 'baz']
 
# retrieve an element
say arr[-1];            # => 'baz'
```