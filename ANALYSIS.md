# Аналіз та покращення — Підготовка до Senior Java

## Загальна оцінка: 7.5/10

Фундамент дуже міцний: проект як стрижень, зв'язка теорія→практика→співбесіда, щоденний roadmap. Але є системні проблеми, які знижують ефективність при твоєму профілі (4+ років, фултайм, EU/UA ринок).

---

## Проблема #1: Дублювання CLAUDE.md ↔ 06_PROJECT.md

**Що не так:** ~60% контенту повторюється. Domain Model, API Endpoints, бізнес-логіка описані в обох файлах. Це створює проблему синхронізації — при зміні одного файлу треба оновити інший.

**Рішення:** Чітко розділити відповідальність:
- `CLAUDE.md` — технічний контекст для Claude Code (структура, стек, команди). Те, що Claude потребує щоб писати код.
- `06_PROJECT.md` — підготовка до розмови про проект на співбесіді (чому такі рішення, trade-offs, як масштабувати, що б змінив). Те, що тобі потрібно щоб ГОВОРИТИ про код.

---

## Проблема #2: Roadmap не враховує 4+ роки досвіду

**Що не так:** Тиждень 1 починається з "HashMap: bucket, hash, collision" — для 4+ років це має бути ПОВТОРЕННЯ за 1 день, а не вивчення з нуля за тиждень. Темп розрахований на Junior→Middle, а не на Senior з gap'ами.

**Рішення:** 
- Місяць 1: швидкий прогін теорії (повторення, не вивчення) + паралельно проект до кроку 5
- Місяць 2: глибокі теми (Concurrency advanced, JVM tuning, Hibernate deep) + проект до кроку 9
- Місяць 3: System Design + Deploy + English/Behavioral
- Тижні 13-14: тільки mock interviews і полірування

---

## Проблема #3: Пропущені критичні теми

### 01_JAVA_CORE.md — відсутні:
- Exception handling (checked vs unchecked, try-with-resources, custom exceptions) — питають ЗАВЖДИ
- Serialization (Serializable, Externalizable, serialVersionUID) — питають часто
- Reflection + Annotations — основа Spring, без розуміння неможливо пояснити як Spring працює
- Java Memory Model формально (happens-before rules повний список)
- Records, Sealed Classes, Pattern Matching — є в списку, але потрібна окрема глибша секція для Java 17-21

### 02_SPRING_HIBERNATE.md — відсутні:
- Testing (Spring Boot Test, @DataJpaTest, @WebMvcTest, @MockBean, TestContainers) — критично для Senior
- Spring Boot 3 міграція (Jakarta namespace, native compilation awareness)
- Spring Data JPA: Query derivation, Specifications, Projections
- Actuator + Micrometer метрики
- Async processing (@Async, @EnableAsync, TaskExecutor)

### 03_DATABASES.md — відсутні:
- Нормалізація (1NF → 3NF → BCNF) — базове, але питають
- PostgreSQL специфіка: JSONB, Arrays, Full-text search
- Database migration strategies (zero-downtime migrations)

### 04_SYSTEM_DESIGN.md — відсутні:
- **Back-of-envelope estimation** — це перше, що перевіряють. Скільки QPS, скільки storage, bandwidth
- **Числа які треба знати напам'ять** (latency числа, розміри даних)
- Concrete examples: як рахувати capacity для URL shortener, для chat
- **12-factor app** — часто питають для cloud-native
- **Database per service pattern** — ключовий для мікросервісів

### 05_LEETCODE.md — відсутні:
- **Trie** — String задачі, autocomplete (прямий зв'язок з проектом!)
- **Union-Find** — Graph connectivity задачі
- **Intervals** (Merge Intervals, Insert Interval) — класичний патерн
- Bit Manipulation основи
- Загальна кількість задач замала: 35 → мінімум 45-50

### 07_ENGLISH_BEHAVIORAL.md — відсутні:
- **Salary negotiation фрази** — для EU/стартапів це важливо
- **Questions to ask the interviewer** — показує senior mindset
- Культурні різниці EU vs UA співбесід

---

## Проблема #4: Немає системи spaced repetition

**Що не так:** "Через тиждень повтори задачу" — це є тільки в LeetCode файлі. Для теорії немає механізму повторення.

**Рішення:** Додати в кожен файл секцію "Flashcard питання" — 5-10 одноречених питань для щоденного self-check. Не вчити заново, а швидко перевірити що не забув.

---

## Проблема #5: Немає метрик готовності

**Що не так:** Статуси 🔴/🟡/🟢 суб'єктивні. Коли тема "закрита"? Коли можна йти далі?

**Рішення:** Для кожної теми додати конкретний критерій:
- 🟢 = можу пояснити без підказок за 2 хвилини + відповісти на follow-up
- 🟡 = знаю концепцію, але плутаюсь в деталях
- 🔴 = не можу пояснити впевнено

---

## Проблема #6: Таймінг Roadmap нереалістичний для фултайм

**Що не так:** 4 місяці при 6-8 годин/день — це ~700 годин. Для людини з 4+ роками досвіду це забагато. Реалістичніше:
- 10-11 тижнів активної підготовки
- 2-3 тижні чистих mock interviews
- Починати подаватись на вакансії з тижня 6-7, а не чекати "поки буду готовий"

**Рішення:** Стиснути roadmap до 3 місяців. Додати milestone: "з тижня 7 починай подаватись".
