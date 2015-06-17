[1]: http://rosettacode.org/wiki/Arithmetic_evaluation

# [Arithmetic evaluation][1]

```ruby
func evalArithmeticExp(s) {
 
    func evalExp(s) {
 
        func operate(s, op) {
           s.split(op).map{|c|c.toNum}.reduce(op);
        }
 
        func add(s) {
            operate(s.replace(/^\+/,'').replace(/\++/,'+'), '+');
        }
 
        func subtract(s) {
            s.gReplace!(/(\+-|-\+)/,'-');
 
            if (s.match(/--/)) {
                return(add(s.replace(/--/,'+')));
            }
 
            var b = s.split('-') -> len == 3
                    ? (-1 * b[1].toNum - b[2].toNum)
                    : (operate(s, '-'));
        }
 
        s.gReplace!(/[()]/,'').gReplace!(/-\+/, '-');
 
        var reM  = /\*/;
        var reMD = %r"(\d+\.?\d*\s*[*/]\s*[+-]?\d+\.?\d*)";
 
        var reA  = /\d\+/;
        var reAS = /(-?\d+\.?\d*\s*[+-]\s*[+-]?\d+\.?\d*)/;
 
        var match;
        while (match = s.match(reMD)) {
            var cap = match.captures.first -> =~ reM ??
                ? (s.replace!(reMD, operate(cap, '*').to_s))
                : (s.replace!(reMD, operate(cap, '/').to_s));
        }
 
        while (match = s.match(reAS)) {
            var cap = match.captures.first -> =~ reA ??
                ? (s.replace!(reAS,      add(cap).to_s))
                : (s.replace!(reAS, subtract(cap).to_s));
        }
 
        return(s);
    }
 
    var rePara = /(\([^\(\)]*\))/;
    s = (s.split.join('').replace(/^\+/,''));
 
    while (var match = s.match(rePara)) {
        s.replace!(rePara, evalExp(match.captures.first));
    }
 
    return(evalExp(s).toNum);
}
```


Testing the function:

```ruby
for [
     ['2+3'                                      =>        5],
     ['-4-3'                                     =>       -7],
     ['-+2+3/4'                                  =>    -1.25],
     ['2*3-4'                                    =>        2],
     ['2*(3+4)+2/4'                              => 2/4 + 14],
     ['2*-3--4+-0.25'                            =>    -2.25],
     ['2 * (3 + (4 * 5 + (6 * 7) * 8) - 9) * 10' =>     7000],
    ] { |expr, res|
 
    var num = (evalArithmeticExp(expr)) == res || (
            "Error occurred on expression '#{expr}': got '#{num}' instead of '#{res}'\n".die;
    );
 
    "%-45s == %10g\n".printf(expr, num);
}
```