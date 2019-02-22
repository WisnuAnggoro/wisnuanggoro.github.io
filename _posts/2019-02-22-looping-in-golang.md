---
layout: post
title: "Looping in Golang"
date: 2019-02-22
tags: [golang, looping, cpp]
---

In C++, we have three methods to iterate statements; they are `for`, `foreach`, and `while`. Fortunately, there is only one method in Golang to loop lines of code; it's `for` method. However, this `for` method in Golang can be used as `for`, `foreach`, and `while` in C++.

## For loop

Siilar to C++, basic Golang `for` loop has three components separated by semicolons: `ìnitial statement`, `condition expression`, and `post statement`. The difference is, unlike `for` loop in C++, we don't need to add parenthesis in between these three comment. Please see the following code that will print number `0` to `9`:

```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

The `initial statement` and `post statement` are optional, so we can refactor the preceding code as follow:

```go
i := 0
for ; i < 10; {
    fmt.Println(i)
    i++ 
}
```

As the preceding code, we move the `initial statement` outside `for` loop and `post statement` inside `for` loop.

**Note: If we omit the `post statement` from the preceding code, it will run infinitely.**

## While loop

We can refactor preceding code by droping semicolons so the code will be as follow:

```go
i := 0
for i < 10 {
    fmt.Println(i)
    i++ 
}
```

The preceding code is similar to the use of `while` loop in C++.

## Foreach

Another `for` loop in Golang is iteration over `slice` or `map`. It's similar to `foreach` loop in C++. To do so, we use `range` form of `for` loop.

Two values will be returned for each iteration when we apply the `for - range` loop. The first is the `index`, and the second is a copy of the element at that index.

The following code will apply the `for - range` loop to print the `pow` slice value:

```go
var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}
for i, v := range pow {
    fmt.Printf("2**%d = %d\n", i, v)
}
```

---

Source links:<br />
[A Tour of Go - Flow control](https://tour.golang.org/flowcontrol/1)<br />
[A Tour of Go - Range](https://tour.golang.org/moretypes/16)