---
title: "How to Write Fast Code?"
excerpt: "A Quick-start Toolkit for Fast Coders"
collection: resources
---

# How to Write Fast Code? &mdash; A Quick-start Toolkit for Fast Coders

Given a slow code, the first thing to look into is to check if the algorithm is efficient enough, i.e., try to improve algorithmic complexity.
The second step is to make sure the code does its work efficiently, i.e., do not do unnecessary or redundant work.
Next we want to make sure the program accesses its data efficiently. 
This is usually checked by using some profiling tools, e.g. [cachegrind](https://valgrind.org/docs/manual/cg-manual.html) to see if the program is memory or IO bound.
Finally we want to parallelize the program as much as possible, to fully leverage modern parallel hardware, like multicore CPUs or GPUs.

1. [Algorithm](#algorithm)
2. [Work Efficiency](#work)
3. [Memory Efficiency](#memory)
4. [Parallelization](#parallelization)

  
## Algorithm: the Big O notation <a name="algorithm"></a>

Please refer to the [algorithm course](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/).

## Work Efficiency: Bentley's Rules <a name="work"></a>

### Data structures 

* Precomputation
 
* Packing and Encoding	
 
* Augmentation	
 
* Caching / memoization
 
### Logic

* Short-circuiting	

* Algebraic Identities	

* Creating a Fast Path	

* Eliminate redundant computation

### Loops	

* Loop fusion	

* Loop hoisting	

* Loop unrolling

* Eliminate wasted iterations

### Functions	

* Coarsening recursion	

* Inlining

* Tail-recursion elimination
	

## Memory Efficiency: Cache, DRAM, IO <a name="memory"></a>

* **Tiling**	modifies the memory access pattern in order to reuse data already present in the cache before that data gets evicted.		

* **Prefetching**	brings data into caches before it is actually used, in order to mask the long latencies required to fetch data from memory.				

* **Pipelining** overlaps communication (data fetch) with computation .					

* **Compression & Compaction**	uses lossy or lossless compression to dynamically determine output locations without introducing Fragmentation.		

* **Loop interchange**	accesses data in a way friendly to cache.

* **Memory access reordering**	reorders operations or tasks to sequentialize memory accesses or reduce reuse distance.					

* **Data Layout Transformation** transforms	array-of-structures (AoS) to structure-of-arrays (SoA).

## Parallelization <a name="parallelization"></a>

* **Parallel primitives composition**	composes parallel programs using parallel patterns or [primitives](https://github.com/cmuparlay/parlaylib/tree/master/examples).

* **Multi-threading**	exploits thread level parallelism.

* **Static/Dynamic scheduling**	chooses the best task scheduling policy.			

* **Regularization**	proactively redistributes or regularizes the skewed workload.		

* **Speculative parallelism**	runs tasks speculatively and checks that they followed a correct order, for tasks with order constraints.

* **Vectorization** exploits data parallelism by using hardware vector units.

* **Privatization**	avoids data race by privatizing shared variables.				

* **Hybrid parallelism** combines task, data and pipeline parallelism.

* **Scatter-to-gather transformation** a.k.a., push vs. pull, switches between	input and output irregularity (i.e. random accesses).			

* **Lock/atomics free concurrency**	a.k.a., non-blocking algorithm or nondeterministic parallellism, removes unnecessary locks or atomic operations.				

* **Asynchronous execution** asynchronously executes tasks that do not depend on each other, i.e. removes unnecessary barrier.	

