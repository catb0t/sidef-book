[1]: http://rosettacode.org/wiki/String_comparison

# [String comparison][1]

```ruby
var methods = %w(== != > >= < <= <=>);
[%w(YUP YUP),%w(YUP Yup),%w(bot bat),%w(aaa zz)].each {|arr|
    var (s1, s2) = arr...;
    methods.each{|m| "%s %s %s\t%s\n".printf(s1, m, s2, s1.(m)(s2))};
    print "\n";
}
```
