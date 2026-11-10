---
title: Persistent Key-Value Store
category: software
featured: true
order: 1
summary: A crash-safe, log-structured key-value store in C++20, with recovery, compaction, and an epoll-based TCP server.
stack: [C++20, Linux, CMake, epoll, CRC32]
image: /assets/img/kv-store.svg
image_alt: Architecture diagram of the key-value store showing the TCP server, in-memory index, and append-only log files
image_caption: Architecture of the store (diagram I made)
repo: https://github.com/azamshahbaz07
---

## The Problem

Almost every backend system depends on a storage engine, and the hardest part of a storage engine isn't storing data. It's making sure the data is still correct after the power goes out halfway through a write. I wanted to understand how real databases guarantee that, so I built one from scratch instead of reading about it.

## The Process

I based the design on **Bitcask**, the log-structured model used in Riak. Every write is appended to the end of a data file instead of updating data in place. An in-memory hash index maps each key to the file and byte offset of its newest value, so a read takes one index lookup and one disk seek.

- **Durability:** a write-ahead log records each operation before it's acknowledged.
- **Integrity:** every record carries a CRC32 checksum, so a torn or corrupted write is detected instead of being returned as data.
- **Crash recovery:** on startup the store replays the log, rebuilds the index, and discards any partial record at the tail.
- **Compaction:** because old values pile up in an append-only log, a compaction pass rewrites only the live keys into new files and swaps them in.
- **Networking:** clients talk to the store over TCP through a multithreaded server built on Linux `epoll`, supporting GET, PUT, and DEL for 64 concurrent clients.

## The Outcome

- **Throughput:** 150K+ reads/sec and 40K+ durable writes/sec with 64 concurrent clients.
- **Durability:** 1,000 randomized `kill -9` crash-injection runs and 100+ unit tests, with zero lost writes.
- **Space:** background compaction cuts disk usage by 60%+.

Beyond the numbers, the project made abstract ideas concrete for me: why appends are fast, why checksums matter, why `fsync` is expensive, and why compaction is a trade-off between disk space and background work.

## What's Next

I want to measure tail latency, not just throughput, and experiment with batching `fsync` calls to see how much latency I can trade for write throughput.
