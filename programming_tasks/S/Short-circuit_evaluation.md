[1]: http://rosettacode.org/wiki/Short-circuit_evaluation

# [Short-circuit evaluation][1]

```ruby
func a(bool) { print 'A'; return bool };
func b(bool) { print 'B'; return bool };
 
# Test-driver
func test() {
    ['&&', '||'].each { |op|
        [[1,1],[1,0],[0,1],[0,0]].each { |pair|
            "a(%s) %s b(%s): ".printf(pair[0], op, pair[1]);
            a(pair[0].to_bool).$op(b(pair[1].to_bool));
            print "\n";
        };
    };
};
 
# Test and display
test();
```

#### Output:
```
a(1) && b(1): AB
a(1) && b(0): AB
a(0) && b(1): A
a(0) && b(0): A
a(1) || b(1): A
a(1) || b(0): A
a(0) || b(1): AB
a(0) || b(0): AB
```