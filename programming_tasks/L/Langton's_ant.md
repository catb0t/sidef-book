[1]: http://rosettacode.org/wiki/Langton's_ant

# [Langton's ant][1]

```ruby
const dirs = [[1,0], [0,-1], [-1,0], [0,1]];
const size = 100;
 
enum |White, Black|;
 
var plane = [];
{|i| plane[i-1] = [White]*size} * size;
 
var (x, y) = ([size/2 int] * 2 ...);
var dir = dirs.len.rand.int;
 
var moves = 0;
loop {
    (x >= 0) && (y >= 0) && (x < size) && (y < size) || break;
 
    given(plane[x][y])
        when (White) { dir--; plane[x][y] = Black }
        when (Black) { dir++; plane[x][y] = White };
 
    moves++;
    [\x, \y]:dirs[dir %= dirs.len] each {|a,b| *a += b };
}
 
say "Out of bounds after #{moves} moves at (#{x}, #{y})";
plane.map{.map {|square| square == Black ? '#' : '.' }}.each{.join.say};
```