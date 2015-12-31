[1]: http://rosettacode.org/wiki/Forest_fire

# [Forest fire][1]

```ruby
define w = `tput cols`.to_i-1;
define h = `tput lines`.to_i-1;
define r = "\033[H";

define red = "\033[31m";
define green = "\033[32m";
define yellow = "\033[33m";

define chars = [' ', green+'*', yellow+'&', red+'&'];

define tree_prob = 0.05;
define burn_prob = 0.0002;

enum |Empty, Tree, Heating, Burning|;

define dirs = [
    %n(-1 -1), %n(-1 0), %n(-1 1), %n(0 -1),
    %n(0   1), %n(1 -1), %n(1  0), %n(1  1),
];

var forest = h.of { w.of { 1.rand < tree_prob ? Tree : Empty } };

var range_h = (0 ... h-1);
var range_w = (0 ... w-1);

func iterate {
    var new = h.of{ w.of(0) };
    range_h.each { |i|
        range_w.each { |j|
            given (new[i][j] = forest[i][j]) {
              when (Tree) {
                1.rand < burn_prob && (new[i][j] = Heating; next);
                dirs.each { |pair|
                    var y = pair[0]+i;
                    range_h.contains(y) || next;
                    var x = pair[1]+j;
                    range_w.contains(x) || next;
                    forest[y][x] == Heating && (new[i][j] = Heating; break);
                }
              }
              when (Heating)            { new[i][j] = Burning }
              when (Burning)            { new[i][j] = Empty   }
              case (1.rand < tree_prob) { new[i][j] = Tree    }
            }
        }
    }
    forest = new;
}

func init_forest {
    print r;
    forest.each { |row|
        print chars.@[row];
        print "\033[E\033[1G";
    }
    iterate();
}

loop { init_forest() }
```


OO approach:

```ruby
define RED = "\e[1;31m";
define YELLOW = "\e[1;33m";
define GREEN = "\e[1;32m";
 
define DIRS = [
    [-1, -1], [0, -1], [1, -1],
    [-1,  0],          [1,  0],
    [-1,  1], [0,  1], [1,  1],
]
 
enum (Empty, Tree, Heating, Burning);
define pix = [' ', GREEN + "*", YELLOW + "*", RED + "*"];
 
class Forest(p=0.01, f=0.001, height, width) {
 
    has coords = [];
    has spot = [];
    has neighbors = [];
 
    method init {
        coords = (0..height ~X 0..width)
        spot = height.of { width.of { [true, false].pick ? Tree : Empty } }
        self.init_neighbors
    }
 
    method init_neighbors {
        for pair in coords {
            var(i, j) = @pair;
            neighbors[i][j] = gather {
                for dir in DIRS {
                    take(\(spot[i + dir[0]][j + dir[1]] \\ next));
                 }
            }
        }
    }
 
    method step {
        var heat = [];
 
        for pair in coords {
            var(i, j) = @pair;
            given (spot[i][j]) {
                when Empty   { spot[i][j] = Tree    if (1.rand < p) }
                when Tree    { spot[i][j] = Heating if (1.rand < f) }
                when Heating { spot[i][j] = Burning; heat << [i, j] }
                when Burning { spot[i][j] = Empty }
            }
        }
 
        for pair in heat {
            var(i, j) = @pair;
            neighbors[i][j].each { |ref|
                *ref = Heating if (*ref == Tree);
            }
        }
    }
 
    method show {
        range(0, height-1).each { |i|
            say pix.@[spot[i]];
        }
    }
}
 
local $| = 1;
var(height, width) = `stty size`.nums...;
 
var forest = Forest(height: height, width: width);
print "\e[2J";
loop {
    print "\e[H";
    forest.show;
    forest.step;
}
```
