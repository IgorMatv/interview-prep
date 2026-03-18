# Бази даних — Підготовка до співбесіди
**Чат для:** SQL, індекси, PostgreSQL, Redis, Kafka, NoSQL  
**Рівень цілі:** Senior  
**Як використовувати:** вставити цей файл на початку сесії, попросити оновити в кінці

---

## Як починати сесію
- *"Дай мені складний SQL запит, я розв'яжу, а ти оціниш і покажеш оптимальніший варіант"*
- *"Поясни мені як B-tree індекс працює зсередини"*
- *"Задай питання по транзакціях рівня Senior"*
- *"Покажи приклад де індекс не використовується і поясни чому"*

---

## Критерії готовності

- 🟢 Можу написати запит/пояснити концепцію + знаю edge cases + можу обґрунтувати рішення
- 🟡 Знаю теорію, але не впевнений в практичному застосуванні
- 🔴 Потребує вивчення

---

## Теми та прогрес

### 📐 Database Design
| Тема | Статус | Нотатки |
|------|--------|---------|
| Нормалізація: 1NF → 2NF → 3NF → BCNF — коли і навіщо | 🔴 | |
| Денормалізація — коли виправдана, trade-offs | 🔴 | |
| ER діаграми — вміти намалювати для свого проекту | 🔴 | |
| Вибір типів даних: коли DECIMAL vs FLOAT, VARCHAR vs TEXT, TIMESTAMP vs TIMESTAMPTZ | 🔴 | |

### 📊 SQL
| Тема | Статус | Нотатки |
|------|--------|---------|
| JOIN types: INNER, LEFT, RIGHT, FULL, CROSS, SELF — коли який | 🔴 | |
| Subqueries vs JOIN — перформанс і коли що краще | 🔴 | |
| Correlated subquery vs non-correlated — різниця в execution | 🔴 | |
| Window functions: ROW_NUMBER, RANK, DENSE_RANK, LAG, LEAD, SUM/AVG OVER | 🔴 | |
| GROUP BY, HAVING, DISTINCT — порядок виконання SQL | 🔴 | |
| CTE (WITH clause) — рекурсивні CTE (tree structures) | 🔴 | |
| UPSERT (INSERT ON CONFLICT DO UPDATE) | 🔴 | |
| COALESCE, NULLIF, CASE WHEN — обробка NULL | 🔴 | |
| Порядок виконання SQL: FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT | 🔴 | |

### 🐘 PostgreSQL специфіка
| Тема | Статус | Нотатки |
|------|--------|---------|
| JSONB — операції, індексування (GIN index), коли використовувати | 🔴 | |
| Arrays — коли масив в колонці OK, коли потрібна окрема таблиця | 🔴 | |
| Full-text search (tsvector, tsquery, GIN) — альтернатива Elasticsearch для простих кейсів | 🔴 | |
| SERIAL vs IDENTITY vs UUID — вибір primary key стратегії | 🔴 | |
| PostgreSQL extensions: PostGIS (geo), pg_trgm (fuzzy search) | 🔴 | |
| VACUUM, ANALYZE, autovacuum — навіщо і як моніторити | 🔴 | |

### 🔍 Індекси
| Тема | Статус | Нотатки |
|------|--------|---------|
| B-tree індекс — структура, balanced tree, page-level storage | 🔴 | |
| Hash index — коли використовувати (тільки equality, не range) | 🔴 | |
| GIN index — для JSONB, arrays, full-text search | 🔴 | |
| GiST index — для геоданих (PostGIS) | 🔴 | |
| Composite index — порядок колонок, left-prefix rule | 🔴 | |
| Covering index (INCLUDE, index-only scan) | 🔴 | |
| Partial index (WHERE clause в CREATE INDEX) | 🔴 | |
| Expression index (на функцію, напр. LOWER(email)) | 🔴 | |
| Коли індекс НЕ використовується: функція на колонку, OR, low cardinality, small table | 🔴 | |
| EXPLAIN ANALYZE — читати execution plan (Seq Scan, Index Scan, Bitmap, Nested Loop, Hash Join) | 🔴 | |
| Index bloat, REINDEX, VACUUM, pg_stat_user_indexes | 🔴 | |

