---
layout: post
title:  "Learning Log 14"
date:   2017-10-24
categories: Leetcode OS Multitasking_in_C++ MapReduce
image:  /preview.jpg
---

### Process vs. Threads

- multi-processing: 
  - interprocess communication, e.g. message queue
- multi-threading:
  - communicate through shared memory
  - pros: fast to start, low overhead, communication is faster
  - cons: difficult to implement, can't run on distributed system

### thread management
- passing parameter: 
  - copy parameter values directly into functions, but will use unnecessary memory;
  - pass reference, but will let threads use shared memory;
  - use move() function to pass parameter
- thread can not be copied
- to transfer ownership of threads:
  - use move function
- how many threads should be created?
  - to solve a complicated task, we should consider creating as many threads as possible, but within the capacity of available CPU resources. Otherwise, an oversubscription problem will occur.
  - we can use ```std::thread::hardware_concurrency();``` to get an indication of how many threads should be created (number of CPU cores).

### functors

### data race and Mutex
- multiple threads are running, every one competes for the resource. 
- to solve this problem, use Mutex to synchronize the threads. While one thread is using a certain thread, the resources will be locked to prevent other thread from accessing it. Once the occupying thread finishes its job, the resource will be unlocked.
- use of mutex lock and unlock function is not recommended. If we used the lock function and certain task goes wrong, the resource will stay locked forever. To avoid this, we should use guard function. So when the program encounters error, the resource will be released.

### deadlock
- If we have two mutex for multiple threads, the program might end up in the situation that one thread has locked one resource while the other thread lock another resource. Each of them is waiting the other to release the resource.
- To avoid this, we should make sure every thread locks resources in the same order
- Or, we can use C++ standard lock function: ```std:lock(_mu, _mu2)```
- 1, always try to lock a single mutex;
- 2, 
- 3, use the standard lock function for multiple mutex;
- 4, try to lock mutex in the same order

### unique_lock and lazy initialization
- a more fine-grained lock mechanism



### MapReduce


### 300. Longest Increasing Subsequence

https://leetcode.com/problems/longest-increasing-subsequence/description/

```python
## 1st solution, DP:
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        if n <= 1: return n
        t = [1 for i in range(n)]
        for i in range(1, n):
            for j in range(0, i):
                if nums[j] < nums[i]:
                    if t[j] + 1 > t[i]:
                        t[i] = t[j] + 1
        return max(t)

## 2nd solution
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        tails = [0] * len(nums)
        size = 0
        for x in nums:
            i, j = 0, size
            while i != j:
                m = (i + j) / 2
                if tails[m] < x:
                    i = m + 1
                else:
                    j = m
            tails[i] = x
            size = max(i + 1, size)
        return size
```





