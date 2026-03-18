# LeetCode & Алгоритми — Підготовка до співбесіди
**Чат для:** алгоритми, структури даних, розбір задач  
**Рівень цілі:** впевнений Medium, базовий Hard  
**Ринок:** EU/UA product + startups (не FAANG — фокус на патерни, не на кількість)  
**Як використовувати:** вставити цей файл на початку сесії, попросити оновити в кінці

---

## Як починати сесію
- *"Дай мені medium задачу по sliding window, я вирішу, потім розбираємо"*
- *"Я вирішив цю задачу [вставити код] — зроби code review, покажи оптимальніше рішення"*
- *"Поясни мені патерн Two Pointers з прикладами"*
- *"Симулюй coding interview: 35 хвилин, 1 задача, задавай уточнюючі питання"*

---

## Стратегія

Для EU/UA/стартап ринку:
- **Патерни > кількість.** Краще знати 13 патернів впевнено, ніж вирішити 80 задач механічно
- **Thinking out loud** важливіший за оптимальне рішення
- **Brute force → optimize** — завжди починай з робочого рішення
- Більшість компаній дають 1-2 medium задачі, рідко hard
- Вміти пояснити Big-O і trade-offs — обов'язково

---

## Патерни (вивчати в такому порядку)

| # | Патерн | Статус | Задачі для закріплення |
|---|--------|--------|----------------------|
| 1 | Two Pointers | 🔴 | Valid Palindrome, Two Sum II, 3Sum, Container With Most Water |
| 2 | Sliding Window | 🔴 | Max Subarray (Kadane's), Longest Substring Without Repeating, Minimum Window Substring |
| 3 | Fast & Slow Pointers | 🔴 | Linked List Cycle, Linked List Cycle II, Find Middle, Happy Number |
| 4 | Binary Search | 🔴 | Search in Rotated Array, Find Peak Element, Koko Eating Bananas |
| 5 | BFS / Level-order | 🔴 | Level Order Traversal, Shortest Path in Grid, Rotting Oranges |
| 6 | DFS / Backtracking | 🔴 | Permutations, Subsets, Word Search, Number of Islands |
| 7 | Dynamic Programming | 🔴 | Climbing Stairs, Coin Change, Longest Common Subsequence, House Robber |
| 8 | Greedy | 🔴 | Jump Game, Meeting Rooms II, Task Scheduler |
| 9 | Heap / Priority Queue | 🔴 | K Largest Elements, Merge K Sorted Lists, Top K Frequent Elements |
| 10 | Monotonic Stack | 🔴 | Next Greater Element, Daily Temperatures, Trapping Rain Water |
| 11 | **Intervals** | 🔴 | Merge Intervals, Insert Interval, Meeting Rooms, Non-overlapping Intervals |
| 12 | **Trie** | 🔴 | Implement Trie, Word Search II, **Search Autocomplete** (зв'язок з проектом!) |
| 13 | **Union-Find** | 🔴 | Number of Connected Components, Redundant Connection |
| 14 | Graph (Dijkstra, Topological Sort) | 🔴 | Network Delay Time, Course Schedule I & II |

---

## Структури даних

| Структура | Статус | Ключове |
|-----------|--------|---------|
| Array, Dynamic Array | 🔴 | Amortized O(1) append, O(n) insert at index |
| Linked List (singly, doubly) | 🔴 | O(1) insert/delete at known position |
| Stack, Queue, Deque | 🔴 | Stack = DFS, Queue = BFS, Deque = sliding window |
| Binary Tree, BST | 🔴 | Inorder BST = sorted, balanced BST = O(log n) |
| Heap (min/max) | 🔴 | O(log n) insert/extract, O(1) peek |
| HashMap / HashSet | 🔴 | O(1) average, O(n) worst case |
| **Trie** | 🔴 | Prefix search O(m), autocomplete |
| Graph (adjacency list) | 🔴 | BFS/DFS O(V+E) |
| **Disjoint Set (Union-Find)** | 🔴 | Nearly O(1) with path compression + union by rank |

---

## Реалістична ціль

| Рівень | Ціль | Призначення |
|--------|------|-------------|
| Easy | ~15 задач | Розминка, впевненість, edge cases |
| Medium | ~30 задач | Основний фокус, 2-3 на кожен патерн |
| Hard | ~5 задач | Розуміння підходу, не обов'язково вирішити за 30 хв |
| **Всього** | **~50 задач** | |

---

## Вирішені задачі

| # | Назва | Рівень | Патерн | Час | Підказка? | Повторено? | Нотатки |
|---|-------|--------|--------|-----|-----------|------------|---------|
| | | | | | | | |

---

## Правила роботи з задачами

1. **Таймер 25-30 хв** — якщо не вирішив, дивишся hints (не відразу повне рішення)
2. **Завжди думай вголос** — навіть коли один: проговорюй підхід, edge cases
3. **Послідовність:** зрозумій задачу → brute force → оптимізуй → код → тести
4. **Після рішення:** Big-O time + space, чи є краще, edge cases які пропустив
5. **Spaced repetition:**
   - Через 1 день: переглянь рішення (не вирішуй, тільки прочитай)
   - Через 3 дні: виріши заново без підказок
   - Через 7 днів: виріши заново — якщо ОК → ✅, якщо ні → ⚠️ повтори ще раз
6. **Java конкретно:** використовуй Java для всіх задач, знай API (PriorityQueue, Deque, Map.getOrDefault)

---

## Template для coding interview

```
1. "Let me make sure I understand the problem..." (перефразуй)
2. "Can I clarify: [edge cases? constraints? sorted input?]"
3. "My initial approach would be... [brute force, O(?)]"
4. "We can optimize this using [pattern], which gives us O(?)"
5. Code
6. "Let me trace through with an example..."
7. "Edge cases: empty input, single element, all same values..."
8. "Time complexity is O(?), space is O(?)"
```

---

## ⚠️ Задачі де застрягав
| Задача | Патерн | Що не зрозумів | Дата повторення |
|--------|--------|----------------|-----------------|
| | | | |

---

## 📊 Статистика
| Тиждень | Easy | Medium | Hard | Патерни | Нотатки |
|---------|------|--------|------|---------|---------|
| | | | | | |

---

## 📋 Покроковий план

### Блок 1 — Two Pointers + Sliding Window + Intervals (Тиждень 1-2)
**6 задач, ~2 на день:**
1. Two Sum II (Easy, Two Pointers) → 3Sum (Medium) → Container With Most Water (Medium)
2. Longest Substring Without Repeating (Medium, Sliding Window) → Max Subarray (Medium, Kadane)
3. Merge Intervals (Medium, Intervals) → Insert Interval (Medium)
4. **Check:** можеш розпізнати коли Two Pointers, коли Sliding Window, коли Intervals

### Блок 2 — Fast/Slow + Binary Search (Тиждень 2-3)
**5 задач:**
1. Linked List Cycle + Cycle II (Fast & Slow)
2. Search in Rotated Array + Find Peak Element (Binary Search)
3. Koko Eating Bananas (Binary Search on answer — нетиповий!)
4. **Check:** binary search on answer — розумієш template

### Блок 3 — BFS + DFS + Backtracking (Тиждень 3-4)
**7 задач:**
1. Number of Islands (DFS on grid), Rotting Oranges (BFS on grid)
2. Level Order Traversal (BFS on tree)
3. Permutations, Subsets (Backtracking)
4. Word Search (DFS + Backtracking)
5. Course Schedule (Topological Sort)
6. **Check:** вмієш розрізнити коли BFS, коли DFS

### Блок 4 — DP + Greedy (Тиждень 4-5)
**7 задач:**
1. Climbing Stairs, House Robber (1D DP)
2. Coin Change, Longest Common Subsequence (2D DP)
3. Jump Game (Greedy), Meeting Rooms II (Greedy + Heap)
4. Task Scheduler (Greedy)
5. **Key insight:** DP = overlapping subproblems, Greedy = local optimal = global optimal

### Блок 5 — Heap + Monotonic Stack + Trie + Union-Find (Тиждень 5-6)
**8 задач:**
1. Top K Frequent (Heap), Merge K Sorted Lists (Heap)
2. Daily Temperatures, Next Greater Element (Monotonic Stack)
3. Implement Trie, Word Search II (Trie) → **search autocomplete в проекті!**
4. Number of Connected Components, Redundant Connection (Union-Find)
5. **Check:** вмієш реалізувати Trie і Union-Find з нуля

### Блок 6 — Dijkstra + Mock Interviews (Тиждень 6-7)
**5 задач + mocks:**
1. Network Delay Time (Dijkstra) → **зв'язок з RouteOptimizer в проекті**
2. 3-5 random medium задач як mock (таймер 35 хв, think aloud)
3. **Key:** пояснюй рішення вголос, пиши clean code, handle edge cases

### Після основного блоку — Maintenance mode
- 1 random medium задача на день (15-20 хв)
- Повторення ⚠️ задач кожні 3 дні
- 1 mock на тиждень (Pramp або Claude)