### 🔒 Транзакції та Concurrency
| Тема | Статус | Нотатки |
|------|--------|---------|
| ACID — пояснити кожну літеру з прикладом | 🔴 | |
| Isolation levels: READ UNCOMMITTED → READ COMMITTED → REPEATABLE READ → SERIALIZABLE | 🔴 | |
| Аномалії: dirty read, non-repeatable read, phantom read, serialization anomaly | 🔴 | |
| PostgreSQL default isolation: READ COMMITTED — що це означає практично | 🔴 | |
| Deadlock у БД — як виявити (pg_stat_activity), як вирішити, prevention strategies | 🔴 | |
| SELECT FOR UPDATE, SELECT FOR SHARE, SKIP LOCKED — use cases | 🔴 | |
| Advisory locks — коли потрібні (route optimization lock?) | 🔴 | |
| Optimistic locking (version column) vs pessimistic (SELECT FOR UPDATE) | 🔴 | |
| MVCC — як PostgreSQL реалізує: xmin/xmax, tuple visibility, snapshot | 🔴 | |

### ⚡ Оптимізація та масштабування
| Тема | Статус | Нотатки |
|------|--------|---------|
| Query optimization — типові прийоми (avoid SELECT *, use specific columns) | 🔴 | |
| N+1 на рівні SQL (batch queries vs loop queries) | 🔴 | |
| Connection pooling (HikariCP) — sizing formula, min/max idle, leak detection | 🔴 | |
| Vertical vs horizontal scaling — trade-offs | 🔴 | |
| Replication: streaming replication (async/sync), logical replication | 🔴 | |
| Read replicas — consistency concerns, replication lag | 🔴 | |
| Sharding — стратегії (hash, range, directory), resharding проблема | 🔴 | |
| Table partitioning — range, list, hash partitioning в PostgreSQL | 🔴 | |
| Zero-downtime migrations: expand-contract pattern, backward compatible changes | 🔴 | |
| Database connection management в мікросервісах | 🔴 | |

### 🔴 Redis
| Тема | Статус | Нотатки |
|------|--------|---------|
| Структури даних: String, Hash, List, Set, Sorted Set (ZSet) — коли яку | 🔴 | |
| TTL і eviction policies (LRU, LFU, noeviction) — як обрати | 🔴 | |
| Кешування паттерни: Cache-Aside, Write-Through, Write-Behind — trade-offs кожного | 🔴 | |
| Cache stampede / thundering herd — як запобігти (locking, probabilistic early expiry) | 🔴 | |
| Redis Pub/Sub vs Streams | 🔴 | |
| Redis як distributed lock (Redlock алгоритм, Redisson) — проблеми і альтернативи | 🔴 | |
| Persistence: RDB snapshots vs AOF append — trade-offs | 🔴 | |
| Redis Cluster: hash slots, failover, client-side awareness | 🔴 | |
| Redis memory management: maxmemory, fragmentation | 🔴 | |

### 📨 Kafka
| Тема | Статус | Нотатки |
|------|--------|---------|
| Topic, partition, offset — зв'язок між ними | 🔴 | |
| Producer: acks (0, 1, all), retries, idempotence (enable.idempotence=true) | 🔴 | |
| Consumer groups, partition assignment strategies, rebalancing | 🔴 | |
| At-least-once vs at-most-once vs exactly-once semantics | 🔴 | |
| Consumer offset management: auto commit vs manual commit | 🔴 | |
| Kafka vs RabbitMQ — коли що (event streaming vs task queue) | 🔴 | |
| Consumer lag — що це, як моніторити, як реагувати | 🔴 | |
| Schema evolution: Avro + Schema Registry (awareness) | 🔴 | |
| Compacted topics — для event sourcing | 🔴 | |
| Transactional producer — exactly-once в Kafka | 🔴 | |

