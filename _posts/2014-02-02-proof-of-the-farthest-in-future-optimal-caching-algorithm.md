---
layout: post
title: "Proof of the Farthest-in-Future Optimal Caching Algorithm"
categories:
  - Programming
  - Algorithms
image: assets/images/algorithm.jpg
description: "Mathematical proof that the Farthest-in-Future algorithm minimizes cache misses"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2014/02/02/proof-of-the-farthest-in-future-optimal-caching-algorithm/](https://blog.henrypoon.com/blog/2014/02/02/proof-of-the-farthest-in-future-optimal-caching-algorithm/)

This topic came up in one of my lectures and I found it a little challenging to understand the proof, so I thought I would write it down as best as I could explain it to help myself and possibly others understand it better.

In a computer, there are various methods of storing information. Information can be stored in the processor cache, RAM, hard disk, etc. It can be faster to request information from a storage medium that is smaller. However, this smaller storage medium cannot fit all the possible information that can be requested. So the idea is to insert a portion of the data into the faster, smaller medium (the **cache**) and the rest into the slower, larger medium (**main memory**).

If a request is made and the data is not available in the faster, smaller medium first, then the data will be read from the slower, larger medium - this is what is known as a **cache miss**.

Given that all the data cannot possibly live in the cache, there must be a way to minimize the number of times that the data must be read from the main memory.

## Optimal Caching - Farthest-in-Future

### The Algorithm

The idea is that there is an algorithm that minimizes the number of cache misses that occur for a set of requests. The _Farthest-in-Future Algorithm_ evicts the item in the cache that is not requested until the farthest in the future. For example, given the following cache with items "a" through "f":

| Cache Items | a b c d e f |
| Future Queries | g a b c e d a b b f |

It is clear that "g" does not exist in the set of cache items and so when "g" is requested, a cache miss will result. An item will be evicted because "g" is not in the cache. According to the _Farthest-in-Future Algorithm_, element "f" will be evicted since it is the one that will be used furthest in the future.

### Definitions

- **Cache Miss** - Occurs when it is necessary to bring in an item from the main memory into the cache
- **Schedule** - A list that contains, for each request, which item is brought into the cache, and which item is evicted
- **Reduced Schedule** - A schedule that only brings in an item when there is a request for that item (so a non-reduced schedule would bring an item into the cache outside of a request for that item)

### Theorem

To be shown:

> _Farthest-in-Future_ is the optimal algorithm that minimizes the number of cache misses.

To prove this, let us say there is a schedule SFF that follows the _Farthest-in-Future Algorithm_ and that there is a schedule optimal S that has a minimum number of cache misses. It can be shown that it is possible to transform S into SFF by performing a series of evictions without increasing the number of cache misses. Since S is already optimal, and the number of cache misses did not increase, then SFF must be optimal.

To perform one transformation, the statement below can be used (it should become clearer further on):

> Let S be a reduced schedule that is the same as SFF for the first j requests, then there is a reduced schedule S' that is the same as SFF for the first j+1 requests, and incurs no more misses than S

## Proof

Let us say the cache at the start looks like this. S and SFF have the exact same contents (this is what was defined in the previous section).

| S | a b c d |
| SFF | a b c d |

Given a schedule S, it can be shown that any request can be made, and the resulting schedule would be equal to the ideal algorithm and does not increase the number of cache misses. Essentially, we want S = S' = SFF after a request is made and that the number of cache misses have not increased. If this can be shown for all different scenarios that items are requested, then _Farthest-in-Future_ is the ideal algorithm.

### Case 1: Item Is Already in the Cache

Now let us say the next item to be requested is item "d". It is clear that this item exists in both caches and no evictions are necessary. Since no evictions are necessary, SFF does not change. It was specified in a prior section that there is a schedule S' that equals SFF, which incurs no more misses than S.

| SFF | a b c d | Read d |
| S | a b c d | Read d |
| S' | a b c d | Read d |

Here, S = S' because no changes had to be made to the cache and there were no cache misses. After the request for item "d", S = S', each with zero cache misses, which is a valid outcome.

### Case 2: Item Is Not in the Cache, S and SFF Evict the Same Item

Let us say the next item to be requested is item "e". Neither cache has this item, so an eviction will have to be made. Let us also say SFF and S both choose to evict item "a" to make room for "e". It was specified in a prior section that there is a schedule S' that equals SFF, which incurs no more misses than S.

| SFF | b c d e | Evict a; Read e |
| S | b c d e | Evict a; Read e |
| S' | b c d e | Evict a; Read e |

Here S = S' because S and SFF both evicted the same item. Both S and S' each have one cache miss (no increase relative to one another), which is a valid outcome.

### Case 3: Item Is Not in the Cache, S and SFF Each Evict A Different Item

This is where the proof can become more confusing. Let us say the next item to be requested is "e". Let us also say that the ideal algorithm, SFF, evicts "a" and S evicts "b". It was specified in a prior section that there is a schedule S' that equals SFF, which incurs no more misses than S. This means that in order to get S' = SFF, S' should evict "a" in order to match with SFF.

| SFF | b c d e | Evict a; Insert e |
| S | a c d e | Evict b; Insert e |
| S' | b c d e | Evict a; Insert e |

Here, S does not agree with S' = SFF. Essentially, these two schedules behave the same, so long as future requests do not request items "a" or "b". This shows that there is a schedule S' that equals SFF, but it is not known whether or not S' has no more cache misses than S, since "a" or "b" can be requested in the future, which can determine whether S or S' has more cache misses.

From this point onward, S and S' behave the same until one of the following happens:

#### Case 3a: Item Is in SFF, But Not S; S Evicts "a"

Let us say eventually item "b" gets requested. In this case, S' and SFF do not need to change. All S has to do is evict "a" to make room for "b". In this case, S has two total cache misses (from request "e" and "b"), while SFF and S' each have only one cache miss, thus fulfilling the cache miss requirement.

| SFF | b c d e | Insert b |
| S | b c d e | Evict a; Insert b |
| S' | b c d e | Insert b |

#### Case 3b: Item Is Neither in SFF Nor S

Let us say eventually item "f" gets requested. S', SFF, and S all need to make an eviction. S' and SFF can evict "b" to make room for "f", and S can evict "a" to make room for "f". In this case, each schedule has two cache misses, thus fulfilling the cache miss requirement.

| SFF | c d e f | Evict b; Insert f |
| S | c d e f | Evict a; Insert f |
| S' | c d e f | Evict b; Insert f |

#### Case 3c: Item Is in SFF, But Not S; S Evicts Item Not Equal to "a"

Let us say eventually item "b" gets requested and S evicts an item that isn't "a", say "c". Now, SFF and S' both already have "b" in the cache. In order to synchronize S and S' to make them comparable to see how many cache misses each have, S' and SFF will evict "c" to make room for "a".

| SFF | a b d e | Evict c; Insert a |
| S | a b d e | Evict c; Insert b |
| S' | a b d e | Evict c; Insert a |

Since "a" is being brought into the cache without a request for "a", this makes S' and SFF no longer a reduced schedule. However, the proof calls for S' and SFF being a reduced schedule. Fortunately, it is possible to transform an unreduced schedule into a reduced one. In this case, each schedule has two cache misses, thus fulfilling the cache miss requirement.

#### Case 3d: Item Is Not in SFF, But in S

The only item that is in S and not SFF is item "a". SFF had evicted it initially at the beginning of Case 3. Since SFF had evicted it, it must have been the item that would be requested furthest into the future. Therefore, it is not possible for item "a" to be requested before other items.

After going through all possible eviction decisions that the schedules can do, it was shown that for each scenario, there was indeed a schedule S' = SFF, where the cache misses incurred in S' no more than S.
