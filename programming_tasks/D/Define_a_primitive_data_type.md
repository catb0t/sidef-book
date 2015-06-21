[1]: http://rosettacode.org/wiki/Define_a_primitive_data_type

# [Define a primitive data type][1]

```ruby
class MyInt(value) {
 
    def min = 1;
    def max = 10;
 
    method new(value is Number) {
        (value > max) || (value < min) && (
            die "Invalid value '#{value}': must be between #{min} and #{max}";
        );
        !value.is_int && (
            die "Invalid value '#{value}': must be an integer";
        );
    }
 
    method new(value) {
        die "Invalid value '#{value}'; expected a number";
    }
 
    method get_value {
        value.get_value.get_value;
    }
 
    method AUTOLOAD(name, *args) {
        var result = value.(name)(args...);
 
        result.is_a(Number) &&
            return MyInt(result.int);
 
        result;
    }
}
 
#
## Tests:
#
var a = MyInt(2);    # creates a new object of type `MyInt`
a += 7;              # adds 7 to a
say a;               # => 9
say a/2;             # => 4
 
var b = (a - 3);     # b is of type `MyInt`
say b;               # => 6
 
say a.to_hex;        # => "0x9" -- an hexadecimal string
 
a -= 7;              # a=2
say (a + b);         # => 8 -- the result of (2 + 6)
 
a += 4;              # a=6
say a+b;             # error: Invalid value '12'; must be between 1 and 10
```