# 🖥️ Operating Systems — Day 1 Interview Notes
> **Topics:** Intro to OS · Types of OS · Multitasking vs Multithreading · Context Switching

---

## 📌 Table of Contents
1. [What is an Operating System?](#1-what-is-an-operating-system)
2. [Why Do We Need an OS?](#2-why-do-we-need-an-os)
3. [Functions of an OS](#3-functions-of-an-os)
4. [Goals of an OS](#4-goals-of-an-os)
5. [Types of Operating Systems](#5-types-of-operating-systems)
6. [Program vs Process vs Thread](#6-program-vs-process-vs-thread)
7. [Multitasking vs Multithreading](#7-multitasking-vs-multithreading)
8. [Context Switching](#8-context-switching)
9. [Interview Questions & Tricks](#9-interview-questions--tricks)

---

## 1. What is an Operating System?

> **Definition:** An OS is a piece of **system software** that manages all resources of a computer system — both hardware and software — and provides an environment in which the user can execute programs in a convenient and efficient manner by **hiding underlying hardware complexity** and acting as a **resource manager**.

### Key Distinction
| Type | Description |
|------|-------------|
| **Application Software** | Performs a specific task for the user (e.g., Chrome, MS Word) |
| **System Software** | Operates and controls the computer system; provides a platform to run application software |
| **Operating System** | The most critical system software — the bridge between hardware and applications |

### Layered View
```
        [ User ]
           ↓
  [ Application Programs ]
           ↓
    [ Operating System ]       ← You are here
           ↓
   [ Computer Hardware ]
```

### 🧠 Memory Trick
> **"ARCH"** — OS does **A**rbitration (resource mgmt), **R**uns programs, **C**onceals hardware, **H**ides complexity (Abstraction)

---

## 2. Why Do We Need an OS?

### What if there were NO OS?
| Problem | Explanation |
|---------|-------------|
| **Bulky & Complex Apps** | Every app would need hardware interaction code in its own codebase — imagine writing disk I/O for every app! |
| **Resource Exploitation** | One app could monopolize the CPU, starving others |
| **No Memory Protection** | App A could read/overwrite App B's memory — catastrophic security issue |

### What is an OS made up of?
> A **collection of system software** — kernel, device drivers, file systems, schedulers, memory managers, etc.

---

## 3. Functions of an OS

| Function | Also Called | Examples |
|----------|-------------|---------|
| Provides access to hardware | — | Keyboard, display, disk |
| Interface between user & hardware | — | GUI, shell |
| **Resource Management** | **Arbitration** | Memory, CPU, devices, files, security, processes |
| **Hides hardware complexity** | **Abstraction** | You write to a "file", not a specific disk sector |
| Isolation & Protection | — | One process can't corrupt another |

### 🧠 Memory Trick
> **"HAIR"** — **H**ardware access, **A**bstraction, **I**solation, **R**esource management

---

## 4. Goals of an OS

- ✅ **Maximum CPU Utilization** — CPU should never be idle unnecessarily
- ✅ **Less Process Starvation** — Every process should eventually get CPU time
- ✅ **Higher Priority Job Execution** — Important processes run first

---

## 5. Types of Operating Systems

### Quick Reference Table

| Type | Key Idea | CPUs | Example | Era |
|------|----------|------|---------|-----|
| **Single Process** | 1 process at a time from ready queue | 1 | MS-DOS | 1981 |
| **Batch Processing** | Jobs grouped into batches by operator | 1 | ATLAS, Manchester Univ. | Late 1950s – early 1960s |
| **Multiprogramming** | Multiple jobs in memory; CPU switches on I/O wait | 1 | THE (Dijkstra) | Early 1960s |
| **Multitasking** | Logical extension of multiprogramming; time-sharing | 1 | CTSS, MIT | Early 1960s |
| **Multi-processing** | Multiple CPUs in one machine | >1 | Windows NT | Modern |
| **Distributed OS** | Multiple networked independent computers | ≥1 per node | LOCUS | Modern |
| **Real-Time OS (RTOS)** | Strict time deadlines; must be error-free | Any | ATCS | Modern |

---

### 5.1 Single Process OS *(Oldest)*
- Only **1 process executes at a time** from the ready queue.
- All other processes must wait their turn.
- **Disadvantage:** CPU sits idle while the current process does I/O.

---

### 5.2 Batch Processing OS

**Flow:**
```
User writes job (punch card)
        ↓
Submit to Operator
        ↓
Operator groups similar jobs into Batches
        ↓
Batches submitted to CPU one by one
        ↓
All jobs of one batch execute together
```

**Disadvantages:**
- ❌ Priorities **cannot** be set — a high-priority job stuck behind a batch has to wait
- ❌ Can lead to **starvation** — a slow batch blocks everything after it
- ❌ CPU may become **idle** during I/O operations (no other job to switch to)

---

### 5.3 Multiprogramming OS

> **Core Idea:** Keep **multiple jobs (code + data) in memory** so the CPU always has something to execute when one job does I/O.

**How it works:**
- Single CPU
- When the current process goes to **wait state** (e.g., disk I/O), CPU **context switches** to another ready process
- **CPU idle time is reduced** significantly

**Key Improvement over Batch:** CPU doesn't sit idle during I/O — it switches to another job.

---

### 5.4 Multitasking OS

> **Multitasking = Logical extension of Multiprogramming**

**Extra features over Multiprogramming:**
- **Time-sharing** — CPU time is divided into slices (quantum), each process gets a turn
- Able to **run more than 1 task "simultaneously"** (rapid switching creates illusion)
- **Context switching + time sharing** both used
- **Increases responsiveness** — user feels the system responds to them immediately
- CPU idle time further reduced

### Multiprogramming vs Multitasking

| Feature | Multiprogramming | Multitasking |
|---------|-----------------|--------------|
| Switching trigger | Process goes to wait/I/O | Time quantum expires OR I/O |
| User interaction | Minimal | High (interactive) |
| Time sharing | ❌ | ✅ |
| Responsiveness | Lower | Higher |

---

### 5.5 Multi-processing OS

> More than **1 CPU in a single computer**

**Advantages:**
- ✅ **Increased Reliability** — if 1 CPU fails, others can take over (fault tolerance)
- ✅ **Better Throughput** — multiple processes run truly in parallel
- ✅ **Less Process Starvation** — if 1 CPU is busy, other CPUs can execute waiting processes

---

### 5.6 Distributed OS

> OS manages many bunches of resources: **≥1 CPUs, ≥1 memory, ≥1 GPUs**, etc.

- **Loosely connected autonomous, interconnected** computer nodes
- Collection of **independent, networked, communicating, and physically separate** computational nodes
- Each node has its own OS; they coordinate via network
- Example: **LOCUS**

**vs Multi-processing:**

| | Multi-processing | Distributed |
|--|-----------------|-------------|
| Location | All CPUs in 1 machine | CPUs in different machines |
| Memory | Shared memory | Each node has its own memory |
| Coupling | Tightly coupled | Loosely coupled |

---

### 5.7 Real-Time OS (RTOS)

> **Real-time** = computations must complete within **strict time boundaries**

- Error-free, deterministic execution
- Used in **safety-critical systems**
- Examples: Air Traffic Control Systems (ATCS), ROBOTS, medical devices, missile systems

**Types of RTOS:**
| Type | Description |
|------|-------------|
| **Hard RTOS** | Missing a deadline = system failure (e.g., airplane autopilot) |
| **Soft RTOS** | Missing a deadline = degraded performance, not catastrophic (e.g., video streaming) |

### 🧠 Memory Trick for Types of OS (in order of evolution):
> **"Single Batch Men Must Demand Real Coffee"**
> **S**ingle → **B**atch → **M**ulti-programming → **M**ulti-tasking → **D**istributed → **R**eal-time → (**C**loud — modern extension)

---

## 6. Program vs Process vs Thread

| | Program | Process | Thread |
|--|---------|---------|--------|
| **Definition** | Executable file with a set of instructions | Program under execution | Single sequence stream within a process |
| **Location** | Stored on **Disk** | Resides in **RAM** (primary memory) | Exists within a process in RAM |
| **Nature** | Passive (compiled code, ready to execute) | Active | Lightweight process |
| **State** | Static | Dynamic | Dynamic |
| **Memory** | No memory allocated | Own memory space | Shares process memory |

### Thread — Deep Dive

A thread is:
- An **independent path of execution** within a process
- A **lightweight process** (cheaper to create/destroy)
- Used to achieve **parallelism** by dividing a process's independent tasks

**Real-world examples:**
- Browser: Each tab = separate thread (rendering, JS execution, network — all concurrent)
- Text editor: Typing, spell-checking, auto-saving, formatting = separate threads running concurrently

---

## 7. Multitasking vs Multithreading

| Feature | Multi-Tasking | Multi-Threading |
|---------|--------------|-----------------|
| **Definition** | Execution of more than one **task (process)** simultaneously | A process divided into several **sub-tasks (threads)**, each with its own execution path |
| **Concept** | More than 1 **process** being context switched | More than 1 **thread** being context switched |
| **No. of CPUs** | 1 CPU | ≥ 1 CPU (better with more) |
| **Isolation & Memory Protection** | ✅ **Exists** — OS allocates separate memory and resources to each process | ❌ **No isolation** — resources are shared among threads of the same process |
| **Memory allocation** | OS gives separate memory to each program | OS allocates to process; all threads of that process **share** the same memory |
| **Overhead** | Higher (process creation is expensive) | Lower (thread creation is cheap) |
| **Communication** | IPC required (complex) | Direct shared memory (simple but needs sync) |
| **Crash impact** | One process crash doesn't affect others | One thread crash can crash the whole process |

### 🧠 Memory Trick
> **"Tasks are Isolated, Threads are Tangled"**
> Multitasking = processes separated by walls. Multithreading = threads sharing the same house.

---

## 8. Context Switching

> **Context switching** = saving the state of the current process/thread and loading the state of the next one.

### Thread Context Switching vs Process Context Switching

| Feature | Thread Context Switching | Process Context Switching |
|---------|--------------------------|---------------------------|
| **What OS saves** | Current state of **thread** (PC, registers, stack) → switches to another thread of the **same process** | Current state of **process** → switches to a **different process** by restoring its state |
| **Memory address space** | ❌ NOT switched (same process = same address space) | ✅ Switched (different process = different address space) |
| **What's included** | Program counter, registers, stack | Program counter, registers, stack **+ memory address space** |
| **Speed** | ⚡ **Fast** | 🐢 **Slow** |
| **CPU Cache** | ✅ **Preserved** (same process memory) | ❌ **Flushed** (new process has different memory) |
| **Cost** | Cheap | Expensive |

### Why is Process Context Switching Slow?
1. Must save/restore more state (entire process memory context)
2. Memory address space changes → TLB (Translation Lookaside Buffer) must be flushed
3. CPU cache is cold after switch — cache misses increase
4. OS must update PCB (Process Control Block)

### 🧠 Memory Trick
> **"Thread switch = same house, just change rooms. Process switch = move to a new house entirely."**
> - Same house → no need to change locks (address space preserved, cache preserved) → Fast
> - New house → new keys, new layout, re-learn everything → Slow

---

## 9. Interview Questions & Tricks

### 🔥 Most Asked Questions

**Q1. What is an OS? What are its functions?**
> OS = resource manager + hardware abstractor. Functions: hardware access, arbitration, abstraction, isolation, protection.

**Q2. What is the difference between Multiprogramming and Multitasking?**
> Both keep multiple jobs in memory. Multiprogramming switches on I/O wait; Multitasking adds time-sharing (quantum-based switching) for better responsiveness.

**Q3. What is the difference between Multiprocessing and Multitasking?**
> Multitasking = 1 CPU, rapid switching (illusion of parallelism). Multiprocessing = multiple CPUs, true parallelism.

**Q4. Process vs Thread?**
> Process = program in execution, isolated, heavyweight. Thread = lightweight unit within a process, shares memory, cheap to create.

**Q5. Why is thread context switching faster than process context switching?**
> Threads share address space → no TLB flush, no cache flush, less state to save/restore. Processes require full address space switch → TLB flush, cache flush, expensive.

**Q6. What is RTOS? Give examples.**
> OS with strict real-time deadlines. Hard RTOS (airplane autopilot) vs Soft RTOS (video streaming). Examples: ATCS, ROBOTS, VxWorks, FreeRTOS.

**Q7. What is the difference between Distributed OS and Multi-processing OS?**
> Multi-processing = multiple CPUs in 1 machine, shared memory, tightly coupled. Distributed = multiple machines networked, each with own memory, loosely coupled.

---

### ⚡ Quick Revision Cheatsheet

```
OS = Resource Manager + Abstraction Layer

Types (Evolution):
Single → Batch → Multiprogramming → Multitasking → Multiprocessing → Distributed → RTOS

Key Differences:
- Multiprogramming vs Multitasking: Add TIME SHARING for multitasking
- Multitasking vs Multiprocessing: Add MORE CPUs for multiprocessing
- Multiprocessing vs Distributed: SEPARATE MACHINES for distributed

Thread vs Process:
- Thread: lightweight, shared memory, fast switch, no isolation
- Process: heavyweight, own memory, slow switch, isolated

Context Switch Speed:
- Thread > Process (because no address space switch, cache preserved)
```

---

> 📅 **Day 1 Complete!**
> Next → **Day 2:** Processes — Lifecycle, PCB, States, IPC, Scheduling Queues
