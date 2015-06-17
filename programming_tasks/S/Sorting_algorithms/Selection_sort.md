[1]: http://rosettacode.org/wiki/Sorting_algorithms/Selection_sort

# [Sorting algorithms/Selection sort][1]

```ruby
class Array {
    method selectionsort {
        0 to (self.len-2) each { |i|
            var min_idx = i;
            i+1 to (self.len-1) each { |j|
                self[j] < self[min_idx] && (
                    min_idx = j;
                );
            };
            self[i, min_idx] = self[min_idx, i];
        };
        return self;
    }
}
 
var ary = [7,6,5,9,8,4,3,1,2,0];
say ary.selectionsort.dump;
```