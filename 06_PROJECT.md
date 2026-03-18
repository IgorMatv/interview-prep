# Проект: Tourist Route Optimizer — Interview Preparation
**Фокус:** як ГОВОРИТИ про проект, обґрунтовувати рішення, відповідати на follow-up  
**Технічний контекст проекту:** див. CLAUDE.md  
**Як використовувати:** вставити перед mock interview або code review сесією

---

## Elevator Pitch (30 секунд)

> Tourist Route Optimizer — це REST API для планування дня в місті. Користувач вказує місто, часовий вікно, категорії місць (музеї, парки) і спосіб пересування. Система оптимізує маршрут алгоритмом Nearest Neighbor + 2-opt, враховуючи години роботи місць і час на дорогу. Стек: Java 21, Spring Boot 3, PostgreSQL, Redis для кешування, Kafka для async подій.

**Тренуй цю відповідь вголос поки не буде < 30 секунд без пауз.**

---

## Чому цей проект сильний для Senior позиції

| Аспект | Що показує | Де поглибити |
|--------|-----------|--------------|
| Route Optimizer | Алгоритмічне мислення, не тільки CRUD | Порівняння з TSP, trade-offs |
| fixedTime stops + opening hours | Бізнес-логіка з constraints, edge cases | Як обробляю конфлікти |
| Redis caching | Розуміння cache invalidation, TTL стратегії | Cache stampede, consistency |
| Kafka events | Async архітектура, eventual consistency | Чому не synchronous, error handling |
| Google Places API | Integration з зовнішнім сервісом, resilience | Circuit breaker, fallback, rate limits |
| Testing | Engineering maturity | Testcontainers, test pyramid |

---

## Технічні рішення — ЧОМУ (головне для Senior)

### Чому Nearest Neighbor + 2-opt?
**Питання інтерв'юера:** "Чому не Dijkstra? Чому не точний алгоритм?"

**Відповідь:**
- Задача маршрутизації з N зупинками — це варіація Traveling Salesman Problem (NP-hard)
- Точне рішення для N>15 зупинок — нереалістичний час
- Nearest Neighbor дає O(n²) рішення, яке в середньому ~25% від оптимуму
- 2-opt improvement зменшує це до ~5-10% від оптимуму
- Для 5-15 зупинок (типовий use case) це працює за < 100ms
- **Trade-off:** оптимальність vs швидкість — для планера дня не потрібна ідеальна точність
- **Альтернативи які розглядав:** Genetic Algorithm (складніший, overkill), Google Directions API (платний, dependency), brute force (O(n!) — неможливо при n>12)

### Чому Haversine а не Google Directions?
- Haversine — безкоштовний, instant, zero dependency
- Google Directions — платний ($5 за 1000 requests), мережева latency
- Haversine дає ~80% accuracy для walking в місті (прямі вулиці)
- **Компроміс:** swap Haversine → Google Directions для production з бюджетом
- **Follow-up:** "як виміряв 80% accuracy?" → порівняв 50 маршрутів Київ, середнє відхилення ~20%

### Чому Redis а не in-memory кеш?
- Горизонтальне масштабування: 2+ інстанси app → shared cache
- TTL management: Redis handled, не треба свій eviction logic
- Persistence: restart app → кеш залишається
- Monitoring: redis-cli + Grafana dashboard
- **Trade-off:** мережева latency (~0.5ms) vs in-memory (0ms), але cache hit >> DB query (5-50ms)
- **Якщо б один інстанс:** Caffeine cache було б достатньо + простіше

### Чому Kafka а не просто синхронна обробка?
- **Основна причина:** decoupling — route creation не повинно залежати від analytics/rating processing
- Route optimize → response за 200ms, Kafka event обробляється async
- Якщо consumer падає — events не втрачаються (durability)
- Легко додати нових consumers (notifications, analytics) без зміни producer
- **Чесна відповідь для інтерв'юера:** для цього масштабу можна було б і без Kafka. Я додав щоб: (1) показати розуміння async архітектури, (2) прокачати навик, (3) мати готову інфраструктуру для масштабування
- **Trade-off:** operational complexity (Zookeeper/KRaft, monitoring) vs scalability

### Чому PostgreSQL а не MongoDB?
- Структуровані дані: Route → RouteStop → Poi — relational by nature
- ACID для route saving (всі stops або нічого)
- PostGIS можливість для geo-queries
- JSONB для semi-structured openingHours — best of both worlds
- **Коли б обрав MongoDB:** якщо schema швидко змінюється, або document-oriented дані

