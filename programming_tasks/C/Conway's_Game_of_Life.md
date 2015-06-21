[1]: http://rosettacode.org/wiki/Conway's_Game_of_Life

# [Conway's Game of Life][1]

```ruby
var w = `tput cols`.to_i-1;
var h = `tput lines`.to_i-1;
var r = "\033[H";
 
var dirs = [[-1,-1], [-1, 0], [-1, 1], [ 0,-1],
            [ 0, 1], [ 1,-1], [ 1, 0], [ 1, 1]];
 
var universe = h.of { w.of {1.rand < 0.1} };
 
func iterate {
    var new = h.of { w.of(false) };
    0...(h-1).each { |i|
        0...(w-1).each { |j|
        var neighbor = 0;
        dirs.each { |dir|
            var y = dir[0]+i;
            var x = dir[1]+j;
            neighbor += (universe[y % h][x % w] ? 1 : 0);
            neighbor > 3 && break;
        };
 
        new[i][j] = (universe[i][j]
                        ? (neighbor ~~ [2,3])
                        : (neighbor ==    3));
       };
    };
    universe = new;
};
 
loop {
    print r;
    say universe.map{|row| row.map{|cell| cell ? '#' : ' '}.join('')}.join("\n");
    iterate();
}
```