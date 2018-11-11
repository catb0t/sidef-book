# Multidimensional arrays

Multidimensional arrays can be defined as:

```ruby
var A = [
          [1, 2],
          [3, 4],
          [5, 6],
          [7, 8],
        ]

var B = [
          [1, 2, 3],
          [4, 5, 6],
        ]
```

Starting with version 3.06, Sidef provides the `Array.wise_op()` method, which takes two arbitrary nested arrays and an operator, folding each element (entrywise) with the provided operator, which is also available as `a ~Wop b`:


```ruby
say ([1,2,[3,[4]]] ~W+ [42,43,[44,[45]]])       #=> [43, 45, [47, [49]]]
```

Alternatively:

```ruby
say wise_op([1,2,[3,[4]]], '+', [42,43,[44,[45]]])   #=> [43, 45, [47, [49]]]
```

Scalar operations:

```ruby
A `scalar_add` 42   # scalar addition       (aliased as `sadd`)
A `scalar_sub` 42   # scalar subtraction    (aliased as `ssub`)
A `scalar_mul` 42   # scalar multiplication (aliased as `smul`)
A `scalar_div` 42   # scalar division       (aliased as `sdiv`)
```

This methods are provided by `Array.scalar_op()`, which, just like `Array.wise_op()`, also supports arbitrary nested arrays:

```ruby
say ([1,2,[3,[4]]] ~S+ 42)   #=> [43, 44, [45,  [46]]]
say ([1,2,[3,[4]]] ~S* 42)   #=> [42, 84, [126, [168]]]
```

...which is equivalent with:

```ruby
say scalar_op([1,2,[3,[4]]], '+', 42)  #=> [43, 44, [45,  [46]]]
say scalar_op([1,2,[3,[4]]], '*', 42)  #=> [42, 84, [126, [168]]]
```

## Iteration over 2D arrays

The extended `for-in` loop, introduced in Sidef 2.23, provides support for iterating over a 2D-array, which is useful in combination with the cross and zip metaoperators:

```ruby
for a,b in ([1,2] ~X [3,4]) {
    say "#{a} #{b}"
}
```

This is equivalent with:

```ruby
[[1,2], [3,4]].cartesian {|a,b|
    say "#{a} #{b}"
}
```

and outputs:

```text
1 3
1 4
2 3
2 4
```

# Matrix

The `Matrix` built-in class (which is a child of the `Array` class), provides support for defining and working with matrices:

```ruby
Matrix(
    [1, 2],
    [3, 4],
)
```

## Operations

A subset of `Matrix` operations are included in the following example:

```ruby
var A = Matrix(
    [2, -3,  1],
    [1, -2, -2],
    [3, -4,  1],
)

var B = Matrix(
    [9, -3, -2],
    [3, -1,  7],
    [2, -4, -8],
)

say (A + B)     # matrix addition
say (A - B)     # matrix subtraction
say (A * B)     # matrix multiplication
say (A / B)     # matrix division

say (A + 42)    # matrix-scalar addition
say (A - 42)    # matrix-scalar subtraction
say (A * 42)    # matrix-scalar multiplication
say (A / 42)    # matrix-scalar division

say A**20       # matrix exponentation
say A**-1       # matrix inverse: A^-1
say A**-2       # (A^2)^-1

say B.det             # matrix determinant
say B.solve([1,2,3])  # solve a system of linear equations
```
