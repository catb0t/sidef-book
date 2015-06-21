[1]: http://rosettacode.org/wiki/Find_common_directory_path

# [Find common directory path][1]

```ruby
var dirs = %w(
    /home/user1/tmp/coverage/test
    /home/user1/tmp/covert/operator
    /home/user1/tmp/coven/members
);
 
var unique_pref = dirs.map{.split('/')}.abbrev.min_by{.len};
var common_dir  = unique_pref.pop:.join('/');
say common_dir;   # => /home/user1/tmp
```