[1]: http://rosettacode.org/wiki/Mandelbrot_set

# [Mandelbrot set][1]

```ruby
__USE_FASTNUM__
 
func mandelbrot(z) {
    var c = z;
    {   z = (z*z + c);
        z.abs > 2 && return true;
    } * 20;
    return false;
}
 
1 ^.. (-1, 0.05) each { |y|
    -2 ..^ (0.5, 0.0315) each { |x|
        print(mandelbrot(y.i + x) ? ' ' : '#');
    };
    print "\n";
}
```