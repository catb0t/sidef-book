[1]: http://rosettacode.org/wiki/Read_a_specific_line_from_a_file

# [Read a specific line from a file][1]

```ruby
func getNthLine(filename, n) {
  var file = File.new(filename);
  file.open_r.each { |line|
     $. == n && return line;
  };
  Sys.warn("file #{file} does not have #{n} lines, only #{$.}\n");
  return nil;
}
 
var wantedLine = getNthLine("/etc/passwd", 7);
wantedLine != nil && print wantedLine;
```