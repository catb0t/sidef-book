[1]: http://rosettacode.org/wiki/LZW_compression

# [LZW compression][1]

```ruby
# Compress a string to a list of output symbols.
func compress(uncompressed is String) -> Array {
 
    # Build the dictionary.
    var dict_size = 256;
    var dictionary = Hash.new;
 
    0 .. dict_size-1 -> each { |i|
        dictionary[i.chr] = i.chr;
    };
 
    var w = '';
    var result = [];
    uncompressed.each { |c|
        var wc = w+c;
        if (dictionary.exists(wc)) {
            w = wc;
        } else {
            result.append(dictionary[w]);
            # Add wc to the dictionary.
            dictionary[wc] = dict_size;
            dict_size++;
            w = c;
        }
    };
 
    # Output the code for w.
    if (w != '') {
        result.append(dictionary[w]);
    };
 
    return result;
};
 
# Decompress a list of output ks to a string.
func decompress(compressed is Array) -> String {
 
    # Build the dictionary.
    var dict_size = 256;
    var dictionary = Hash.new;
 
    0 .. dict_size-1 -> each { |i|
        dictionary[i.chr] = i.chr;
    };
 
    var w = compressed.shift;
    var result = w;
    compressed.each { |k|
        var entry;
        if (dictionary.exists(k)) {
            entry = dictionary[k];
        } elsif (k == dict_size) {
            entry = w+w.substr(0,1);
        } else {
            die "Bad compressed k: #{k}";
        };
        result += entry;
 
        # Add w+entry[0] to the dictionary.
        dictionary[dict_size] = w+entry.substr(0,1);
        dict_size++;
 
        w = entry;
    };
    return result;
};
 
# How to use:
var compressed = compress('TOBEORNOTTOBEORTOBEORNOT');
say compressed.join(' ');
var decompressed = decompress(compressed);
say decompressed;
```

#### Output:
```
T O B E O R N O T 256 258 260 265 259 261 263
TOBEORNOTTOBEORTOBEORNOT
```