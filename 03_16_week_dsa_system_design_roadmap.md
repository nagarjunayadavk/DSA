03_16_week_dsa_system_design_roadmap.md
# 16-Week Realistic Master Roadmap for Working Professionals

> **Designed for a Full-Time Working Engineer:**  
> • Weekdays: **1.5 Hours / day** (45 mins morning, 45 mins evening)  
> • Weekends: **3 to 4 Hours / day** (deep dive, design, review)  
> • Total Target: **~100–120 high-yield DSA problems + 8 LLD topics + 6 HLD topics**

---

## Daily Schedule Blueprint

```text
[WEEKDAY SCHEDULE: 1.5 Hours]
├── Morning (45 mins) : 1 New DSA Problem (Focus: Pattern Recognition, Code in Java)
└── Evening (45 mins) : Revise 1 Past Problem OR Read Java/Spring/DB Theory (30 mins) + 15 mins Git/IDE review

[WEEKEND SCHEDULE: 3.5 Hours (Saturday & Sunday)]
├── Morning (2.0 hrs) : Solve 2–3 Medium DSA Problems under 30-min timer
└── Afternoon (1.5 hrs): Low-Level Design (Saturday) / High-Level System Design (Sunday)
```

---

## Phase 1: Core Patterns & Linear Structures (Weeks 1 – 4)

### Week 1: Arrays & Hashing
- [ ] Read Pattern 1 & Pattern 2 from `01_14_algorithmic_patterns_guide.md`
- [ ] [LC 217] Contains Duplicate (Easy)
- [ ] [LC 242] Valid Anagram (Easy)
- [ ] [LC 1] Two Sum (Easy)
- [ ] [LC 49] Group Anagrams (Medium)
- [ ] [LC 347] Top K Frequent Elements (Medium)
- [ ] [LC 238] Product of Array Except Self (Medium)
- [ ] **Theory Deep Dive:** `HashMap` internals in Java 17 (Buckets, Hash collisions, Red-Black Tree threshold 8).

### Week 2: Two Pointers & In-Place Array Ops
- [ ] [LC 125] Valid Palindrome (Easy)
- [ ] [LC 167] Two Sum II - Input Array Is Sorted (Medium)
- [ ] [LC 15] 3Sum (Medium)
- [ ] [LC 11] Container With Most Water (Medium)
- [ ] [LC 42] Trapping Rain Water (Hard - study the two-pointer approach)
- [ ] **Theory Deep Dive:** Java String immutability, `StringBuilder`, and memory footprint.

### Week 3: Sliding Window
- [ ] [LC 121] Best Time to Buy and Sell Stock (Easy)
- [ ] [LC 3] Longest Substring Without Repeating Characters (Medium)
- [ ] [LC 424] Longest Repeating Character Replacement (Medium)
- [ ] [LC 567] Permutation in String (Medium)
- [ ] [LC 76] Minimum Window Substring (Hard)
- [ ] **Theory Deep Dive:** `ConcurrentHashMap` vs `Collections.synchronizedMap()` and segment locking.

### Week 4: Stack & Monotonic Stack
- [ ] [LC 20] Valid Parentheses (Easy)
- [ ] [LC 155] Min Stack (Medium)
- [ ] [LC 150] Evaluate Reverse Polish Notation (Medium)
- [ ] [LC 739] Daily Temperatures (Medium - Monotonic Stack)
- [ ] [LC 84] Largest Rectangle in Histogram (Hard - Monotonic Stack)
- [ ] **Theory Deep Dive:** Java Memory Model (Stack frames vs Heap memory, `StackOverflowError` causes).

---

## Phase 2: Non-Linear Structures & Search (Weeks 5 – 8)

### Week 5: Binary Search & Modified Binary Search
- [ ] [LC 704] Binary Search (Easy)
- [ ] [LC 74] Search a 2D Matrix (Medium)
- [ ] [LC 153] Find Minimum in Rotated Sorted Array (Medium)
- [ ] [LC 33] Search in Rotated Sorted Array (Medium)
- [ ] [LC 875] Koko Eating Bananas (Medium - Binary Search on Answer)
- [ ] **Theory Deep Dive:** Thread safety in Java, volatile variables, and atomic classes (`AtomicInteger`).

### Week 6: Linked Lists (Cycle Detection & In-Place Reversals)
- [ ] [LC 206] Reverse Linked List (Easy)
- [ ] [LC 21] Merge Two Sorted Lists (Easy)
- [ ] [LC 141] Linked List Cycle (Easy)
- [ ] [LC 142] Linked List Cycle II (Medium)
- [ ] [LC 143] Reorder List (Medium)
- [ ] [LC 19] Remove Nth Node From End of List (Medium)
- [ ] **Theory Deep Dive:** Java Garbage Collection roots, Reference types (Strong, Soft, Weak, Phantom).

### Week 7: Trees & Binary Search Trees (DFS)
- [ ] [LC 226] Invert Binary Tree (Easy)
- [ ] [LC 104] Maximum Depth of Binary Tree (Easy)
- [ ] [LC 543] Diameter of Binary Tree (Easy)
- [ ] [LC 100] Same Tree (Easy)
- [ ] [LC 572] Subtree of Another Tree (Easy)
- [ ] [LC 235] Lowest Common Ancestor of a BST (Medium)
- [ ] [LC 98] Validate Binary Search Tree (Medium)
- [ ] **Theory Deep Dive:** Spring `@Transactional` propagation (`REQUIRED`, `REQUIRES_NEW`) and rollback rules.

