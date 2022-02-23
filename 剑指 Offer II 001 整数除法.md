[题目描述](https://leetcode-cn.com/problems/xoh6Oh/)

思路：模拟体系上讲到的 CPU 除法原理进行计算 [Reference](https://yinwhe.notion.site/02-ALU-0d602345fb6645aa84ba1b91d0e3b28d)

Code:

```rust
fn divide(a: i32, b: i32) -> i32 {
    let postive_flag = (a > 0 && b > 0) || (a < 0 && b < 0);

    let mut a = (a as i64).abs();
    let mut b = (b as i64).abs();
    let mut res = 0i64;

    for i in 0..=31 {
        let temp = b << (31 - i);
        if a >= temp {
            a -= temp;
            res |= 1;
        }
        res <<= 1;
    }
    res >>= 1;

    if postive_flag {
        (i32::MAX as u32).min(res as u32) as i32
    } else {
        - (res as i32)
    }
}
```

