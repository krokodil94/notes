[[What is Polymorphism in Python]]
**Concurrency** refers to the ability of a system to manage multiple tasks within overlapping time periods. It does not necessarily mean these tasks execute at the exact same instant. Rather, concurrency is about structuring a program to handle multiple operations by interleaving their execution, often on a single processor core.

**Parallelism**, by contrast, involves the simultaneous execution of multiple tasks. This typically requires multiple CPU cores or processors working in tandem, with each handling a separate portion of the workload at the same time.

### The Kitchen Analogy

A concurrent kitchen employs a single chef who rapidly switches between preparing multiple dishes. The chef might chop vegetables for one dish, then stir a sauce for another, then return to the first dish to continue preparation. From an observer's perspective, it appears that multiple dishes are being prepared "at once," but in reality, the chef is performing one action at a time in rapid succession.

A parallel kitchen has multiple chefs, each working on different dishes simultaneously. One chef prepares the appetiser while another works on the main course, and a third handles dessert. True simultaneous work is happening across multiple workers.

Same kitchen, different strategies, different outcomes.


Concurrency is fundamentally about task scheduling, coordination, and resource management. It enables a program to handle multiple operations by strategically interleaving their execution, whether on a single core or across multiple threads.
![[Pasted image 20260202183205.png]]

### Python Example: Implementing Concurrency with asyncio

To examine concurrency in more detail, we’ll create a simple application which gets data on various APIs asynchronously. This is an example of how Python’s library, asyncio, lets us spawn multiple network operations without blocking so we can effectively use the waiting time.

In this implementation, we’ll be simulating API calls to a weather service, a news service, and a user profile database. Pay attention to the fact that all three requests begin nearly at the same time, yet the program doesn’t wait until one of them is completed before it begins the next one.

```python
import asyncio

async def fetch_data_from_api(api_name, delay):
    print(f"Starting request to {api_name}...")
    await asyncio.sleep(delay)  # Simulates network I/O wait
    print(f"Received response from {api_name}")
    return f"Data from {api_name}"

async def fetch_user_profile(user_id):
    print(f"Fetching profile for user {user_id}...")
    await asyncio.sleep(1.5)
    print(f"Profile loaded for user {user_id}")
    return {"user_id": user_id, "name": "John Doe"}

async def main():
    # All tasks start and are managed concurrently
    results = await asyncio.gather(
        fetch_data_from_api("Weather API", 2),
        fetch_data_from_api("News API", 1),
        fetch_user_profile(12345)
    )
    print("\nAll operations completed!")
    print("Results:", results)

asyncio.run(main())
```

**What happens during execution:**

1. All three async functions are initiated at approximately the same time.
2. The event loop manages their execution, switching between tasks when one is waiting (during `await` statements).
3. While one task waits for simulated I/O, the event loop allows other tasks to make progress.
4. The task with the shortest delay completes first, even though all were started together.
5. No task blocks the others, resulting in efficient use of the single thread.
6. 
**Key insight:** Concurrency optimises responsiveness and resource utilisation. It doesn’t inherently make individual tasks complete faster. Instead, it allows multiple tasks to make progress during the same time period, particularly when those tasks involve waiting for external resources.

## What Parallelism Looks Like in Practice

![[Pasted image 20260202185153.png]]
Parallelism concerns itself with genuine simultaneous execution. This approach leverages multiple CPU cores or processors to divide work and execute portions concurrently in real time.
Parallelism shines when dealing with CPU-intensive operations such as mathematical computations, image processing, video rendering, or training deep learning models.

### Python Example: Implementing Parallelism with multiprocessing

To work with a sufficiently complex example, we’ll compute the sum of the squares of millions of numbers. In contrast to the concurrent code sample, where we were waiting to receive I/O, we are actually doing some CPU-intensive work. You’ll notice the reduction in the time taken to execute the work when it’s shared by a number of cores.

```python
from multiprocessing import Process, current_process
import time

def compute_heavy_task(task_name, iterations):
    """Simulates a CPU-intensive operation"""
    process_name = current_process().name
    print(f"{task_name} started on {process_name}")

    # Simulate CPU-bound work
    result = 0
    for i in range(iterations):
        result += i ** 2

    time.sleep(1)  # Additional simulated work
    print(f"{task_name} completed on {process_name}. Result: {result}")
    return result

if __name__ == "__main__":
    start_time = time.time()

    # Create separate processes for each task
    p1 = Process(target=compute_heavy_task, args=("Task 1", 10000000))
    p2 = Process(target=compute_heavy_task, args=("Task 2", 10000000))
    p3 = Process(target=compute_heavy_task, args=("Task 3", 10000000))

    # Start all processes (they run on separate CPU cores)
    p1.start()
    p2.start()
    p3.start()

    # Wait for all processes to complete
    p1.join()
    p2.join()
    p3.join()

    end_time = time.time()
    print(f"\nAll tasks completed in {end_time - start_time:.2f} seconds")
```

