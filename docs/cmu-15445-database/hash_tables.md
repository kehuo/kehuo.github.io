---
id: cmu-15445-db-hash-tables
sidebar_label: Hash Tables
title:  Hash Tables
permalink: /cmu-15445-database/hash-table
---

# Hash Table

### Course Status

We are now going to talk about how to support the DBMS execution engine to read/write data from pages.

Two types of data structures:
- Has Tables
- Trees

### Data Structures

- Internal Meta-data
- Core Data Storage
- Temporary Data Structures
- Table Indexes

### Design Decisions

#### Data Organization
How we layout data structure in memory/pages and what information to store to support efficient access.

#### Concurrency
How to enable multiple threads to access the data structure at the same time without causing problems.


### Hash Table
#### Design Decision 1: Hash Function
- How to map a large key space into a smaller domain.
- Trade-off between being fast vs. collision rate.

#### Design Decision 2: Hashing Scheme
- How to handle key collisions after hashing.
- Trade-off between allocating a large hash table vs. additional instructions to get/put keys.


### Today Agenda
- Hash Functions
- Static Hashing Schemes (number of keys are fixed.)
- Dynamic Hashing Schemes (keys are incrementally grow and shrink the size of the hash table)

### Hash Functions
For any input key, return an integer representation of that key.

We do NOT want to use a cryptographic hash function for DBMS hash tables (e.g., SHA-2), becahse SHA-2 is slow.

We want something that is fast and has a low collision rate.

### Known Hash Functions

#### CRC-64 (1975)
- Used in networking for error detection.

#### MurmurHash (2008)
- Designed as a fast, general-purpose hash function.

#### Google CityHash (2011)
- Designed to be faster for short keys (< 64 bytes).

#### Facebook XXHash (2012)
- From the creator of zstd compression.

#### Google FarmHash (2014)
- New version of CityHash with better collision rates.

Conclusion: From a database developer's perspective, just use XX Hash 3.


### Static Hashing Schemes

- Approach 1: Linear Probe Hashing 

- Approach 2: Robin Hood Hashing

- Approach 3: Cuckoo Hashing

#### Linear Probe Hashing

Single giant table of slots.

Resolve collusions by linearly searching for the next free slot in the table.
- To determine whether an element is present, hash to a location in the index and scan for it.
- Must store the key in the index to known when to stop scanning.
- Insertions and deletions are generalizations of lookups. 


### Non Unique Keys
Choices 1: Separate Linked List.
- Store values in separate storage area for each key.

Choices 2: Redundant Keys
- Store dunpolicate keys entries together in the has table.
- This is easier to implement so this is what most systems do.


### Observatioin

The previous hash tables require the DBMS to know the number of elements it wants to store.
- Otherwise, it must rebuild the table if it needs to grow/shrink in size.

Dynamic hash tables resize themselves on demand.
- Chained Hashing
- Extendible Hashing
- Linear Hashing

#### Extendible Hashing

This is an extension of Chained-hashing approach, where we split buckets instead of letting the linked list grow forever.

multiple slot locations can point to the same bukcet chain.

Reshuffle bucket entries on split and increase the number of bits to examine.
- Data movement is localized to just the split chain.

 