---

## ✅ Закриті теми

---

## ⚠️ Gap'и та слабкі місця

---

## 💬 Типові питання на співбесіді

**Warm-up:**
- Що таке індекс і як він прискорює запити?
- ACID — поясни кожну літеру
- LEFT JOIN vs INNER JOIN — різниця

**Middle:**
- Які є isolation levels? Що таке phantom read?
- Чим відрізняється sharding від replication?
- Навіщо потрібен Redis, якщо є БД?
- Напиши window function для ranking

**Senior:**
- Composite index на (A, B, C) — для яких запитів використається? WHERE B=? AND A=? спрацює?
- Як MVCC дозволяє читати без блокування? Поясни xmin/xmax
- Проектуй кешування для high-traffic API: який паттерн, який TTL, як invalidate
- Як досягти exactly-once в Kafka? Які компроміси?
- Zero-downtime migration: як додати NOT NULL колонку без downtime?
- Cache stampede — що це і як вирішити?
- EXPLAIN ANALYZE показує Seq Scan на таблиці з індексом — чому? (statistics, small table, function on column)
- Як підібрати розмір connection pool (HikariCP)?

---

## 🔄 Щоденні Flashcard питання

1. B-tree: чому log(N) пошук? Що зберігається в leaf nodes?
2. Composite index (A,B,C): які запити покриває?
3. MVCC: як PostgreSQL знає які рядки бачить транзакція?
4. READ COMMITTED vs REPEATABLE READ — конкретна різниця?
5. Cache-Aside pattern: хто пише в кеш? хто інвалідує?
6. Kafka: що відбувається коли consumer падає? (rebalancing, offset)
7. HikariCP: від чого залежить оптимальний розмір пулу?
8. Redis eviction: що станеться коли пам'ять закінчиться?
9. Різниця між Redis Pub/Sub і Kafka?
10. Коли NOT використовувати індекс? (low cardinality, small table, write-heavy)

---

## 📊 Статистика сесій
| Дата | Теми | Прогрес | Нотатки |
|------|------|---------|---------|
| | | | |

---

## 📋 Покроковий план вивчення

### Крок 1 — SQL + PostgreSQL (2 дні)
1. Window functions: ROW_NUMBER для топ-5 POI по місту, LAG для порівняння рейтингів
2. CTE: перепиши складний nested query через WITH
3. JSONB: напиши query для фільтрації по openingHours (чи відкрито в понеділок)
4. EXPLAIN ANALYZE: запусти на 5 найчастіших запитах проекту, інтерпретуй
5. **Перевірка:** Claude дає повільний запит → ти аналізуєш план + додаєш індекс

### Крок 2 — Індекси deep (1 день)
1. Додай composite index (city, category) → перевір EXPLAIN
2. Partial index: poi WHERE rating > 4.0 (тільки популярні)
3. JSONB GIN index на openingHours
4. **Перевірка:** "коли індекс НЕ допоможе?" — назви 5 випадків

### Крок 3 — Транзакції + MVCC (1 день)
1. Відкрий 2 psql sessions → продемонструй phantom read → зміни isolation level
2. MVCC: подивись xmin/xmax через system columns
3. Deadlock: створи навмисно → побач pg_stat_activity → виправ ordering
4. **Перевірка:** поясни MVCC без підказок за 3 хвилини

### Крок 4 — Redis прикладне (2 дні)
1. Cache-Aside: закешуй POI by city, перевір cache hit/miss
2. Cache stampede prevention: distributed lock на cache rebuild
3. Eviction policy: обери і обґрунтуй для проекту
4. **Перевірка:** "як спроектувати кешування для 10K QPS на POI endpoint?"

### Крок 5 — Kafka прикладне (1 день)
1. Producer: route.created з idempotence enabled
2. Consumer: manual offset commit, обробка помилок
3. Моніторинг: consumer lag через kafka-consumer-groups.sh
4. **Перевірка:** "що станеться якщо consumer впаде на 5 хвилин?"
