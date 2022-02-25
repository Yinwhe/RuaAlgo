[题目描述](https://leetcode-cn.com/problems/aseY1I/)

**思路：**

这题整体思路很明晰，双层遍历就行（似乎在遍历上没有更好的思路了），优化点在如何判断两个字符串是否有重合。

题目中强调了字符都是小写的（肯定有用啦），考虑使用 位优化 来记录字符串中每个字符。

**Code:**

```rust
pub fn max_product(words: Vec<String>) -> i32 {
    let mut max_product = 0;
    let mut bits = vec![0; words.len()];

    words
        .iter()
        .enumerate()
        .map(|(i, word)| {
            word.chars()
                .map(|c| bits[i] |= 1 << (c as i32 - 'a' as i32))
                .count();
        })
        .count();

    for i in 0..words.len() {
        for j in i + 1..words.len() {
            if bits[i] & bits[j] == 0 {
                max_product = max_product.max((words[i].len() * words[j].len()) as i32);
            }
        }
    }

    max_product
}

```

