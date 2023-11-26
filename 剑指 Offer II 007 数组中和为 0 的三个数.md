[题目描述](https://leetcode-cn.com/problems/1fGaJU/)

**思路：**

想到之前做的 two_sum 问题，先将序列排序，然后每次选取一个元素作为 two_sum 的 target，这样就可以得到一个满足的三元组。

需要注意的是一些重复元素的跳过。

**Code:**

```rust
pub fn three_sum(mut nums: Vec<i32>) -> Vec<Vec<i32>> {
    let mut res = Vec::new();
    if nums.len() <= 2 {
        return res;
    }
    nums.sort();
    for i in 0..nums.len() - 2 {
        if nums[i] > 0 {
            break;
        }

        if i != 0 && nums[i] == nums[i - 1] {
            continue;
        }

        two_sum(&nums[i + 1..], -nums[i])
            .into_iter()
            .map(|mut v| {
                v.push(nums[i]);
                res.push(v);
            })
            .count();
    }

    res
}

fn two_sum(nums: &[i32], target: i32) -> Vec<Vec<i32>> {
    let mut i = 0;
    let mut j = nums.len() - 1;
    let mut sum = 0;
    let mut res = Vec::new();

    loop {
        if i >= j {
            break;
        }

        sum = nums[i] + nums[j];
        if sum == target {
            res.push(vec![nums[i], nums[j]]);
            // Skip same
            while i < j && nums[i] == nums[i + 1] {
                i += 1;
            }
            // Skip same
            while i < j && nums[j] == nums[j - 1] {
                j -= 1;
            }

            i += 1;
            j -= 1;
        } else if sum > target {
            j -= 1;
        } else {
            i += 1;
        }
    }

    res
}
```

