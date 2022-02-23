[题目描述](https://leetcode-cn.com/problems/w3tCBm/)

思路：巧了，rust 有自带的方法 `count_ones`，直接写的话，考虑一个奇数 i 比 i/2 肯定多一个 1，偶数 i 则与 i/2 有一样的 1。

Code:

```rust
pub fn count_bits(n: i32) -> Vec<i32> {
  let mut res = vec![];
  for i in 0..=n {
    res.push(i.count_ones() as i32)
  }

  res
}
// Or
pub fn count_bits(n: i32) -> Vec<i32> {
    let mut res = vec![0];
    res.reserve(n as usize);
    for i in 1..=n {
        res.push(res[(i/2) as usize] + i % 2);
    }
    
    res
}
```

