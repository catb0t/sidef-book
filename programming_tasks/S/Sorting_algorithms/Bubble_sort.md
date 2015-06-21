[1]: http://rosettacode.org/wiki/Sorting_algorithms/Bubble_sort

# [Sorting algorithms/Bubble sort][1]

```ruby
func bubble_sort(arr is Array) -> Array {
    loop {
        var swapped = false;
        { |i|
            arr[i-1] > arr[i] && (
                arr[i-1, i] = arr[i, i-1];
                swapped = true;
            );
        } * arr.offset;
        swapped || break;
    };
    return arr;
};
```