# Daily Roadmap — 3 місяці до Senior Java

> **Профіль:** 4+ років досвіду, фултайм підготовка (6-8 год/день)  
> **Ринок:** EU remote, UA product, стартапи  
> **Стратегія:** ти вже знаєш основи — фокус на ГЛИБИНУ, ПРОЕКТ і ПОЯСНЕННЯ вголос  

> Відкривай цей файл кожного ранку. Знайди свій тиждень. Після виконання — ✅.  
> Раз на тиждень онови статуси в відповідних MD файлах.

---

## ⏰ Структура дня (6-8 годин)

| Час | Активність | Тривалість |
|-----|-----------|-----------|
| Ранок | LeetCode (1 задача) + flashcard повторення | 1 год |
| До обіду | Теорія (вивчення або mock) | 1.5-2 год |
| Після обіду | Проект з Claude Code | 2-3 год |
| Вечір | Англійська: пояснення теми вголос або STAR practice | 30 хв |
| **З тижня 7** | Подача резюме + cover letters | +1 год |

---

## 🗓 МІСЯЦЬ 1 — Фундамент + Проект до MVP

### Тиждень 1 — Java Collections швидко + Project Scaffold
> Мета: прогнати колекції за 2 дні (повторення, не вивчення з нуля), запустити проект

| День | Теорія (1.5 год) | Проект (2-3 год) | LeetCode (1 год) |
|------|------------------|------------------|-------------------|
| Пн | HashMap deep: bucket, hash, treeify, resize. LinkedHashMap, TreeMap | Spring Boot scaffold, Docker Compose (PostgreSQL + Redis + Kafka) | Two Pointers: Valid Palindrome |
| Вт | equals/hashCode контракт. Generics: PECS, type erasure | Poi entity, PoiCategory enum, PoiRepository | Two Pointers: 3Sum |
| Ср | Iterator fail-fast, Collections.unmodifiableList vs List.of | PoiService, PoiController, DTOs (PoiRequest/Response) | Two Pointers: Container With Most Water |
| Чт | Stream API: collectors (groupingBy, toMap), flatMap | GlobalExceptionHandler, Swagger, validation (@Valid) | Sliding Window: Longest Substring |
| Пт | Optional antipatterns, Java 21: Records, Sealed, Pattern matching | Фільтрація POI (city, category), пагінація (Pageable) | Sliding Window: Max Subarray |
| Сб | Exception handling: checked vs unchecked, try-with-resources | JWT Auth: User entity, register, login, JwtAuthFilter | Intervals: Merge Intervals |
| Нд | **Self-check:** поясни HashMap + Stream API вголос за 5 хв | Протестуй всі endpoints через Swagger | — |

### Тиждень 2 — Concurrency + Route Entities
> Мета: Concurrency — найважливіша тема Core Java, route CRUD готовий

| День | Теорія | Проект | LeetCode |
|------|--------|--------|----------|
| Пн | Thread lifecycle, volatile, happens-before rules | Route + RouteStop entities, repositories | Fast & Slow: Linked List Cycle |
| Вт | synchronized, Java Memory Model, deadlock | RouteService: basic save, get, delete | Binary Search: Search Rotated Array |
| Ср | ReentrantLock, StampedLock, AtomicInteger, CAS | RouteController: POST/GET/DELETE endpoints | Binary Search: Find Peak Element |
| Чт | ExecutorService, ThreadPoolExecutor параметри | GET /users/me/routes (history з пагінацією) | BFS: Level Order Traversal |
| Пт | CompletableFuture chaining, exception handling | Unit тести PoiService (JUnit 5 + Mockito) | BFS: Rotting Oranges |
| Сб | ConcurrentHashMap, Virtual Threads (Java 21) | @WebMvcTest для PoiController | — |
| Нд | **Mock #1:** Core Java питання з Claude (30 хв) | Code review всього коду → рефактор | — |

### Тиждень 3 — JVM + Route Optimizer (KEY WEEK)
> Мета: RouteOptimizer — серце проекту, має бути бездоганним

| День | Теорія | Проект | LeetCode |
|------|--------|--------|----------|
| Пн | JVM memory model: heap, stack, metaspace | HaversineCalculator + unit тести | DFS: Number of Islands |
| Вт | GC: G1 deep (regions, mixed GC, humongous), ZGC basics | NearestNeighborStrategy + unit тести | DFS: Permutations |
| Ср | Class loading, JIT, escape analysis | TwoOptStrategy + unit тести | DFS: Word Search |
| Чт | Memory leaks: типові причини, profiling tools | TimelineBuilder (assign times, travel time) | DP: Climbing Stairs |
| Пт | Reflection, Annotations — як Spring їх використовує | Opening hours validation + warning system | DP: Coin Change |
| Сб | Design Patterns в проекті: Strategy, Builder, Proxy | RouteOptimizer orchestrator + POST /routes/optimize | — |
| Нд | SOLID через призму свого проекту | **Тестування optimizer:** 5 POI → перевір розклад | — |

