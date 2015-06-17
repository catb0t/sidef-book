[1]: http://rosettacode.org/wiki/Rate_counter

# [Rate counter][1]

```ruby
var benchmark = require('Benchmark').();   # .() denotes that the Perl module is function-oriented
 
func job1 {
    #...job1 code...
};
func job2 {
    #...job2 code...
};
 
const COUNT = -1;   # run for one second
benchmark.timethese(COUNT, :('Job1' => job1, 'Job2' => job2));
```