[1]: http://rosettacode.org/wiki/Forest_fire

# [Forest fire][1]

```ruby
var w = `tput cols`.to_i-1;
var h = `tput lines`.to_i-1;
var r = "\033[H";
 
const (
    red    = "\033[31m",
    green  = "\033[32m",
    yellow = "\033[33m",
);
 
var tree_prob = 0.05;
var burn_prob = 0.0002;
 
enum |Empty, Tree, Heating, Burning|;
 
const dirs = [
    %n(-1 -1), %n(-1 0), %n(-1 1), %n(0 -1),
    %n(0   1), %n(1 -1), %n(1  0), %n(1  1),
];
 
var chars = [' ', green+'*', yellow+'&', red+'&'];
var forest = h.of { w.of { 1.rand < tree_prob ? Tree : Empty } };
 
func iterate {
    var new = h.of{ w.of(0) };
    range(0, h-1).each { |i|
        range(0, w-1).each { |j|
            given(new[i][j] = forest[i][j])
                when(Tree) {
                    1.rand < burn_prob && (new[i][j] = Heating; next);
                    dirs.each { |pair|
                        var y = pair[0]+i;
                        y ~~ range(0, h-1) || next;
                        var x = pair[1]+j;
                        x ~~ range(0, w-1) || next;
                        forest[y][x] == Heating && (new[i][j] = Heating; break);
                    }
                }
                when(Heating)            { new[i][j] = Burning; next }
                when(Burning)            { new[i][j] = Empty         }
                case(1.rand < tree_prob) { new[i][j] = Tree          };
        }
    };
    forest = new;
}
 
func init_forest {
    print r;
    forest.each { |row|
        print chars[row].join;
        print "\033[E\033[1G";
    };
    iterate();
}
 
loop { init_forest() };
```