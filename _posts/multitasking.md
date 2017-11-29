## Multitasking in Python


### In Python3 (concurrent.futures)

we can use concurrent.futures (https://docs.python.org/dev/library/concurrent.futures.html#threadpoolexecutor) for multi-threading and multi-processing.


## Multi-threading

Note: Thread class was implemented in CPython. Due to the Global Interpreter Lock (GIL), only one thread can execute Python code at once. If you would like to make better use of the computational resources of multi-core machines, you should use multiprocessing or concurrent.futures.ProcessPoolExecutor. However, threading is still an appropriate model if you want to run multiple I/O-bound tasks simultaneously.

### Thread Pool

https://en.wikipedia.org/wiki/Thread_pool

A thread pool is a software design pattern for achieving concurrency of execution in a computer program. A thread pool matains multiple threads waiting for tasks to be allocated for concurrent execution by the supervising program. By maintaining a pool of threads, the model increases performance and avoids latency in execution due to frequent creation and destruction of threads for short-lived tasks. The number of available threads is tuned to the computing resources available to the program, such as parallel processors, cores, memory and network sockets.


### Daemon thread

- If a daemon thread (say B) is created within user thread (say A), then ending of this user/parent thread will NOT end the daemon/child thread.
- When all the non-daemon threads complete, daemon threads terminates automatically.
- If a daemon thread was created from a daemon thread then this is also a daemon thread. 
- Daemon threads are service providers for user threads running in the same process.
