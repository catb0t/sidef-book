[1]: http://rosettacode.org/wiki/Vector_products

# [Vector products][1]

```ruby
class Vector(x, y, z) {
    method ∙(vec) {
        self[:x..:z] »*« vec[:x..:z] [+];
    }
 
    method ⨉(vec) {
        Vector(self[:y]*vec[:z] - self[:z]*vec[:y],
               self[:z]*vec[:x] - self[:x]*vec[:z],
               self[:x]*vec[:y] - self[:y]*vec[:x]);
    }
 
    method to_s {
        "(#{self[:x]}, #{self[:y]}, #{self[:z]})";
    }
};
 
var a = Vector(3, 4, 5);
var b = Vector(4, 3, 5);
var c = Vector(-5, -12, -13);
 
say "a=#{a}; b=#{b}; c=#{c};";
say "a ∙ b = #{a ∙ b}";
say "a ⨉ b = #{a ⨉ b}";
say "a ∙ (b ⨉ c) = #{a ∙ (b ⨉ c)}";
say "a ⨉ (b ⨉ c) = #{a ⨉ (b ⨉ c)}";
```

#### Output:
```
a=(3, 4, 5); b=(4, 3, 5); c=(-5, -12, -13);
a ∙ b = 49
a ⨉ b = (5, 5, -7)
a ∙ (b ⨉ c) = 6
a ⨉ (b ⨉ c) = (-267, 204, -3)
```