[1]: http://rosettacode.org/wiki/Arithmetic_evaluation

# [Arithmetic evaluation][1]

```ruby
func evalArithmeticExp(s) {
 
    func evalExp(s) {
 
        func operate(s, op) {
           s.split(op).map{|c| c.to_num }.reduce(op);
        }
 
        func add(s) {
            operate(s.sub(/^\+/,'').sub(/\++/,'+'), '+');
        }
 
        func subtract(s) {
            s.gsub!(/(\+-|-\+)/,'-');
 
            if (s ~~ /--/) {
                return(add(s.sub(/--/,'+')));
            }
 
            (var b = s.split('-')).len == 3
                    ? (-1 * b[1].to_num - b[2].to_num)
                    : (operate(s, '-'));
        }
 
        s.gsub!(/[()]/,'').gsub!(/-\+/, '-');
 
        var reM  = /\*/;
        var reMD = %r'(\d+\.?\d*\s*[*/]\s*[+-]?\d+\.?\d*)';
 
        var reA  = /\d\+/;
        var reAS = /(-?\d+\.?\d*\s*[+-]\s*[+-]?\d+\.?\d*)/;
 
        var match;
        while (match = s.match(reMD)) {
            (var cap = match.captures[0]) ~~ reM
                ? (s.sub!(reMD, operate(cap, '*').to_s))
                : (s.sub!(reMD, operate(cap, '/').to_s));
        }
 
        while (match = s.match(reAS)) {
            (var cap = match.captures[0]) ~~ reA
                ? (s.sub!(reAS,      add(cap).to_s))
                : (s.sub!(reAS, subtract(cap).to_s));
        }
 
        return(s);
    }
 
    var rePara = /(\([^\(\)]*\))/;
    s.split!.join!('').sub!(/^\+/,'');
 
    var match;
    while (match = s.match(rePara)) {
        s.sub!(rePara, evalExp(match.captures[0]));
    }
 
    return(evalExp(s).to_num);
};
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
    ] { |arr|
 
    var (expr, res) = arr...;
    var num = (evalArithmeticExp(expr)) == res || (
            "Error occurred on expression '#{expr}': got '#{num}' instead of '#{res}'\n".die;
    );
 
    "%-45s == %10g\n".printf(expr, num);
}
```