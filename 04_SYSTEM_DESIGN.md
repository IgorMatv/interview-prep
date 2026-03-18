# System Design — Підготовка до співбесіди
**Чат для:** архітектура систем, мікросервіси, паттерни, масштабування  
**Рівень цілі:** Senior  
**Як використовувати:** вставити цей файл на початку сесії, попросити оновити в кінці

---

## Як починати сесію
- *"Задай мені system design задачу, я буду проектувати вголос, ти задаватимеш питання як інтерв'юер"*
- *"Поясни мені Saga pattern — choreography vs orchestration з прикладами"*
- *"Розбери зі мною як спроектувати мій туристичний додаток для 100K користувачів"*
- *"Зроби back-of-envelope estimation для URL shortener"*

---

## Фреймворк для System Design інтерв'ю

### Структура відповіді (45 хвилин)
1. **Clarify requirements** (5 хв) — functional + non-functional, scale numbers
2. **Back-of-envelope estimation** (5 хв) — QPS, storage, bandwidth
3. **High-level design** (10 хв) — компоненти, API, data model
4. **Deep dive** (20 хв) — bottlenecks, scaling, trade-offs
5. **Wrap up** (5 хв) — моніторинг, failure scenarios, future improvements

### Питання які ЗАВЖДИ треба задати
- Скільки користувачів? DAU/MAU?
- Read vs write ratio?
- Потрібна consistency чи availability важливіша?
- Які latency вимоги? (P99 < 200ms?)
- Чи потрібен real-time чи near-real-time достатньо?
- Географія: один регіон чи глобально?

---

## 📐 Back-of-Envelope Estimation (MUST KNOW)

### Числа які треба знати напам'ять

**Latency:**
- L1 cache: ~1 ns
- L2 cache: ~4 ns
- RAM access: ~100 ns
- SSD random read: ~100 μs
- HDD random read: ~10 ms
- Network round trip (same datacenter): ~0.5 ms
- Network round trip (cross-continent): ~150 ms

**Throughput:**
- SSD sequential read: ~1 GB/s
- HDD sequential read: ~100 MB/s
- Network: 1 Gbps = ~100 MB/s
- Redis: ~100K ops/sec (single instance)
- PostgreSQL: ~10K queries/sec (simple queries, good hardware)
- Kafka: ~1M messages/sec (per partition ~10K)

**Storage:**
- 1 char = 1 byte (ASCII), 2-4 bytes (UTF-8)
- 1 timestamp = 8 bytes
- 1 UUID = 16 bytes
- 1 KB ≈ 1000 chars text
- 1 MB ≈ 1 min MP3
- 1 GB ≈ 1000 photos (1MB each)
- 1 TB = 1000 GB

**Scale:**
- 1 day = 86,400 sec ≈ 100K sec (for estimation)
- 1 month ≈ 2.5M sec
- 1M DAU × 10 requests/day = 10M requests/day ≈ 100 QPS
- 100 QPS → 1 сервер норм, 10K QPS → потрібен кластер

### Як рахувати (приклад: Tourist Route Optimizer)
```
Users: 100K DAU
Actions per user: 3 route optimizations + 10 POI views = 13 requests
Total: 100K × 13 = 1.3M requests/day
QPS: 1.3M / 86400 ≈ 15 QPS average
Peak (10x): ~150 QPS → один сервер з кешем витримає

Storage (per route):
- Route record: ~500 bytes
- 5 RouteStops: 5 × 200 = 1000 bytes
- Total per route: ~1.5 KB
- 100K users × 3 routes/day × 1.5KB = 450 MB/day
- Per year: ~160 GB → одна PostgreSQL інстанція
```

---

## Теми та прогрес