### Week 8: Trees BFS & Level Order
- [ ] [LC 102] Binary Tree Level Order Traversal (Medium)
- [ ] [LC 199] Binary Tree Right Side View (Medium)
- [ ] [LC 103] Binary Tree Zigzag Level Order Traversal (Medium)
- [ ] [LC 230] Kth Smallest Element in a BST (Medium)
- [ ] [LC 105] Construct Binary Tree from Preorder and Inorder Traversal (Medium)
- [ ] **Theory Deep Dive:** Spring Bean Lifecycle, Circular Dependency resolution, and AOP proxies.

---

## Phase 3: Graphs, Heaps & Low-Level Design (Weeks 9 – 12)

### Week 9: Heaps / Priority Queue & Merge Intervals
- [ ] [LC 56] Merge Intervals (Medium)
- [ ] [LC 57] Insert Interval (Medium)
- [ ] [LC 215] Kth Largest Element in an Array (Medium)
- [ ] [LC 973] K Closest Points to Origin (Medium)
- [ ] [LC 621] Task Scheduler (Medium)
- [ ] [LC 295] Find Median from Data Stream (Hard - Two Heaps)
- [ ] **LLD Topic 1:** Design an **LRU Cache** (HashMap + Doubly Linked List, LeetCode 146).

### Week 10: Graph BFS & DFS
- [ ] [LC 200] Number of Islands (Medium)
- [ ] [LC 695] Max Area of Island (Medium)
- [ ] [LC 133] Clone Graph (Medium)
- [ ] [LC 994] Rotting Oranges (Medium - Multi-source BFS)
- [ ] [LC 417] Pacific Atlantic Water Flow (Medium)
- [ ] **LLD Topic 2:** Design a **Rate Limiter** (Token Bucket, Leaky Bucket, Sliding Window Counter).

### Week 11: Advanced Graphs (Topological Sort & Disjoint Set)
- [ ] [LC 207] Course Schedule (Medium)
- [ ] [LC 210] Course Schedule II (Medium)
- [ ] [LC 684] Redundant Connection (Medium - Union Find)
- [ ] [LC 261] Graph Valid Tree (Medium)
- [ ] **LLD Topic 3:** Design a **Notification Service** (Strategy pattern for Email, SMS, Push; asynchronous worker pool).

### Week 12: Backtracking & Dynamic Programming Basics
- [ ] [LC 78] Subsets (Medium)
- [ ] [LC 39] Combination Sum (Medium)
- [ ] [LC 46] Permutations (Medium)
- [ ] [LC 70] Climbing Stairs (Easy)
- [ ] [LC 198] House Robber (Medium)
- [ ] [LC 322] Coin Change (Medium)
- [ ] **LLD Topic 4:** Design an **Enterprise RBAC Permission System** (Role, Group, Page, Action models, Decorator/Composite patterns).

---

## Phase 4: High-Level Design (HLD) & Interview Execution (Weeks 13 – 16)

### Week 13: Distributed Caching & Database Scaling
- [ ] **HLD Topic 1:** Design a **Distributed Cache System** (Redis Cluster, Cache-Aside, Write-Through, Cache Stampede, TTL, Eviction policies).
- [ ] **HLD Topic 2:** Database Sharding, Replication, Consistency models (CAP Theorem, PACELC, Read Replicas, Connection Pooling with HikariCP).
- [ ] Solve 3 Random LeetCode Mediums under 25-minute timers.

### Week 14: Messaging & Event-Driven Architecture
- [ ] **HLD Topic 3:** Design a **Distributed Message Queue / Pub-Sub (Kafka / RabbitMQ)** (Partitioning, consumer groups, offset management, dead-letter queues).
- [ ] **HLD Topic 4:** Design a **URL Shortener (TinyURL)** (Hashing algorithms, Base62 encoding, unique ID generation via Snowflake ID).
- [ ] Solve 3 Random LeetCode Mediums.

### Week 15: Full System Design Case Studies & Resume Launch
- [ ] **HLD Topic 5:** Design an **Ad Targeting, Audience Segmentation & Attribution Analytics Platform** (Map directly to your AdTS experience!).
- [ ] **HLD Topic 6:** Design an **E-Commerce Flash Sale System** (Distributed locking with Redisson, concurrency handling, database race conditions).
- [ ] Update Resume with bullet points from `02_resume_project_description_and_experience.md`.
- [ ] Polish LinkedIn profile, update headline: *"Senior Full-Stack Software Engineer | Java 17 | Spring Boot | React | Distributed Caching"*.

### Week 16: Mock Interviews & Active Applications
- [ ] Conduct 2 Mock DSA rounds (Pramp.com or with a peer).
- [ ] Conduct 1 Mock System Design round.
- [ ] Prepare STAR behavioral stories using `05_system_design_and_behavioral_interview_prep.md`.
- [ ] Apply to 10–15 target companies (referrals preferred via LinkedIn outreach to engineering managers).
