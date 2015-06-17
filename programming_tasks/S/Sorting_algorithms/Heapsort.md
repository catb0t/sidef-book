[1]: http://rosettacode.org/wiki/Sorting_algorithms/Heapsort

# [Sorting algorithms/Heapsort][1]

```ruby
func siftDown(a, start, end) {
    var root = start;
    while ((2*root + 1) <= end) {
        var child = (2*root + 1);
        if ((child+1 <= end) && (a[child] < a[child + 1])) {
            child += 1;
        };
        if (a[root] < a[child]) {
            a[child, root] = a[root, child];
            root = child;
        } else {
            return;
        }
    }
}
 
func heapify(a, count) {
    var start = ((count - 2) / 2);
    while (start >= 0) {
        siftDown(a, start, count-1);
        start -= 1;
    }
}
 
func heapSort(a, count) {
    heapify(a, count);
    var end = (count - 1);
    while (end > 0) {
        a[0, end] = a[end, 0];
        end -= 1;
        siftDown(a, 0, end)
    }
}
 
var arr = (1..10 shuffle);  # creates a shuffled array
say arr.dump;               # prints the unsorted array
heapSort(arr, arr.len);     # sorts the array in-place
say arr.dump;               # prints the sorted array
```

#### Output:
```
[10, 5, 2, 1, 7, 6, 4, 8, 3, 9]
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```