### Як обробляю fixedTime stops?
- fixedTime stop = "я маю бути в ресторані о 13:00" → arrival locked
- Optimizer розділяє stops на groups: before/after кожного fixedTime
- Оптимізує кожну group окремо, потім з'єднує
- Edge case: два fixedTime конфліктують (не вистачає часу між ними) → warning в response
- **Follow-up:** "а якщо fixedTime stop закритий в цей час?" → validation перед optimization, error в response

---

## Питання які ТОЧНО задаватимуть

### Про архітектуру
**Q: Як масштабуватимеш на 100K користувачів?**
Підготована відповідь в 04_SYSTEM_DESIGN.md → секція "Масштабування свого проекту"

**Q: Що станеться якщо Google Places API недоступний?**
A: Circuit Breaker (Resilience4j) → fallback на локальну базу POI. Graceful degradation: пошук не працює, але все інше ОК. Health check endpoint показує degraded state.

**Q: Як забезпечуєш data consistency?**
A: @Transactional на RouteService.save() — route + всі stops зберігаються atomically. Optimistic locking (@Version) для concurrent route updates. Kafka events — at-least-once з idempotent consumer.

**Q: Як тестуєш?**
A: Три рівні: unit тести (Mockito) для RouteOptimizer і бізнес-логіки; slice тести (@WebMvcTest, @DataJpaTest) для контролерів і репозиторіїв; integration тести (Testcontainers) для повного flow з реальною PostgreSQL і Redis.

### Про код
**Q: Покажи найскладніший код в проекті**
A: TimelineBuilder — він має враховувати: travel time між stops, visit duration, opening hours check, fixedTime constraints, overflow warning. Це ~100 рядків з чіткою step-by-step логікою.

**Q: Де застосовуєш design patterns?**
A: Strategy (NearestNeighborStrategy, TwoOptStrategy — можна додати нову стратегію без зміни RouteOptimizer), Builder (Route створення), Template Method (optimizer flow), Observer (Kafka events), Proxy (Spring AOP logging).

**Q: Яка найскладніша проблема яку вирішив?**
A: Opening hours validation з timezone awareness + fixedTime constraints. Парсинг JSON → перевірка по day of week → конфлікт з fixedTime → graceful warning замість error.

### Про рішення
**Q: Що б зробив інакше якби починав заново?**
Підготуй ЧЕСНУ відповідь. Приклади:
- Почав би з integration тестів раніше — зекономив би час на debug
- Використав би Flyway замість Liquibase (простіше для цього масштабу)
- Додав би API versioning з початку
- Розглянув би event-driven architecture з самого початку

**Q: Який технічний борг є в проекті?**
A: (ЧЕСНІСТЬ тут = Senior mindset) — Haversine замість реальних відстаней, немає rate limiting на API, немає pagination для route history, error messages можна зробити informatіvнішими.

---

## Прогрес розробки

| Крок | Компонент | Статус | Нотатки |
|------|-----------|--------|---------|
| 1 | Scaffold + Docker Compose | 🔴 | |
| 2 | POI модуль (CRUD + DTOs) | 🔴 | |
| 3 | Auth (JWT) | 🔴 | |
| 4 | Route entities (basic CRUD) | 🔴 | |
| 5 | Route Optimizer (NN + 2-opt) | 🔴 | |
| 6 | Timeline Builder + Opening Hours | 🔴 | |
| 7 | Redis caching | 🔴 | |
| 8 | Kafka events | 🔴 | |
| 9 | Google Places integration | 🔴 | |
| 10 | Rating module | 🔴 | |
| 11 | Share (public links) | 🔴 | |
| 12 | Tests (unit + integration + Testcontainers) | 🔴 | |
| 13 | Deploy (Docker + CI/CD) | 🔴 | |
| 14 | Polish (README + Swagger) | 🔴 | |

---

## Interview Storytelling Checklist

Перед співбесідою перевір що можеш:
- [ ] Пояснити проект за 30 секунд (elevator pitch)
- [ ] Пояснити кожне технічне рішення з trade-offs
- [ ] Намалювати архітектуру на дошці/screen share
- [ ] Показати найцікавіший код (TimelineBuilder або RouteOptimizer)
- [ ] Відповісти на "як масштабуєш?" з конкретними числами
- [ ] Відповісти на "що б змінив?" ЧЕСНО
- [ ] Пояснити testing strategy

---

## 📊 Сесії
| Дата | Що зробив | Питання / Проблеми |
|------|-----------|-------------------|
| | | |
