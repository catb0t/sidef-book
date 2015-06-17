[1]: http://rosettacode.org/wiki/Anagrams/Deranged_anagrams

# [Anagrams/Deranged anagrams][1]

```ruby
func find_deranged(a) {
    a.range.each { |i|
        i+1 ... a.offset -> each { |j|
            a[i].overlaps(a[j]) || (
                "length %d: %s => %s\n".printf(a[i].len, a[i], a[j]);
                return true;
            );
        }
    };
    return false;
}
 
func main () {
    var file = %f'/tmp/unixdict.txt';
 
    file.open_r(&var fh, &var err)
        || "Can't open file `#{file}' for reading: #{err}\n".die;
 
    var letter_list = Hash.new;
 
    # Store anagrams in hash table by letters they contain
    fh.words.each { |word|
        letter_list[word.sort] \\= [] append(word);
    };
 
    letter_list.keys
         .grep {|k| letter_list[k].len > 1}      # take only ones with anagrams
         .sort {|a,b| b.len <=> a.len}           # sort by length, descending
         .each {|key|
 
        # If we find a pair, they are the longested due to the sort before
        find_deranged(letter_list[key]) && break;
    };
}
 
main();
```

#### Output:
```
length 10: excitation => intoxicate
```