**What happens during execution:**

1. Three separate processes are spawned, each allocated to available CPU cores.
2. Each process runs independently with its own memory space and Python interpreter.
3. All three CPU-intensive calculations execute truly simultaneously across multiple cores.
4. The total runtime is determined by the longest-running task, not the cumulative sum of all tasks.
5. On a multi-core system, this completes approximately three times faster than sequential execution.

**Key insight:** Parallelism achieves actual speedup by distributing computational workload across multiple processors. This directly reduces total execution time for CPU-bound operations.

## Concurrency vs. Parallelism: A Detailed Comparison

|Aspect|Concurrency|Parallelism|
|---|---|---|
|**Core Definition**|Managing and coordinating multiple tasks within overlapping time periods|Executing multiple tasks simultaneously across multiple processors|
|**Primary Goal**|Improve structure, responsiveness, and resource efficiency|Increase raw computational throughput and speed|
|**CPU Utilization**|Can work on single or multiple cores through interleaving|Requires multiple cores or processors for true parallelism|
|**Execution Model**|Task switching and scheduling|Simultaneous execution across hardware|
|**Optimal Use Case**|I/O-bound operations (network requests, file operations, database queries)|CPU-bound operations (mathematical computations, data processing, rendering)|
|**Common Implementation Techniques**|Async/await patterns, threads, coroutines, event loops|Multiprocessing, GPU computing, and distributed computing frameworks|
|**Performance Characteristic**|Reduces idle time and improves throughput without necessarily speeding up individual tasks|Directly reduces execution time by dividing the work|
|**Typical Applications**|Web servers, REST APIs, GUI applications, chat systems, and real-time notifications|Video encoding, scientific simulations, machine learning training, big data analytics|
|**Resource Overhead**|Lower (shared memory, lightweight context switching)|Higher (separate memory spaces, inter-process communication costs)|
### When to Use Each:

Use **concurrency** when you want to handle more tasks effectively within the same time period, particularly when those tasks spend time waiting for external resources.

Use **parallelism** when you want to complete tasks faster by leveraging multiple processors to divide the computational workload.

## Real-World Applications and Use Cases

### Concurrency in Production Systems

#### 1. Web Servers and APIs

Modern web frameworks like Node.js, Django with async views, and FastAPI handle thousands of simultaneous client connections. Each request may involve database queries, external API calls, or file operations. Concurrency allows the server to handle new requests while waiting for I/O operations from previous requests to complete.

#### 2. Real-Time Communication

Chat applications, collaborative editing tools, and live streaming platforms manage multiple simultaneous connections. Messages must be received, processed, and broadcast to multiple clients concurrently without blocking any single connection.

#### 3. Mobile Applications

Mobile apps perform background synchronization, push notification handling, and data caching while maintaining a responsive user interface. The UI thread remains free while background operations proceed concurrently.

#### 4. Microservices Orchestration

Service meshes coordinate multiple API calls to different microservices, aggregating results efficiently without waiting for each call to complete sequentially.

### Parallelism in Production Systems

#### 1. Machine Learning and AI

Training neural networks involves massive matrix computations that can be distributed across multiple GPU cores or even multiple machines. Frameworks like TensorFlow and PyTorch automatically parallelise operations across available hardware.

#### 2. Big Data Processing

Distributed computing frameworks such as Apache Spark, Hadoop, and Dask divide large datasets across cluster nodes. Each node processes its portion of the data in parallel, enabling analysis of petabyte-scale datasets.

#### 3. Media Processing

Video transcoding, image batch processing, and audio rendering leverage multiple CPU cores or GPUs. Each frame or segment can be processed independently in parallel.

#### 4. Scientific Computing

Computational physics simulations, genome sequencing, and climate modelling require enormous computational resources. Parallelism across supercomputer clusters enables these calculations to complete in reasonable time frames.

#### 5. Financial Modelling

Risk analysis and portfolio optimisation involve running thousands of scenarios. Parallel processing allows these computations to execute simultaneously, providing results quickly enough for real-time decision making.

