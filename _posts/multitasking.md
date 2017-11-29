## Multitasking in Python


### In Python3 (concurrent.futures)

we can use concurrent.futures (https://docs.python.org/dev/library/concurrent.futures.html#threadpoolexecutor) for multi-threading and multi-processing.


## Multi-threading

https://docs.python.org/3.5/library/threading.html

Note: Thread class was implemented in CPython. Due to the Global Interpreter Lock (GIL), only one thread can execute Python code at once. If you would like to make better use of the computational resources of multi-core machines, you should use multiprocessing or concurrent.futures.ProcessPoolExecutor. However, threading is still an appropriate model if you want to run multiple I/O-bound tasks simultaneously.

### Thread Pool

https://en.wikipedia.org/wiki/Thread_pool

A thread pool is a software design pattern for achieving concurrency of execution in a computer program. A thread pool matains multiple threads waiting for tasks to be allocated for concurrent execution by the supervising program. By maintaining a pool of threads, the model increases performance and avoids latency in execution due to frequent creation and destruction of threads for short-lived tasks. The number of available threads is tuned to the computing resources available to the program, such as parallel processors, cores, memory and network sockets.


### Daemon thread

- If a daemon thread (say B) is created within user thread (say A), then ending of this user/parent thread will NOT end the daemon/child thread.
- When all the non-daemon threads complete, daemon threads terminates automatically.
- If a daemon thread was created from a daemon thread then this is also a daemon thread. 
- Daemon threads are service providers for user threads running in the same process.



## Multi-processing

https://docs.python.org/3.5/library/multiprocessing.html

Multi-processing is a package that supports spawning processes using an API similar to the threading module.


### Spawning

Spawning refers to a function that loads and executes a new child process. The current process may wait for the child to terminate or may continue to execute concurrent computing.

### Fork

In the context of Unix OS, fork is an operation whereby a process creates a copy of itself. For a process to start the execution of a different program, it first forks to create a copy of itself. Then, the copy, called the child process, overlays itself with the other program. 

### Start Methods

- Spawn: Unnecessary file descriptors and handles from the parent process will not be inherited.
- Fork: All resources of the parent are inherited by the child process. However, safely forking a multithreaded process is problematic.
- Forkserver

### Exchange objects between processes

1. Queue, thread and process safe
2. Pipes, 

