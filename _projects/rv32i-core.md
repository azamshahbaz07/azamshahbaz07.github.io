---
title: Pipelined RV32I Core
category: hardware
featured: false
order: 1
summary: A pipelined processor implementing the RISC-V RV32I base integer instruction set, written in Verilog.
stack: [Verilog, RISC-V, RTL design, Simulation]
image: /assets/img/rv32i-pipeline.svg
image_alt: Five-stage pipeline diagram with fetch, decode, execute, memory, and writeback stages
image_caption: Classic five-stage pipeline structure (diagram I made)
repo: https://github.com/azamshahbaz07
---

## The Problem

I could write RISC-V assembly, but I wanted to understand what actually happens to each instruction inside the processor. The best way to learn that was to build the processor.

## The Process

I implemented the **RV32I** base integer instruction set in Verilog and split execution into pipeline stages so several instructions are in flight at once. Pipelining is where the real design work is: an instruction may need a result that hasn't been written back yet (a data hazard), or the pipeline may have fetched the wrong instructions after a branch (a control hazard). Resolving those hazards correctly was the core challenge, and I verified the design in simulation with test programs.

## The Outcome

Building the core changed how I write software. I now think about how loads, branches, and dependencies look to the pipeline, which connects directly to the low-latency systems work I want to do.

## Other hardware work

I've also built an Ethernet frame parser in RTL, a memory-mapped dot-product accelerator, and a custom dual-channel oscilloscope. Write-ups for these are coming soon.
