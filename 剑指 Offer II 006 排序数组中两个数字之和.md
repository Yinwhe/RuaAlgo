[题目描述](https://leetcode-cn.com/problems/kLl5u1/)

**思路：**

采用双指针，如果两数之和大于目标值，则缩减右指针，否则增加左指针。

**Code:**

```rust
pub fn two_sum(numbers: Vec<i32>, target: i32) -> Vec<i32> {
    let mut sum = 0;
    let mut i = 0;
    let mut j = numbers.len() - 1;
    loop {
        sum = numbers[i] + numbers[j];
        if sum == target {
            return vec![i as i32, j as i32];
        }

        if sum > target {
            j -= 1;
        } else {
            i += 1;
        }
    }
}
```

