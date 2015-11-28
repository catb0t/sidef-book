[1]: http://rosettacode.org/wiki/Find_duplicate_files

# [Find duplicate files][1]

It uses the portable _File::Find_ module which means that it should work, virtually, on any platform.

```ruby
# usage: sidef fdf.sf [size] [dir1] [...]

func find_duplicate_files(Block code, size_min=0, *dirs) {
    var files = Hash.new;
    var f = frequire('File::Find');
    f.find(
        Hash.new(
            no_chdir => 1,
            wanted   => func(arg) {
                var file = File.new(arg);
                file.is_file || return;
                file.is_link && return;
                var size = file.size;
                size >= size_min || return;
                files{size} := [] -> append(file);
            },
        ) => dirs...
    );

    files.values.each { |set|
        set.len > 1 || next;
        var dups = Hash.new;
        0 ..^ set.end-1 -> each { |i|
            for (var j = i+1; j <= set.end; j++) {
                if (set[i].compare(set[j]) == 0) {
                    dups{set[i]} := [] -> append(set.pop_at(j--));
                }
            }
        }
        dups.each{ |k,v| code.call(k.to_file, v...) };
    }

    return;
}

var duplicates = Hash.new;
func collect(*files) {
    duplicates{files[0].size} := [] -> append(files);
}

find_duplicate_files(collect, Num(ARGV.shift \\ 0), ARGV...);

duplicates.keys.sort{ |a,b| b.to_i <=> a.to_i}.each { |key|
    say "=> Size: #{key}\n#{'~'*80}";
    duplicates{key}.each { |files|
        say "#{files.map{.to_s}.sort.join(%Q[\n])}\n#{'-'*80}";
    }
}
```


Section of sample output:


#### Output:
```
% sidef fdf.sf 0 /tmp /usr/bin
=> Size: 5656
~~~~~~~~~~~~~~~~~~~~~~~~~~
/usr/bin/precat
/usr/bin/preunzip
/usr/bin/prezip
--------------------------
=> Size: 2305
~~~~~~~~~~~~~~~~~~~~~~~~~~
/usr/bin/gunzip
/usr/bin/uncompress
--------------------------
=> Size: 2
~~~~~~~~~~~~~~~~~~~~~~~~~~
/tmp/a.txt
/tmp/b.txt
--------------------------
/tmp/m.txt
/tmp/n.txt
--------------------------
```
