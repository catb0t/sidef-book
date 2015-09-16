[1]: http://rosettacode.org/wiki/Top_rank_per_group

# [Top rank per group][1]

```ruby
var data = <<'EOF'.lines.map{ (var h = Hash.new)[%w(name id salary dept)] = .split(','); h };
Tyler Bennett,E10297,32000,D101
John Rappl,E21437,47000,D050
George Woltman,E00127,53500,D101
Adam Smith,E63535,18000,D202
Claire Buckman,E39876,27800,D202
David McClellan,E04242,41500,D101
Rich Holcomb,E01234,49500,D202
Nathan Adams,E41298,21900,D050
Richard Potter,E43128,15900,D101
David Motsinger,E27002,19250,D202
Tim Sampair,E03033,27000,D101
Kim Arlich,E10001,57000,D190
Timothy Grove,E16398,29900,D190
EOF
 
var n = (ARGV ? ARGV[0].to_i : "usage: #{__MAIN__} [n]\n".die);
 
data.map { _[:dept] }.uniq.sort.each { |d|
    var es = data.grep { _[:dept] == d }.sort {|a,b|
        b[:salary].to_num <=> a[:salary].to_num
    };
    say d;
    n.times {
        es || break;
        var e = es.shift;
        printf("%-15s | %-6s | %5d\n", e[%w(name id salary)]...);
    };
    print "\n";
};
```

#### Output:
```
$ sidef top_rank.sf 3
D050
John Rappl      | E21437 | 47000
Nathan Adams    | E41298 | 21900

D101
George Woltman  | E00127 | 53500
David McClellan | E04242 | 41500
Tyler Bennett   | E10297 | 32000

D190
Kim Arlich      | E10001 | 57000
Timothy Grove   | E16398 | 29900

D202
Rich Holcomb    | E01234 | 49500
Claire Buckman  | E39876 | 27800
David Motsinger | E27002 | 19250
```