### Hybrid Approaches

In practice, sophisticated systems frequently combine both paradigms. Consider a modern web application:

1. The web server handles client requests concurrently (handling multiple users simultaneously).
2. Each request may trigger parallel data processing tasks (such as image resizing across multiple cores).
3. The database connection pool manages concurrent query execution.
4. Background job workers process tasks in parallel (such as sending emails or generating reports).

This layered approach leverages the strengths of both concurrency and parallelism to create systems that are both responsive and computationally efficient.

## Choosing the Right Approach for Your Problem


|If Your Task Is...|Choose...|Reasoning|
|---|---|---|
|**I/O-bound** (waiting for network, disk, or database operations)|**Concurrency**|Maximises efficiency by allowing other work to proceed during wait times. The bottleneck is not CPU computation but external resource availability.|
|**CPU-bound** (heavy mathematical computation, data processing, rendering)|**Parallelism**|Distributes computational load across multiple processors, directly reducing execution time. The bottleneck is CPU capacity.|
|**Mixed workload** (both I/O operations and intensive computation)|**Concurrency + Parallelism**|Concurrent handling of I/O operations combined with parallel processing of CPU-intensive segments provides optimal performance.|
|**Many small, independent tasks**|**Concurrency** (if I/O) or **Parallelism** (if CPU)|Choose based on whether tasks are waiting or computing.|
|**Few large, divisible computations**|**Parallelism**|Split each computation across cores for maximum speedup.|

### Common Pitfall to Avoid

