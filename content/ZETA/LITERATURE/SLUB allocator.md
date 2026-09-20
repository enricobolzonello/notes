---
up:
  - "[[OS - Virtual Memory]]"
tags:
  - atomic
created: 2026-04-02 14:47
---

As explained in [[OS - Virtual Memory#Slab allocation]], there's 3 parts to a slab based allocator:
- caches
- slab
- objects

![[slub_allocator.png]]

- when the kernel wants to make an allocation, it will find the right cache and then find a partial slab to allocate that object.
- if no partial or free slab, the allocator will allocate new slabs with the [[OS - Virtual Memory#Buddy system|buddy allocator]]
- each free slab in the partial list will have a pointer to the next free slab, creating a linked list


# References
- https://sam4k.com/linternals-memory-allocators-0x02/