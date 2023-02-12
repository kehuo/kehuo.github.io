---
id: cmu-15445-db-mem-mgmt-and-buffer-cache
sidebar_label: Memory Management And Buffer Cache
title:  CMU 15445 Database Overview
permalink: /cmu-15445-database/memory-mgmt-and-buffer-cache
---

# Memory Management and Buffer Cache

### OS Page Cache

Most disk operations go through the OS API. Unless the DBMS tells it not to, the OS maintains
its own filesystem cache (a.k.a page cache, buffer cache, etc.).

Most DBMSs use direct I/O (O_DIRECT) to bypass the OS cache.

- Redundant copies of pages.
- Different eviction policies.
- Loss of control over file I/O.

![Image about how DBMS interact with OS I/O API with and without OS filesystem cache](../../static/image/cmu15445_os_fs_cache.png)


### Buffer Replcement Policies

When the DBMS needs to free up a frame to make room for a new page, it must decide which page to **evict** from the buffer pool.

Goals:

- Correctness
- Accuracy
- Speed
- Meta-data overhead




