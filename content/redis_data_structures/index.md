---
date: 2016-03-09T00:11:02+01:00
title: Redis Data Structures with beacon
weight: 10
---

This is designed to help the user understand what is going on inside of redis at a low level.  The following are redis keys (with examples) and what they store.

* **`ip:<sha3:512 hashed id>`**  
  This entry is created only if a client has used the beacon-id to store an address
  type: redis key
  content: host ip
  example `ip:bd98828400c404c3feaf<SNIP>` 192.168.2.2
* **`sec:<sha3:512 hashed id>`**  
  This entry is created once an id has been provisioned.
  type: redis key
  content: sha3:512 hash of security key
  example `sec:bd98828400c404c3fea<SNIP>` e7f8a5a8f35343d`<SNIP>`
