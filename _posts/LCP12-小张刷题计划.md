---
title: LCP12.小张刷题计划
date: 2020-06-19 21:40:19
tags: 算法
---

### 题干在此

![](https://i.loli.net/2020/06/19/5kcyxPC1EOoRwUm.png)

### 解题思路

这道题我没想出来思路。给出一个用例，我能用脑子直接算出来，但是的确写不出方法。

而且没有找到js的解题思路，看得c++的代码才明白思路，而且真的很精妙，再给我时间也是想不出来解法，有点挫败感。

但是有机会留下来这道题的第一个js解题思路，还是比较开心的。

```js
var minTime = function(time, m) {
    if(time.length <= m) { return 0 }
    let l = 0
    let r = Number.MAX_VALUE
    while(l < r) {
        let mid = Math.floor(l + (r - l) / 2)
        if(canS(time, m, mid)) {
            r = mid
        } else {
            l = mid + 1
        }
    }
    return r
};

var canS = function(time, m, mid) {
    let sum = 0
    let count = 0
    let maxt = 0
    for( let t of time) {
        sum = sum + t
        maxt = Math.max(maxt, t)
        if(sum - maxt > mid) {
            if( ++count == m) { return false }
            sum = t
            maxt = t
        }
    }
    return true
}
```

### 总结

加油吧，要学的还是很多。