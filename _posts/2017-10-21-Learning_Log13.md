---
layout: post
title:  "Learning Log 13"
date:   2017-10-21
categories: Leetcode OS
image:  /preview.jpg
---

### hash table

generally, we can think it as a mapping from key to value, ideeally, it maps to a unique place to store value. The best scenario is it provides a uniform distribution of hash values

to solve collision, we can use open addressing. It's resolved by probing. Probing includes liearn probing, quadratic probing and double hashing.

- Linear probing
Search: find next available slot
Insert/Delete: iterate through the following slots until find an empty slot or move one back to this slot

Someone implement hash table and it is slow, why? 
- poor hash function
- bad open addressing strategy

Use hash table to store data, but there is much more data than the machine's RAM, how to deal with that? 

### process vs thread

a process is an instance of a computer program that is being executed. It contains the program code and its current activity. Depending on the OS, a process may be made up of multiple threads of execution that execute instructions concurrently.

a thread of execution is the smallest sequence of programmed instructions that can be managed independently by a scheduler, which is typically a prat of the OS.

Each process provides the resources needed to execute a program. A process has a virtual address space, executable code, open handles to system objexts, a security context, a unique process identifier, environment variables, a priority class, minimum and maximum working set sizes and at least one thread of execution. Each process is started with a single thread, often called the primary thread, but can create additional threads from any of its threads. A thread is the entity within a processthat can be scheduled for execution. All threads of a process share its virtual address space and system resources. In addition, each thread maintains exception handlers, a scheduling priotity, thread local storage, a unique thread identifier and a set of structures the system will use to save the thread context until it is scheduled.

Typical difference is:

- processes run in seperated memory while threads run in shared memory
- processes are typically independent while threads exist as a subset of a process
- processes carry considerably more state information than threads, whereas mutiple threads within a process share process state as well as memory and other resources
- processes have seperated address spaces while threads share their address space
- process interact only through system-provided inter-process communication mechanism
- context switching between threads in the same process is typically faster than switching between processes

### IPC vs ITC (Interprocess communication vs Interthread communication)

- IPC: a record stored on disk that can be accessed by mutiple processes

- Socket: a data stream sent over  a network interface, either to difference process on the same computer or to another computer on the network. Typically byte-oriented, sockets rarely preserve message boundaries. Data written through a socket reuqires formating to preserve message boundaries.

- Message Queue: a data stream similar to socket, but which usually preserves message boundaries. Typically implmented by the OS. They allow muitple processes to read and write to the meassage queue without being directly connected to each other.

- Publish/Subscribe Observer

- Pipe: an unidirectional data channel. Data written to the end of pipe is buffered by the OS until it is read from the read end of the pipe. Two-way data streams between processes can be achieved by creating two pipes untilizing standard input and output.

- Shared memory: multiple processes are given access to the same block of memory which creates a shared buffer for the processes to communicate with each other.

- Semaphore: a simple structure that synchronizes multiple processes acting on shared resources.

- ITC: synchronization primitives like locks and semaphores through events like wait, notify. 

Each thread has a private stack which it can quickly add and remove items from. This makes stack based memory fast. But if you use too much stack memory, as occurs in infinite recursion, you will get a stack overflow.

All threads share a common heap. Since all threads share the same heap, access to the allocator/deallocator must be synchronized. There are various methods and libs for avoiding allocator contention.

Some languages allow you to create private pools of memory or inidividual heaps which you can assign to a single thread.

Every thread would be allocated its own memory space in stack while typically there is only one heap within one process. This means heap space is shared among all threads. Since it is global, it is faster in speed. But also, this causes synchronization issues, which could possibly slow the whole system down.

### Memory Management

https://en.wikibooks.org/wiki/Memory_Management/Stacks_and_Heaps

- stack-based

- heap-based

### SOAP (Simple Object Access Protocol) vs REST (Representational State Transfer)

- SOAP is a protocol while REST is an architectural styple. 
- SOAP is highly secure as it defines its own security. REST inherits security measures from the underlying transport.
- SOAP message request is processed slower as compared with REST.
- SOAP supports only XML while REST supports data formats like plain text, XML, HTML and JSON.
- SOAP is commonly used in payment gateways, financial and telecommunication services while REST is commonly used in social media, web chat and mobile services.

If the security is a major concern and the resources are not limited then we should use SOAP web services. Like if we are creating a web service for banking related work then we should go with SOAP as here high security is needed.

On the other hand if security is not a major concern and we have limited resources. Or we want to create an API that will be easily used by other developers publicly then we should go with REST web services.
  

### 256. Paint House

https://leetcode.com/problems/paint-house/discuss/

```python
class Solution(object):
    def minCost(self, costs):
        """
        :type costs: List[List[int]]
        :rtype: int
        """
        prev = [0] * 3
        for now in costs:
            prev = [now[i] + min(prev[:i] + prev[i+1:]) for i in range(3)]
        return min(prev)
```

### 276. Paint Fence

https://leetcode.com/problems/paint-fence/discuss/

```python
class Solution(object):
    def numWays(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: int
        """
        if n == 0:
            return 0
        if n == 1:
            return k
        same, dif = k, k*(k-1)
        for i in range(3, n+1):
            same, dif = dif, (same+dif)*(k-1)
        return same + dif
```

### 91. Decode Ways

https://leetcode.com/problems/decode-ways/description/

```python
class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if s == '': return 0
        n = len(s)
        dp =[0 for i in range(n+1)]
        dp[0] = 1
        dp[1] = 1 if s[0] != '0' else 0
            
        for i in range(2, n+1):
            first = int(s[i-1:i])
            second = int(s[i-2:i])
            if 1 <= first <= 9:
                dp[i] += dp[i-1]
            if 10 <= second <= 26:
                dp[i] += dp[i-2]
        return dp[-1]
```

### 714. Best Time to Buy and Sell Stock with Transaction Fee

https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/description/

```C++
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int size = prices.size();
        vector<int>buy(size+1, INT_MIN);
        vector<int>sell(size+1, 0);
        for(int i = 0; i < size; i++)
        {
            buy[i+1] = max(sell[i] - prices[i], buy[i]);
            sell[i+1] = max(buy[i+1] + prices[i] - fee, sell[i]);
        }
        return sell.back();
    }
};
```

```python
import sys
class Solution:
    def maxProfit(self, prices, fee):
        """
        :type prices: List[int]
        :type fee: int
        :rtype: int
        """
        n = len(prices)
        buy = [-sys.maxsize for i in range(n+1)]
        sell = [0 for i in range(n+1)]
        for i in range(n):
            buy[i+1] = max(sell[i] - prices[i], buy[i])
            sell[i+1] = max(buy[i+1] + prices[i] - fee, sell[i])
        return sell[-1]
```

### 322. Coin Change

https://leetcode.com/problems/coin-change/discuss/

```C++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int Max = amount + 1;
        vector<int> dp(amount + 1, Max);
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            for (int j = 0; j < coins.size(); j++) {
                if (coins[j] <= i) {
                    dp[i] = min(dp[i], dp[i - coins[j]] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
};
```

```python
class Solution(object):
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        """
        dp = [amount+1 for i in range(amount+1)]
        dp[0] = 0
        for i in range(1, amount+1):
            for j in range(len(coins)):
                if coins[j] <= i:
                    dp[i] = min(dp[i], dp[i-coins[j]]+1)
        return -1 if dp[-1] > amount else dp[-1]
```







