[1]: http://rosettacode.org/wiki/Sleep

# [Sleep][1]

```ruby
var sec = read(Number);       # any positive number (it may be fractional)
say "Sleeping...";
Sys.sleep(sec);               # in seconds
#Sys.usleep(sec);             # in microseconds
#Sys.nanosleep(sec);          # in nanoseconds
say "Awake!";
```