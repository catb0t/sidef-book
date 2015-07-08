[1]: http://rosettacode.org/wiki/Ulam_spiral_(for_primes)

# [Ulam spiral (for primes)][1]

```ruby
var Imager  = require('Imager');
var ntheory = frequire('ntheory');
 
var n     = (ARGV ? ARGV.shift.to_i : 512);
var start = (ARGV ? ARGV.shift.to_i : 1);
var file  = "ulam.png";
 
func cell(n, x, y, start) {
    y -= (n   >> 1);
    x -= (n-1 >> 1);
    var l = 2*(x.abs > y.abs ? x.abs : y.abs);
    var d = (y > x  ? (l*3 + x + y) : (l - x - y));
    (l-1)**2 + d + start - 1;
}
 
var Imager::Color = 'Imager::Color'.to_caller;
 
var black = Imager::Color.new('#000000');
var white = Imager::Color.new('#FFFFFF');
 
var img = Imager.new(xsize => n, ysize => n, channels => 1);
img.box(filled => 1, color => white);
 
(n-1).range.each { |y|
    (n-1).range.each { |x|
        var v = cell(n, x, y, start);
        ntheory.is_prime(v) && (
            img.setpixel(x => x, y => y, color => black)
        );
    }
}
 
img.write(file => file)
    || die "Cannot write `#{file}': #{img.errstr}";
```