[1]: https://rosettacode.org/wiki/Sunflower_fractal

# [Sunflower fractal][1]

```ruby
require('Imager')
 
func draw_sunflower(seeds=3000) {
    var img = %O<Imager>.new(
        xsize => 400,
        ysize => 400,
    )
 
    var c = (sqrt(1.25) + 0.5)
    { |i|
        var r = (i**c / seeds)
        var θ = (2 * Num.pi * c * i)
        var x = (r * sin(θ) + 200)
        var y = (r * cos(θ) + 200)
        img.circle(x => x, y => y, r => i/(5*seeds))
    } * seeds
 
    return img
}
 
var img = draw_sunflower()
img.write(file => "sunflower.png")
```


[Sunflower fractal](https://github.com/trizen/rc/blob/master/img/sunflower-sidef.png)