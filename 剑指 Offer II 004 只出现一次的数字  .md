[题目描述](https://leetcode-cn.com/problems/WGki4K/)

**思路：**

顺序遍历是肯定的，但如何做到不用额外的空间呢？考虑到题目中强调了“其他每个元素都恰出现三次”，肯定是有用的。

想到先对序列进行排序，然后每 3 个进行检查，那么只出现一次的会恰好在每组的第一个。

**Code:**

```rust
pub fn single_number(mut nums: Vec<i32>) -> i32 {
    nums.sort();
    for mut i in 0..(nums.len()/3) {
        i *= 3;
        if nums[i] == nums[i+1] && nums[i+1] == nums[i+2] {
            continue;
        } else {
            return nums[i]
        }
    }

    nums.last().unwrap().to_owned()
}
```

