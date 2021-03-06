[1]: https://rosettacode.org/wiki/Brownian_tree

# [Brownian tree][1]

```ruby
const size = 100
const mid = size>>1
const particlenum = 1000
 
var map = []
var spawnradius = 5
 
func set(x, y) {
    map[x][y] = 1
}
 
func get(x, y) {
    map[x][y] \\ 0
}
 
set(mid, mid)
 
var blocks = [
    " ",
    "\N{UPPER HALF BLOCK}",
    "\N{LOWER HALF BLOCK}",
    "\N{FULL BLOCK}"
]
 
func block(a, b) {
    blocks[2*b + a]
}
 
func display {
    0..size `by` 2 -> map {|y|
        0..size -> map {|x|
            if ([x, y].all { .-mid < spawnradius }) {
                block(get(x, y), get(x, y+1))
            } else { " " }
        }.join
    }.join("\n").say
}
 
for progress in (^particlenum) {
    var (x=0, y=0)
 
    var reset = {
        do {
            (x, y) = (
                (mid-spawnradius .. mid+spawnradius  -> pick),
                [mid-spawnradius,   mid+spawnradius] -> pick
            )
            (x, y) = (y, x) if (1.rand < 0.5)
        } while(get(x, y))
    }
 
    reset.run
 
    while ([[-1, 0, 1]]*2 -> cartesian.any {|pair|
        get(x+pair[0], y+pair[1])
    } -> not) {
        x = [x-1, x, x+1].pick
        y = [y-1, y, y+1].pick
 
        if (1.rand < 0.25) {
            x = (x >= mid ? (x-1) : (x+1))
            y = (y >= mid ? (y-1) : (y+1))
        }
 
        if ([x,y].any { .-mid > spawnradius }) {
            reset.run
        }
    }
 
    set(x, y)
    display() if (progress %% 50)
 
    if ((spawnradius < mid) && [x,y].any { .-mid > spawnradius-5 }) {
        ++spawnradius
    }
}
 
display()
```

#### Output:
```
                                 ▄               ▄▀          ▄  ▀▄                                   
                         ▀█▄▄▀ █  █▄█▀        ▄  █▄          ▀▄█ █                                   
                        ▄▀  ▀▄█      █       ▄▀ ▄▀   █ ▄    ▄▀  ▀ ▀  ▄ ▄▀                            
                              ▀▀▄  ▄▀        █▄▀█     ▀█ ▄ ▄▀        ▄█▄▄                            
                              ▄▄▄▀ ▄▀      ▀▀ ▀  ▀▄   ▀▄▀ ▀        ▀▀▄▀  ▀                           
                             ▄▀ ▀▄▀▄           ▄ ▄▄▀   █▄▄     ▄ ▄  █                                
                                    █▄         ▄▀█     █  ▄  █▀ ▀▄█▀                                 
                                 ██▀ ▄▀▄▄▀▄   ▀▀█      ▄▀█  █   ▀                                    
                  ▀▄ ▀▄     ▀▀█          ▀▄  ▄▄▄ █▀     ▀▄▀▀                                         
                ▄ █▄▄▄▀     █▄▄▀     ▄▀▀▄ █▄▀▄ ▄▀▀▄  ▀▄▄█      ▄  ▄                                  
                ▀▀█▄▀          ▀▄▄     ▀▄▀  ██▄ ▀▄▀    █▀▄▄ ▄▄█ ▀▀                                   
               ▀▄▀▄█ ▄ ▄▀  ▄█    ▀█▀▄     ▄▀ ▄▀▄▀ █▀ █▀▀ ▄ ▄▀                                        
               ▄█  ▄▀▀▀▄ ▄ ▀▄ █ ▄  █        ▄ ▀█▀▄▀  █ ▄▄█▀▀      ▀▄▀                                
                     ▀█▄▀▀▄▀▄  ▀▄▄▀▀  ▄▄    ▀▄▀ ▀▄ ▄█▀█   ▀▄  ▄ ▄▄▀                                  
                   ▄▄▀  ▀    █▄  ▀▀▄▀ ▄█   █      ▀▄▄ ▄       ▄█  ▀▄▀      █                         
                 ▄    ▄  ▄▄▀▄▀ ▄ ▄▄▄█  ▄█ ▄▀      █▀██▀▄ ▄▀ ▄▀  ▄▄  ▀▀   ▄▀  ▄                       
            ▄▄▄▄▀     ▀▄     ▀▀▄   ▀ ▀▀▄ ▀ ▀█▀ ▀█▄▀  ▄   ▄▀▀   █▄▄     ▄▄▀▄▄▀    ▄▀                  
                ▀▄▄▄ █▀ ▀▀▄█    ▀▄▀▄▄ ▀▄▄▄  ▄█   ▀█▀▀▄▄ █    ▄▀▄▄ ▄▄  ▄▀        ▄▀                   
              ▀▄▀  ▄▀   ▄▄▄▄▀▄▄▄▄ ██▄  ▄▄▀▄▀▄▄▀ ▄▀ ▄▄▄▀▄▄█▄▄▀▀   █ ▄▄▀▄█▄    ▄ █▄▄▄                  
          ▀▄ █▀     ▀█▄▀ █▄▀ ▀▀ ▀█▄▀ ▀▄▄█▀ ▀▄▀█▄▄▀▀▄ ▀   ▄█▄█▀█   ▀   █ ▀█▄▀▀▄▀▀ ▄▀                  
           ▀▀       ▀ ▄  ▀▄▀     ▀▄ ▄▄▀ ▀ ▄▀  ▀  ▀▄        ▄▀  ▀▄ ▄     ▀ █▄▄                        
                   ▄▄█ ▀█▀     ▄  ▄▀█ ▀  █      ██ ▄▀     ▀▄▀ ▄▀▄▀▄▀█      ▀ ▀                       
                 ▀▀   █    ▄   ▀█▀ █   ▄▀   ▄▄█▀ ▀▀▄        ▀  █   ▄▀▄  ▄                            
              ▀▀▄▄          ▀▄ █     ▄▀▄   █   ▀█▄█ ▀▄▄▀▄▄      ▀ ▀   ▀▀▄                            
                 ▄█▄   ▀▄▀▄▄ ▄▀▀      ▀ ▀▄ ▄▀   ▄▀▄    █ █▄  ▄▀                                      
                   ▄▀▄█▀ █ █▀█           ▄    ▄▀ ▀▄▀      ▄█▀ █▄▄▀▀▄                                 
          ▄   ▄▀▄▄█     ▀▄   ▄▀▄        ▀ ▀▀▄▀   █       ▀ ▄█ ▀▄▀▄  █                                
           ▀▄▀  ▀▀█     █▄▄ ▀  ▄▀         █▀    ▀ ▀▄▀▀▄▄▀  █  ▄▀  ▀▄ ▀▄                              
          ▀▀       ▀   ██▀ ▀▄ ▄█       ▄▄▀▄▀      █▀                ▀                                
                     ▄▀  █   ▀▄         ▄▀   ▀▄ ▄█ ▀▀                                                
                    ▀▄  ▀█▄          ▄▄▀▄   ▄▀▀▀▄▄▄                                                  
                      ▀    ▀            ▀       ▄▀ █▀  ▄                                             
                                                  ▄▄▀█▄▀▄                                            
                                                ▄▀▄   █  ▀                                           
                                              ▄▀▄▄▄▀                                                 
                                             ▀   █ █                                                 
                                                 ▀█                                                  
```