### 🏗️ Fundamentals
| Тема | Статус | Нотатки |
|------|--------|---------|
| CAP теорема — CP vs AP, PACELC розширення | 🔴 | |
| BASE vs ACID — коли який підхід | 🔴 | |
| Horizontal vs vertical scaling — конкретні числа коли мігрувати | 🔴 | |
| Load balancer: Round Robin, Least Connections, IP Hash, Consistent Hashing | 🔴 | |
| Reverse proxy (nginx) vs load balancer — різниця | 🔴 | |
| CDN — як працює, pull vs push, cache invalidation | 🔴 | |
| API Gateway — функції (auth, rate limiting, routing, aggregation) | 🔴 | |
| Rate limiting: Token Bucket, Sliding Window, Fixed Window — implementation | 🔴 | |
| Consistent hashing — virtual nodes, як додавати/прибирати сервери | 🔴 | |
| **12-Factor App** — кожен фактор з прикладом | 🔴 | |
| DNS, how internet works (від URL до response) | 🔴 | |

### 🔌 Мікросервіси паттерни
| Тема | Статус | Нотатки |
|------|--------|---------|
| Monolith → мікросервіси — коли мігрувати, strangler fig pattern | 🔴 | |
| **Database per service** — як забезпечити data consistency без спільної БД | 🔴 | |
| Saga pattern: choreography (events) vs orchestration (coordinator) | 🔴 | |
| Event Sourcing — переваги (audit trail, replay), складність (projections, eventual consistency) | 🔴 | |
| CQRS — коли виправданий, зв'язок з Event Sourcing | 🔴 | |
| **Outbox pattern** — transactional messaging без distributed transaction | 🔴 | |
| Circuit breaker — states (closed→open→half-open), fallback strategies | 🔴 | |
| Bulkhead pattern — isolate failures | 🔴 | |
| Retry with exponential backoff + jitter | 🔴 | |
| Service discovery: client-side vs server-side (Eureka, Consul, K8s DNS) | 🔴 | |
| API versioning: URL path vs header vs query param | 🔴 | |
| Distributed tracing: correlation ID, OpenTelemetry | 🔴 | |

### 📡 Комунікація
| Тема | Статус | Нотатки |
|------|--------|---------|
| Sync vs async комунікація — trade-offs, коли який | 🔴 | |
| REST vs GraphQL vs gRPC — конкретні use cases кожного | 🔴 | |
| WebSockets vs SSE vs Long polling — коли який | 🔴 | |
| Message queue (RabbitMQ) vs event streaming (Kafka) — різниця | 🔴 | |
| Idempotency — idempotency key pattern, retry safety | 🔴 | |
| Back pressure — як обробляти коли consumer не встигає | 🔴 | |

### 🗄️ Storage & Data
| Тема | Статус | Нотатки |
|------|--------|---------|
| SQL vs NoSQL — конкретні критерії вибору з прикладами | 🔴 | |
| Document DB (MongoDB) — коли вибрати, schema flexibility trade-offs | 🔴 | |
| Wide-column (Cassandra) — write-heavy, time series | 🔴 | |
| Search engine (Elasticsearch) — inverted index, коли потрібен | 🔴 | |
| Object storage (S3) — для медіа, backup, data lake | 🔴 | |
| Data lake vs data warehouse — ETL/ELT | 🔴 | |
| Blob storage strategies, CDN integration | 🔴 | |

### 🔐 Security & Reliability
| Тема | Статус | Нотатки |
|------|--------|---------|
| Authentication: session-based vs token-based (JWT), OAuth2 flows | 🔴 | |
| HTTPS, TLS, certificate management | 🔴 | |
| DDoS protection strategies | 🔴 | |
| SLA, SLO, SLI — як визначати і моніторити | 🔴 | |
| Failover strategies: active-passive, active-active | 🔴 | |
| Disaster recovery: RPO, RTO | 🔴 | |

### 🔍 Observability
| Тема | Статус | Нотатки |
|------|--------|---------|
| Three pillars: Metrics (Prometheus), Logs (ELK), Traces (Jaeger/Zipkin) | 🔴 | |
| Structured logging — JSON logs, correlation ID | 🔴 | |
| Health checks: readiness vs liveness — різниця для K8s | 🔴 | |
| Alerting: alert fatigue, SLO-based alerting | 🔴 | |
| Dashboards: key metrics для кожного компоненту (latency P50/P95/P99, error rate, throughput) | 🔴 | |

---

## Задачі для практики

### Зроблено
| Дата | Задача | Ключові рішення | Що пропустив |
|------|--------|-----------------|-------------|
| | | | |

