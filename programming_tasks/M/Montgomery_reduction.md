[1]: https://rosettacode.org/wiki/Montgomery_reduction

# [Montgomery reduction][1]

```ruby
func montgomeryReduce(m, a) {
    {
        a += m if a.is_odd
        a >>= 1
    } * m.as_bin.len
 
    a % m
}
 
var m  = 750791094644726559640638407699
var t1 = 323165824550862327179367294465482435542970161392400401329100
 
var r1 = 440160025148131680164261562101
var r2 = 435362628198191204145287283255
 
var x1 = 540019781128412936473322405310
var x2 = 515692107665463680305819378593
 
say("Original x1:        ", x1)
say("Recovererd from r1: ", montgomeryReduce(m, r1))
say("Original x2:        ", x2)
say("Recovererd from r2: ", montgomeryReduce(m, r2))
 
print("\nMontgomery computation of x1^x2 mod m:    ")
var prod = montgomeryReduce(m, t1/x1)
var base = montgomeryReduce(m, t1)
 
for (var exponent = x2; exponent ; exponent >>= 1) {
    prod = montgomeryReduce(m, prod * base) if exponent.is_odd
    base = montgomeryReduce(m, base * base)
}
 
say(montgomeryReduce(m, prod))
say("Library-based computation of x1^x2 mod m: ", x1.powmod(x2, m))
```

#### Output:
```
Original x1:        540019781128412936473322405310
Recovererd from r1: 540019781128412936473322405310
Original x2:        515692107665463680305819378593
Recovererd from r2: 515692107665463680305819378593

Montgomery computation of x1^x2 mod m:    151232511393500655853002423778
Library-based computation of x1^x2 mod m: 151232511393500655853002423778
```