### Тиждень 4 — Spring Deep + Polish Optimizer
> Мета: Spring internals на senior рівні, optimizer battle-tested

| День | Теорія | Проект | LeetCode |
|------|--------|--------|----------|
| Пн | Spring IoC: BeanFactory vs ApplicationContext, lifecycle, BeanPostProcessor | fixedTime stops logic в optimizer | DP: House Robber |
| Вт | Bean scopes (prototype в singleton pitfall), @Conditional, @Profile | Integration тести optimizer (edge cases: порожній маршрут, 1 stop, overflow) | DP: LCS |
| Ср | Spring AOP: JDK vs CGLIB, self-invocation, @Around | Logging aspect для RouteOptimizer (час виконання) | Greedy: Jump Game |
| Чт | @Transactional deep: propagation, rollback rules, readOnly | @Transactional в RouteService, тест rollback behavior | Greedy: Meeting Rooms II |
| Пт | Spring Boot autoconfiguration, @SpringBootApplication internals | Profiles: dev/prod конфігурація, application-dev.yml | Greedy: Task Scheduler |
| Сб | Serialization: Jackson deep, custom serializers, @JsonView | Рефактор DTOs, Jackson конфігурація для openingHours JSON | — |
| Нд | **Mock #2:** Spring + Hibernate питання (30 хв) | Підсумок місяця: що зроблено, що ні | — |

---

## 🗓 МІСЯЦЬ 2 — Глибина + Повна функціональність

### Тиждень 5 — Hibernate Deep + Redis
> Мета: N+1 знайти і виправити, Redis працює

| День | Теорія | Проект | LeetCode |
|------|--------|--------|----------|
| Пн | Entity lifecycle, persistence context, dirty checking | spring.jpa.show-sql=true → знайди N+1 → виправ | Heap: Top K Frequent |
| Вт | LAZY vs EAGER, @EntityGraph, @BatchSize, JOIN FETCH | @EntityGraph для Route → stops → poi | Heap: Merge K Sorted Lists |
| Ср | @Version (optimistic locking), CascadeType, orphanRemoval | @Version в Route, тест concurrent update | Monotonic Stack: Daily Temperatures |
| Чт | L1/L2 кеш Hibernate, Spring Data Specifications | Redis підключення, @Cacheable на POI by city | Trie: Implement Trie |
| Пт | Liquibase міграції, zero-downtime migration patterns | @CacheEvict при оновленні рейтингу, TTL config | Trie: Word Search II |
| Сб | — | Liquibase міграції для всіх таблиць | — |
| Нд | **Self-check:** поясни N+1 + 3 способи вирішення | Перевір Redis працює: cache hit в логах | — |

### Тиждень 6 — SQL + Kafka + Google Places
> Мета: всі інтеграції працюють

| День | Теорія | Проект | LeetCode |
|------|--------|--------|----------|
| Пн | B-tree index, composite index, left-prefix rule | Додай індекси, EXPLAIN ANALYZE на 5 запитів | Union-Find: Connected Components |
| Вт | Window functions, CTE, MVCC | Kafka: RouteEventProducer (route.created) | Graph: Network Delay (Dijkstra) |
| Ср | Isolation levels, deadlock detection, SELECT FOR UPDATE | Kafka: RouteEventConsumer (log + aggregate rating) | Graph: Course Schedule |
| Чт | HikariCP tuning, connection pool sizing | Google Places: PlacesApiClient, GET /pois/search | 1 random medium |
| Пт | Kafka: partitions, consumer groups, exactly-once | Rating module: POST /pois/{id}/rate | 1 random medium |
| Сб | — | Share module: generate token, GET /routes/shared/{token} | — |
| Нд | **Mock #3:** DB + Redis + Kafka питання | Повний flow test: create POI → optimize route → share | — |

### Тиждень 7 — Testing + System Design + ПОЧИНАЙ ПОДАВАТИСЬ
> **MILESTONE:** починай подаватись на вакансії. Не чекай "поки готовий" — interview процес займає 2-4 тижні.