A frequent mistake is attempting to use threading for CPU-bound tasks in languages with a Global Interpreter Lock (like Python's CPython) and expecting parallel speedups. In such cases, threads provide concurrency but not true parallelism.

The GIL ensures only one thread executes Python bytecode at a time, leading to context-switching overhead without genuine parallel execution. For CPU-bound work in Python, multiprocessing or C extensions are necessary for true parallelism.


## Why This Distinction Matters in Practice

Grasping the difference between concurrency and parallelism extends beyond writing faster code. It fundamentally influences how you architect systems and make technological decisions:
First of all, choosing the appropriate execution model for each component of your system leads to cleaner, more maintainable code. You avoid over-engineering solutions or applying the wrong tool to a problem.

Understanding these concepts also prevents wasteful patterns such as spawning unnecessary processes for I/O-bound work or using single-threaded approaches for parallelizable computations. This directly translates to reduced infrastructure costs.

Systems designed with proper concurrency models also scale horizontally more effectively. Those leveraging parallelism appropriately utilise hardware resources fully as you scale vertically.

In addition, you’ll get some key performance optimisations by choosing the right approach. When profiling reveals bottlenecks, knowing whether to optimise for concurrency or parallelism guides your refactoring efforts in the right direction.

Beyond this, in cloud environments where you pay for compute resources, efficient use of concurrency and parallelism directly affects operational costs. An efficiently concurrent system might handle 10x the load on the same hardware compared to a poorly designed synchronous alternative.

And these concepts are fundamental to backend engineering, distributed systems, DevOps, machine learning engineering, and systems programming. They appear frequently in technical interviews and are essential for senior engineering roles.

## Common Misconceptions and Clarifications

### "Using threads automatically gives me parallelism."

In reality, threads enable concurrency but do not guarantee parallel execution. In systems with a Global Interpreter Lock (like CPython) or on single-core machines, threads run concurrently but not in parallel. True parallelism requires multiple CPU cores and mechanisms that avoid locking constraints.

### "Parallelism is always faster than sequential execution."

In fact, parallelism introduces overhead, including process creation, inter-process communication, and data synchronisation costs. For small tasks or I/O-bound operations, this overhead can outweigh benefits. Parallelism shows gains when the computational work justifies the overhead.

### "Concurrency and parallelism are mutually exclusive."

As you’ve learned, modern high-performance systems routinely combine both. A web server can handle requests concurrently, with each request triggering parallel processing. Understanding how to layer these approaches is key to building sophisticated systems.

### "More threads or processes always mean better performance."

Beyond a certain point, adding more threads or processes leads to diminishing returns and even performance degradation due to increased context switching and resource contention. The optimal number depends on workload characteristics and available hardware.

### “Async/await makes my code run faster."

Async/await improves efficiency for I/O-bound operations by reducing idle time, but it does not speed up CPU-bound computations. It changes how waiting is handled, not how quickly individual operations execute.

## Practical Implementation Strategies

### How to Implement Concurrency

To introduce concurrency into your programs, first you’ll need to find where time is wasted. Blocking operations that are held waiting on external resources are the best candidates to be put under concurrent execution.

Say you’re building a web scraper to fetch a bunch of data on a variety of sites. Every single HTTP request is most likely waiting until the server gets a response back. Other requests might be underway in your program instead of waiting around during this waiting period. These wait points are identifiable by profiling your application and searching the operations with network calls, file I/O, or database queries.

After you’ve discovered these wait points, the next big step will be to select the concurrency primitive. In Python, I/O-bound operations perform very well using the patterns of async/await with the support of the asyncio framework. It also comes with a minimal cost.

```python
import asyncio
import aiohttp

async def fetch_user_api(user_id):
    async with aiohttp.ClientSession() as session:
        async with session.get(f'https://api.example.com/users/{user_id}') as response:
            return await response.json()

async def query_database(user_id):
    # Simulating database query
    await asyncio.sleep(0.5)
    return {'preferences': 'theme:dark', 'notifications': True}

async def get_complete_user_data(user_id):
    api_data, db_data = await asyncio.gather(
        fetch_user_api(user_id),
        query_database(user_id)
    )
    return {**api_data, **db_data}
```

### When Implementing Parallelism

Before committing parallelism into your system, you’ll need to profile the system and make sure that what causes your bottleneck is CPU-bound computation. Many developers think that their code requires parallelism when it should actually employ concurrency.

You can use profiling tools such as Python cProfile or line profilers to determine where time is being used or wasted in your program. When the time spent in computational loops is as large as compared to waiting in I/O, then parallelism can be beneficial.
To take an example, when processing images, the execution time in pixel manipulation algorithms consumes 90% of the execution time. This is a good sign that parallelism would be useful.

Deciding how to partition the work between multiple processors is sometimes a complex issue that you should consider carefully (in terms of dividing tasks into independent points). These chunks should be able to be processed individually without needing to communicate with each other on a regular basis.

Imagine that you have to examine the log files of several servers. Processing each file may happen on a different core, and the results will get added at the final stage.

```python
from multiprocessing import Pool
import re

def analyze_log_file(filepath):
    error_count = 0
    with open(filepath, 'r') as f:
        for line in f:
            if re.search(r'ERROR|CRITICAL', line):
                error_count += 1
    return filepath, error_count

if __name__ == '__main__':
    log_files = ['server1.log', 'server2.log', 'server3.log', 'server4.log']

    with Pool(processes=4) as pool:
        results = pool.map(analyze_log_file, log_files)

    for filepath, count in results:
        print(f'{filepath}: {count} errors found')
```

In this example, each log file is processed entirely on one core without needing to communicate with other processes until the final result aggregation.

## Tools and Technologies by Language

### Python

Python has a concurrent and parallel environment. For concurrent programming, the asyncio library offers a more modern syntax of async/await that’s ideal in I/O-bound tasks such as web scraping or API communication.

The threading module allows shared memory execution, but is restricted on CPU-bound tasks by the Global Interpreter Lock. The concurrent futures module is a high-level interface to concurrent task execution, which can be useful when you want to parallelize I/O operations without having to write the low-level code of asynchronous operations.

Sometimes you’ll need actual parallelism because your job requires a lot of CPU time. Multiprocessing starts individual Python processes, which don’t use the GIL at all.

In the case of data science and machine learning processes, distributed parallelism is offered in libraries such as joblib, ray, and dask and can run on your laptop up to a cluster of computers.

## Conclusion

Concurrency focuses on program structure and efficient task coordination. It allows systems to handle multiple operations within overlapping time periods, maximizing resource utilization and responsiveness.

Parallelism focuses on computational throughput and execution speed. It divides work across multiple processors to complete tasks faster through simultaneous execution.

The most powerful systems strategically combine both approaches, applying each where it provides the greatest benefit.The next time you face a performance challenge, ask yourself these critical questions:

1. Is my bottleneck caused by waiting (I/O-bound) or by computation (CPU-bound)?
    
2. Am I trying to handle more tasks simultaneously or complete tasks faster?
    
3. Do I need better resource utilisation or raw computational throughput?
    

Your answers will guide you toward the right solution. Understanding when to apply concurrency, when to leverage parallelism, and when to combine them is what separates adequate solutions from exceptional ones. This knowledge empowers you to build systems that are not only fast but also efficient, scalable, and economically viable.