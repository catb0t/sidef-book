[1]: http://rosettacode.org/wiki/Monty_Hall_problem

# [Monty Hall problem][1]

```ruby
var n = 1000;                                 # number of times to play
var switchWins = (var stayWins = 0);          # sum of each strategy's wins
 
n.times {                                     # play the game n times
   var prize = 3.rand.int;
   var chosen = 3.rand.int;
 
   var show;
   { show = 3.rand.int }
     do while {show ~~ [chosen, prize]};
 
   given(chosen)
     when (prize)                 { stayWins   += 1 }
     when (3 - show - prize)      { switchWins += 1 }
     default                      { die "~ error ~" };
}
 
say ("Staying wins %.2f%% of the time."   % (100.0 * stayWins   / n));
say ("Switching wins %.2f%% of the time." % (100.0 * switchWins / n));
```

#### Output:
```
Staying wins 34.80% of the time.
Switching wins 65.20% of the time.
```