| День | Теорія | Проект | LeetCode | Job search |
|------|--------|--------|----------|------------|
| Пн | Testing: @SpringBootTest, @WebMvcTest, @DataJpaTest, @MockBean | Testcontainers: PostgreSQL integration test | 1 medium | Онови LinkedIn |
| Вт | Testcontainers: Redis, Kafka | Integration тести для повного route flow | 1 medium | Резюме ready |
| Ср | System Design: CAP, back-of-envelope, latency numbers | MockMvc тести для всіх контролерів | 1 medium | 3-5 applications |
| Чт | System Design: load balancer, rate limiting, CDN | — | 1 medium | — |
| Пт | **SD Practice:** URL Shortener (45 хв вголос) | — | — | 3-5 applications |
| Сб | — | Dockerfile, docker-compose prod, actuator health | — | — |
| Нд | Розбір SD задачі з Claude — де gaps | — | — | — |

### Тиждень 8 — System Design + Deploy
| День | Теорія | Проект | LeetCode | Job search |
|------|--------|--------|----------|------------|
| Пн | Мікросервіси: Saga, Outbox, Circuit Breaker | GitHub Actions: build + test | 1 medium | 3-5 applications |
| Вт | Database per service, CQRS, Event Sourcing | Deploy на Railway/Render | 1 medium | — |
| Ср | **SD Practice:** Chat система (45 хв) | GitHub Actions: auto-deploy | 1 medium | — |
| Чт | REST vs gRPC vs GraphQL, idempotency | README: архітектура, як запустити, скріншоти | 1 medium | 3-5 applications |
| Пт | Observability: metrics, traces, structured logging | Swagger: всі endpoints з описами | — | — |
| Сб | — | Фінальний polish проекту | — | — |
| Нд | **Mock #4:** System Design — "масштабуй Tourist API до 1M users" | — | — | — |

---

## 🗓 МІСЯЦЬ 3 — Interviews + Polish

### Тиждень 9 — English + Behavioral prep
| День | Теорія | English/Behavioral | LeetCode |
|------|--------|-------------------|----------|
| Пн | Повторення слабких тем з Java Core | Tell me about yourself — напиши, переклади, тренуй | 1 medium |
| Вт | Повторення слабких тем Spring | Elevator pitch проекту (30 сек) англійською | 1 medium |
| Ср | Повторення слабких тем DB | 4 STAR stories — напиши, переклади | 1 medium |
| Чт | — | **Mock behavioral англійською** (30 хв з Claude) | 1 medium |
| Пт | — | Questions to ask + salary negotiation prep | — |
| Сб | — | Пояснити 3 теми англійською (HashMap, @Transactional, проект) | — |
| Нд | — | **Mock #5:** повний технічний mock англійською (1 год) | — |

### Тиждень 10 — Full Mock Week
| День | Активність (весь день) |
|------|----------------------|
| Пн | Mock: Java Core (1 год) + LeetCode medium під таймер (35 хв) |
| Вт | Mock: Spring + Hibernate (1 год) + LeetCode medium |
| Ср | Mock: System Design (45 хв) + DB питання (30 хв) |
| Чт | Mock: Behavioral англійською (30 хв) + Project deep dive (30 хв) |
| Пт | Mock: ПОВНИЙ interview loop (2-3 години) — behavioral → coding → system design |
| Сб | Повторення gap'ів знайдених за тиждень |
| Нд | Mock з живою людиною (Pramp / interviewing.io) |

### Тижні 11-12 — Active Interview Mode
> Пріоритет: реальні співбесіди > підготовка

**Щодня:**
- Ранок: 1 LeetCode medium (30 хв таймер) — maintenance
- Перед кожною співбесідою: перечитай відповідні MD файли
- Після кожної співбесіди: запиши питання і свої слабкі відповіді → targeted review
- 1 mock на тиждень (Pramp або Claude)
- Продовжуй подаватись: 5-10 applications на тиждень

---

## 📌 Правила

1. **Проект > Теорія** — якщо мало часу, працюй над проектом
2. **Вголос > В голові** — пояснюй кожну тему вголос (англійською з тижня 9)
3. **Не відставай більше ніж на 2 дні** — краще скороти день, ніж пропустити
4. **З тижня 7 подавайся!** — interview pipeline = 2-4 тижні, не чекай
5. **Mock interviews з місяця 2** — не "поки буду готовий", а прямо зараз
6. **Після кожного тижня** — 15 хв: онови статуси в MD файлах, запиши gap'и
7. **Якщо тема дається важко** — витрать ще день, але не більше двох

---

## 📊 Weekly Review Template

Кожної неділі заповнюй:

```
## Тиждень X Review
Дата: ___

### Що зроблено:
- Теорія: 
- Проект: 
- LeetCode: X задач (__ easy, __ medium)
- Mock interviews: 

### Gap'и знайдені:
- 

### План на наступний тиждень:
- Priority 1: 
- Priority 2: 
- Priority 3: 

### Applications sent: __
### Interviews scheduled: __
```
