[1]: https://rosettacode.org/wiki/Bilinear_interpolation

# [Bilinear interpolation][1]

```ruby
require('Imager')
 
func scale(img, scaleX, scaleY) {
    var (width, height) = (img.getwidth, img.getheight)
    var (newWidth, newHeight) = (int(width*scaleX), int(height*scaleY))
 
    var out = %O<Imager>.new(xsize => newWidth, ysize => newHeight)
 
    var lerp = { |s, e, t|
        s + t*(e-s)
    }
 
    var blerp = { |c00, c10, c01, c11, tx, ty|
        lerp(lerp(c00, c10, tx), lerp(c01, c11, tx), ty)
    }
 
    for x,y in (^newWidth ~X ^newHeight) {
        var gxf = (x/newWidth  * (width  - 1))
        var gyf = (y/newHeight * (height - 1))
 
        var gx = gxf.int
        var gy = gyf.int
 
        var *c00 = img.getpixel(x => gx,   y => gy  ).rgba
        var *c10 = img.getpixel(x => gx+1, y => gy  ).rgba
        var *c01 = img.getpixel(x => gx,   y => gy+1).rgba
        var *c11 = img.getpixel(x => gx+1, y => gy+1).rgba
 
        var rgb = 3.of { |i|
            blerp(c00[i], c10[i], c01[i], c11[i], gxf - gx, gyf - gy).int
        }
 
        out.setpixel(x => x, y => y, color => rgb)
    }
 
    return out
}
 
var img = %O<Imager>.new(file => "input.png")
var out = scale(img, 1.6, 1.6)
out.write(file => "output.png")
```