[1]: http://rosettacode.org/wiki/Bulls_and_cows

# [Bulls and cows][1]

```ruby
var size = 4;
var num = (1..9 shuffle.ft(0, size-1));
 
for (var guesses = 0; true; guesses++) {
 
    var bulls = 0;
    var cows  = 0;
 
    var input = (
                  Sys.scanln("Input: ").split(1)
                                       .unique
                                       .grep {.~~/^[1-9]$/}
                                       .map  {.to_i}
                );
 
    input.len == size || (
        "Invalid input!\n".warn;
        guesses--;
        next;
    );
 
    if (input == num) {
        "You did it in %d attempts!\n".printf(guesses);
        break;
    }
 
    num.range.each { |i|
        if (num[i] == input[i]) {
            bulls++;
        }
        elsif (num.contains(input[i])) {
            cows++;
        }
    }
 
    "Bulls: %d; Cows: %d\n".printf(bulls, cows);
}
```