### Список задач (від простих до складних)
1. [ ] URL Shortener — estimation + design (найлегша, для розминки)
2. [ ] Rate Limiter — алгоритми + distributed implementation
3. [ ] Paste bin — storage decisions, TTL
4. [ ] **Туристичний маршрутизатор** — СВІЙ проект, розбери на 1K → 100K → 1M users
5. [ ] Notification система — multi-channel, priority queue, deduplication
6. [ ] Chat система (WhatsApp) — WebSockets, message ordering, delivery status
7. [ ] News Feed (Twitter) — fan-out on write vs fan-out on read
8. [ ] Ride sharing (Uber) — geo matching, real-time updates
9. [ ] Search autocomplete — Trie, ranking, caching
10. [ ] Video streaming (YouTube) — CDN, transcoding, recommendations

---

## 🗺️ Масштабування свого проекту (KEY для співбесіди)

Це найважливіша секція — вміти розповісти про масштабування СВОГО проекту.

### 1 → 100 users (current state)
- Single PostgreSQL, single app instance
- In-memory caching достатньо
- Monolith нормально

### 100 → 10K users
- Додати Redis для кешування POI і маршрутів
- Connection pool tuning (HikariCP)
- Додати індекси, EXPLAIN ANALYZE
- Async обробка через @Async або Kafka

### 10K → 100K users
- Horizontal scaling: 2-3 app instances behind load balancer
- PostgreSQL read replicas для GET endpoints
- Redis Cluster для availability
- CDN для статики (якщо є UI)
- Rate limiting на API Gateway рівні
- Structured logging + distributed tracing

### 100K → 1M users
- Виділити Route Optimizer в окремий сервіс (CPU-intensive)
- Database sharding по city або region
- Kafka для async processing (ratings, analytics, notifications)
- Pre-compute popular routes для top cities
- Geo-distributed deployment (EU + UA)
- Circuit breaker для Google Places API

---

## ✅ Закриті теми

---

## ⚠️ Gap'и та слабкі місця

---

## 🔄 Щоденні Flashcard питання

1. CAP: чим є PostgreSQL? чим є Cassandra?
2. Back-of-envelope: 1M DAU, 10 requests/user — скільки QPS?
3. Consistent hashing: навіщо virtual nodes?
4. Saga choreography vs orchestration: trade-offs?
5. Outbox pattern: яку проблему вирішує?
6. Circuit breaker: 3 стани і transition rules?
7. 12-factor app: назви 5 факторів
8. Latency: RAM vs SSD vs Network (порядок magnitude)
9. Коли монолiт краще за мікросервіси?
10. REST vs gRPC: коли gRPC виграє?

---

## 📊 Статистика сесій
| Дата | Задача / Тема | Що вдалось | Що провалив |
|------|---------------|------------|-------------|
| | | | |

---

## 📋 Покроковий план вивчення

### Крок 1 — Estimation + Fundamentals (2 дні)
1. Вивчи таблицю latency числа НАПАМ'ЯТЬ
2. Зроби estimation для свого проекту (записано вище)
3. CAP: визнач свій проект, поясни чому
4. 12-factor app: пройдись по кожному, відміть що вже є в проекті
5. **Практика:** URL Shortener — вголос 45 хв, почни з estimation

### Крок 2 — Мікросервіси паттерни (2 дні)
1. Saga: як би виглядав route creation flow в мікросервісах?
2. Outbox pattern: чому event публікація в @Transactional + Kafka producer недостатньо
3. Circuit Breaker: що коли Google Places API лежить? fallback стратегія
4. **Практика:** Chat система — 45 хв, focus на messaging і delivery

### Крок 3 — Масштабування свого проекту (2 дні)
Підготуй розповідь для кожного рівня масштабу (секція вище).
1. Намалюй архітектурну діаграму для 100K users
2. Визнач bottlenecks для кожного рівня
3. **Практика:** Claude грає інтерв'юера — "як масштабуєш до 1M?" — 30 хв mock

### Крок 4 — Advanced tasks (1-2 дні)
1. News Feed: fan-out on write vs read — порівняй trade-offs
2. Notification: multi-channel priority з deduplication
3. **Перевірка:** можеш спроектувати будь-яку з задач за 45 хв вголос
