---
title: "How to Write Fast Code?"
excerpt: "A Quick-start Toolkit for Fast Coders"
collection: resources
---

# How to Write Fast Code? &mdash; A Quick-start Toolkit for Fast Coders

Given a slow code, the first thing to look into is to check if the algorithm is efficient enough, i.e., try to improve algorithmic complexity.
The second step is to make sure the code does its work efficiently, i.e., do not do unnecessary or redundant work.
Next we want to make sure the program accesses its data efficiently. 
This is usually checked by using some [profiling](https://en.algorithmica.org/hpc/profiling/) tools, e.g. [cachegrind](https://valgrind.org/docs/manual/cg-manual.html), to see if the program is memory or IO bound.
Finally we want to parallelize the program as much as possible, to fully leverage modern parallel hardware, like multicore CPUs or GPUs.

1. [Algorithm](#algorithm)
2. [Work Efficiency](#work)
3. [Memory Efficiency](#memory)
4. [Parallelization](#parallelization)

  
## Algorithm: the Big O notation <a name="algorithm"></a>

Please refer to the [algorithm course](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/).

[Cache-Oblivious Algorithms](https://en.algorithmica.org/hpc/external-memory/oblivious/)

## Work Efficiency: Bentley's Rules <a name="work"></a>

In performance engineering, the **work** of a program (on a given input) is the sum total of all the operations executed by the program.
You can think about work as the number of executed instructions. 
We don’t like doing unnecessary work, because that generally means our program is wasting hardware resources.

If we reduce work, our program usually runs faster (but not always, because hardware is complicated). 
But reducing work is a good heuristic for making your code run faster: execute fewer instructions.

Algorithmic engineering is a great way to reduce work, which you should be familiar with from an algorithms class.
Here we summarize a list of techniques to reduce work, beyond algorithms, which are known as the Bentley's rules.
We classify them into four categories: data structures, logics, loops and functions.

### Data structures 

* **Precomputation** performs calculations in advance so as to avoid doing them at *mission-critical* times.
 
* **[Alignment and Packing](https://en.algorithmica.org/hpc/cpu-cache/alignment/)** stores more than one data value in a machine word.
  
* **Encoding** converts data values into a representation that requires fewer bits.
 
* **Augmentation** adds information to a data structure to make common operations do less work.
 
* **Caching / Memoization** stores results that have been accessed recently so that the program need not compute them again.

 
### Logic

* **Short-circuiting** stops evaluating as soon as you know the answer.

* **Algebraic Identities** replaces expensive algebraic expressions with algebraic equivalents that require less work.

* **Creating a Fast Path** replaces expensive operations with cheaper ones under some conditions. 

<!--* **Eliminating redundant computation** removes redundant computation that is unnecessary.-->

### Loops	

* **Loop fusion**, a.k.a jamming, is to combine multiple loops over the same index range into a single loop body, thereby saving the overhead of loop control.	

* **Loop hoisting**, a.k.a. loop-invariant code motion, is to avoid recomputing loop-invariant code each time through the body of a loop.

* **Loop unrolling** combines several consecutive iterations of a loop into a single iteration, thereby reduces the total number of iterations of the loop and, consequently, the number of times that the instructions that control the loop must be executed.

* **Eliminate wasted iterations** modifies loop bounds to avoid executing loop iterations over essentially empty loop bodies.

### Functions	

* **Coarsening recursion** increases the size of the base case and handle it with more efficient code that avoids function-call overhead.	

* **Inlining** avoids the overhead of a function call by replacing a call to the function with the body of the function itself.

* **Tail-recursion elimination** removes the overhead of a recursive call that occurs as the last step of a function.
  The call is replaced with a branch to the top of the function, and the storage for the local variables of the function is reused by the erstwhile recursive call.
	

## Memory Efficiency: Cache, DRAM, IO <a name="memory"></a>

Many of the modern applications are actually memory bound, instead of compute bound, as computation in modern processors is much faster then accessing data in the memory.
For memory bound applications, the key to improve performance is to improve memory efficiency.

Generally there are three ways we can improve memory efficiency: 
(1) improve data locality, 
(2) hide memory access latency,
and (3) improve memory bandwidth efficiency.

### Improve Locality

* **Tiling** modifies the memory access pattern in order to reuse data already present in the cache before that data gets evicted.

* **Loop interchange**	accesses data in a way friendly to cache.

* **Memory access reordering**	reorders operations or tasks to sequentialize memory accesses or reduce reuse distance.

### Hide Latency

* **[Prefetching](https://en.algorithmica.org/hpc/cpu-cache/prefetching/)** brings data into caches before it is actually used, in order to mask the long latencies required to fetch data from memory.				

* **Pipelining** overlaps communication (data fetch) with computation .					

### Improve Bandwidth Efficiency

* **Compression & Compaction**	uses lossy or lossless compression to dynamically determine output locations without introducing Fragmentation.					

* **[Data Layout Transformation](https://en.algorithmica.org/hpc/cpu-cache/aos-soa/)** transforms array-of-structures (AoS) to structure-of-arrays (SoA).


## Parallelization <a name="parallelization"></a>

There are three major reasons for inefficient parallel code:
(1) limited parallelism,
(2) high synchronization overhead,
(3) load imbalance.

### Increase Parallelism

* **Parallel primitives composition** composes parallel programs using parallel patterns or [primitives](https://github.com/cmuparlay/parlaylib/tree/master/examples).

* **Multi-threading** exploits thread-level parallelism (TLP). It is often used for task parallelism.

* **[Vectorization](https://en.algorithmica.org/hpc/simd/)**, a.k.a SIMD, exploits data parallelism by using hardware vector units.	

* **Hybrid parallelism** combines task, data and pipeline parallelism.

* **Speculative parallelism** runs tasks speculatively and checks that they followed a correct order, for tasks with order constraints.

### Reduce Synchronization Overhead	

* **Privatization** avoids data race by privatizing shared variables.	

* **Scatter-to-gather transformation**, a.k.a. push-vs-pull, switches between	input and output irregularity (i.e. random accesses).			

* **Lock/atomics free concurrency**, a.k.a. *non-blocking* or *nondeterministic* parallellism, removes unnecessary locks or atomic operations.				

* **Asynchronous execution** asynchronously executes tasks that do not depend on each other, i.e. removes unnecessary barriers.

### Load Balancing

* **Static/Dynamic scheduling**	chooses the best task scheduling policy to balance workload with minimum scheduling overhead.			

* **Regularization** proactively redistributes or regularizes the skewed workload.	

