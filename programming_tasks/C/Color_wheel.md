[1]: http://rosettacode.org/wiki/Color_wheel

# [Color wheel][1]

```ruby
require('Imager')
 
var (width, height) = (300, 300)
var center = Complex(width/2 , height/2)
 
var img = %s|Imager|.new(
                      xsize => width,
                      ysize => height,
                     )
 
for y, x in (^height ~X ^width) {
    var vector = (center - x - y.i)
    var magnitude = (vector.abs * 2 / width)
    var direction = ((Num.pi + atan2(vector.real, vector.imag)) / Num.tau)
    img.setpixel(
        x     => x,
        y     => y,
        color => Hash(hsv => [360*direction, magnitude, magnitude < 1 ? 1 : 0])
    )
}
 
img.write(file => 'color_wheel.png')
```