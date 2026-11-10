---
title: Work-Stealing Thread Pool + Allocator
category: software
featured: false
order: 2
summary: A work-stealing thread pool built on Chase-Lev deques, paired with a thread-caching memory allocator.
stack: [C++20, Linux, Valgrind, TSan/ASan]
image: /assets/img/thread-pool.svg
image_alt: Diagram of worker threads with their own deques, one thread stealing work from another
image_caption: Each worker owns a deque; idle workers steal from the other end (diagram I made)
repo: https://github.com/azamshahbaz07
---

## The Problem

A simple thread pool uses one shared task queue protected by a lock. Under load, every thread fights over that lock, and adding cores stops helping. I wanted to understand how production runtimes avoid that bottleneck.

## The Process

Each worker thread owns a **Chase-Lev deque**. A worker pushes and pops its own tasks from one end with no locking in the common case. When a worker runs out of work, it **steals** from the opposite end of another worker's deque, using atomic operations to resolve the race when both sides go for the last task. Callers get results back through futures.

Allocation was the next bottleneck: if every task allocates through the global allocator, threads contend there instead. So I built a **thread-caching allocator** that gives each thread its own size-class free lists and only falls back to a shared pool when a cache runs dry or overflows.

## The Outcome

- **Scaling:** a 6× speedup on 8 threads.
- **Allocation:** 3–5× faster than `malloc` on small multithreaded allocations.
- **Correctness:** 80+ tests and 1,000+ stress runs under ThreadSanitizer, AddressSanitizer, and Valgrind, with zero data races or leaks.

The project also taught me memory ordering in practice: which operations need acquire/release semantics, which need a full fence, and how easy it is to write lock-free code that passes tests but is still wrong.
