[1]: http://rosettacode.org/wiki/Pythagoras_tree

# [Pythagoras tree][1]

```ruby
require('GD::Simple')
 
func tree(img, x1, y1, x2, y2, depth) {
 
    depth <= 0 && return()
 
    var dx = (x2 - x1)
    var dy = (y1 - y2)
 
    var x3 = (x2 - dy)
    var y3 = (y2 - dx)
    var x4 = (x1 - dy)
    var y4 = (y1 - dx)
    var x5 = (x4 + 0.5*(dx - dy))
    var y5 = (y4 - 0.5*(dx + dy))
 
    var square = %s<GD::Polygon>.new
    square.addPt(x1,y1)
    square.addPt(x2,y2)
    square.addPt(x3,y3)
    square.addPt(x4,y4)
 
    var triangle = %s<GD::Polygon>.new
    triangle.addPt(x3, y3)
    triangle.addPt(x4, y4)
    triangle.addPt(x5, y5)
 
    var color = img.colorAllocate(0, 255/depth, 0)
    img.filledPolygon(square, color)
    img.filledPolygon(triangle, color)
 
    tree(img, x4, y4, x5, y5, depth - 1)
    tree(img, x5, y5, x3, y3, depth - 1)
}
 
var (width=1920, height=1080);
var img = %s'GD::Simple'.new(width, height);
tree(img, width/2.3, height, width/1.8, height, 7)
 
var fh = File('pythagoras_tree.png').open('>:raw')
fh.print(img.png)
fh.close
```