[1]: http://rosettacode.org/wiki/List_rooted_trees

# [List rooted trees][1]

```ruby
func bagchain(x, n, bb, start=0) {
    n || return [x]
 
    var out = []
    start.to(bb.end).each { |i|
        var (c, s) = @bb[i]
        if (c <= n) {
            out += bagchain([x[0] + c, x[1] + s], n-c, bb, i)
        }
    }
 
    return out
}
 
func bags(n) {
    n || return [[0, ""]]
    var upto = []
    (n-1).downto(1).each { |i| upto += bags(i) }
    bagchain([0, ""], n-1, upto).map{|p| [p[0]+1, '('+p[1]+')'] }
}
 
func replace_brackets(s) {
    var (depth, out) = (0, [])
    s.each { |c|
        if (c == '(') {
            out.append(<( [ {>[depth%3])
            ++depth
        }
        else {
            --depth
            out.append(<) ] }>[depth%3])
        }
    }
    return out.join
}
 
bags(5).each { |x|
    say replace_brackets(x[1])
}
```

#### Output:
```
([{([])}])
([{()()}])
([{()}{}])
([{}{}{}])
([{()}][])
([{}{}][])
([{}][{}])
([{}][][])
([][][][])
```