[1]: https://rosettacode.org/wiki/Color_quantization

# [Color quantization][1]

```ruby
require('Image::Magick')
 
func quantize_image(n = 16, input, output='output.png') {
    var im = %O<Image::Magick>.new
    im.Read(input)
    im.Quantize(colors => n, dither => 1)    # 1 = None
    im.Write(output)
}
 
quantize_image(input: 'Quantum_frog.png')
```
