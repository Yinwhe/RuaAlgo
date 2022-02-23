[题目描述](https://leetcode-cn.com/study-plan/lcof/?progress=wgfwcn1)

思路：对原来的字符串逆序后，逐位进行计算即可

Code:

```rust
pub fn add_binary(a: String, b: String) -> String {
    let mut a_iter = a.chars().rev();
    let mut b_iter = b.chars().rev();

    let mut carry = 0u32;
    let mut res = String::new();

    for _ in 0..a.len().max(b.len()) {
        let x = a_iter.next().unwrap_or('0').to_digit(10).unwrap();
        let y = b_iter.next().unwrap_or('0').to_digit(10).unwrap();

        match x + y + carry {
            0 => res.push('0'),
            1 => {
                res.push('1');
                carry = 0;
            }
            2 => {
                res.push('0');
                carry = 1;
            }
            3 => {
                res.push('1');
                carry = 1;
            }
            _ => unreachable!(),
        }
    }
    if carry == 1 {
        res.push('1');
    }

    res.chars().rev().collect::<String>()
}
```

