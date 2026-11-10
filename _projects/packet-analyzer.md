---
title: Multithreaded Packet Analyzer
category: software
featured: true
order: 3
summary: Parses Ethernet, VLAN, IPv4, TCP, and UDP traffic from pcap files and live sockets through a lock-free pipeline.
stack: [C++20, Linux, CMake, Python, libFuzzer]
image: /assets/img/packet-pipeline.svg
image_alt: Pipeline diagram showing capture, lock-free queues, parser threads, and flow table
image_caption: Capture-to-flow-table pipeline (diagram I made)
repo: https://github.com/azamshahbaz07
---

## The Problem

Network tools have to parse untrusted bytes at line rate. That means the parser has to be fast, and it also has to survive malformed input without crashing. I wanted to build one that did both.

## The Process

Packets come either from saved **pcap** files or live from Linux **AF_PACKET** raw sockets. A capture thread hands raw frames to parser threads through **lock-free queues**. The parsers decode the layers in order (Ethernet, optional VLAN tags, IPv4, then TCP or UDP), bounds-checking every header before trusting a length field. A sharded flow table tracks each connection, and TCP streams are reassembled in order.

## Verification

- **Correctness:** I compared my parser's output against **tshark** (Wireshark's command-line tool) on 50+ captures.
- **Robustness:** I fuzzed the parsing code with **libFuzzer**, which feeds it mutated inputs to find crashes and out-of-bounds reads, alongside 70+ unit tests.

## The Outcome

The pipeline sustains **2M+ packets/sec** and tracks **100K+ concurrent connections**. Fuzzing found edge cases I would never have written tests for, and fixing them taught me to treat every length field in a packet as a potential bug. Comparing against tshark gave me confidence that the parser was actually correct, not just stable.
