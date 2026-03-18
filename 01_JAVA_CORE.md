# Core Java — Підготовка до співбесіди
**Чат для:** теорія Core Java, Collections, JVM, Concurrency  
**Рівень цілі:** Senior (підтягнути глибину при 4+ роках досвіду)  
**Як використовувати:** вставити цей файл на початку сесії, попросити оновити в кінці

---

## Як починати сесію

Приклади запитів:
- *"Поясни мені як працює HashMap зсередини, потім задай питання як на співбесіді"*
- *"Я розкажу тобі як працює GC, а ти скажи де я помиляюсь або що пропустив"*
- *"Задай мені 5 питань по Concurrency рівня Senior, оціни мої відповіді"*
- *"Зроби mock-сесію по темі Collections: 20 хвилин, питання від простого до складного"*

---

## Критерії готовності теми

- 🟢 Можу пояснити без підказок за 2 хв + відповісти на follow-up + навести приклад з проекту
- 🟡 Знаю концепцію, але плутаюсь в деталях або не можу навести реальний приклад
- 🔴 Не можу пояснити впевнено або ніколи не вивчав глибоко

---

## Теми та прогрес

### 📦 Collections & Generics
| Тема | Статус | Нотатки |
|------|--------|---------|
| ArrayList vs LinkedList — внутрішня реалізація, Big-O | 🔴 | |
| HashMap: bucket, hash, collision, treeify (Java 8+), resize | 🔴 | |
| LinkedHashMap (access-order для LRU), TreeMap (Red-Black tree), EnumMap | 🔴 | |
| HashSet, LinkedHashSet, TreeSet — зв'язок з Map | 🔴 | |
| equals() / hashCode() контракт — що ламається при порушенні | 🔴 | |
| Generics: type erasure, wildcards (? extends/super), bounded types, PECS | 🔴 | |
| Comparable vs Comparator, Comparator.comparing() chaining | 🔴 | |
| Collections.unmodifiableList vs List.of vs List.copyOf | 🔴 | |
| Iterator, fail-fast vs fail-safe (ConcurrentModificationException) | 🔴 | |
| Queue, Deque, ArrayDeque vs LinkedList як Queue | 🔴 | |

### 🔤 String, Stream API & Modern Java
| Тема | Статус | Нотатки |
|------|--------|---------|
| String immutability, String pool, intern(), compact strings (Java 9+) | 🔴 | |
| String vs StringBuilder vs StringBuffer — коли що | 🔴 | |
| Stream API: map, filter, reduce, collect, flatMap, peek | 🔴 | |
| Collectors: toMap, groupingBy, partitioningBy, joining | 🔴 | |
| Optional — правильне використання, antipatterns | 🔴 | |
| Lambdas, functional interfaces (Function, Predicate, Consumer, Supplier) | 🔴 | |
| Method references: static, instance, constructor | 🔴 | |
| Java 17: Records, Sealed classes, Pattern matching for instanceof | 🔴 | |
| Java 21: Pattern matching in switch, Sequenced Collections | 🔴 | |

### ⚠️ Exception Handling
| Тема | Статус | Нотатки |
|------|--------|---------|
| Checked vs Unchecked — філософія, коли який | 🔴 | |
| try-with-resources, AutoCloseable, suppressed exceptions | 🔴 | |
| Custom exceptions — best practices, exception hierarchy в проекті | 🔴 | |
| Exception handling в Stream API (як обробляти checked exceptions в lambda) | 🔴 | |
| Error vs Exception, StackOverflow, OutOfMemory — коли ловити | 🔴 | |

### 🔄 Concurrency & Multithreading
| Тема | Статус | Нотатки |
|------|--------|---------|
| Thread lifecycle, daemon threads, Thread vs Runnable vs Callable | 🔴 | |
| volatile — memory visibility guarantee, happens-before | 🔴 | |
| synchronized — monitor, intrinsic lock, reentrance | 🔴 | |
| Java Memory Model: happens-before rules (повний список) | 🔴 | |
| Race condition, deadlock, livelock, starvation — приклади і рішення | 🔴 | |
| ReentrantLock, ReadWriteLock, StampedLock — порівняння | 🔴 | |
| AtomicInteger, AtomicReference, CAS операції, ABA проблема | 🔴 | |
| ExecutorService, ThreadPoolExecutor (corePoolSize, maxPoolSize, queue) | 🔴 | |
| CompletableFuture — chaining, thenApply vs thenCompose, exception handling | 🔴 | |
| ConcurrentHashMap (segments → Node locking Java 8+), CopyOnWriteArrayList | 🔴 | |
| BlockingQueue (ArrayBQ vs LinkedBQ), CountDownLatch, CyclicBarrier, Semaphore | 🔴 | |
| Virtual Threads (Java 21) — carrier threads, pinning, коли використовувати | 🔴 | |
| Structured Concurrency (Java 21 preview) — basic awareness | 🔴 | |
| ForkJoinPool, parallel streams — підводні камені | 🔴 | |

### ⚙️ JVM Internals & GC
| Тема | Статус | Нотатки |
|------|--------|---------|
| JVM memory: heap, stack, metaspace (замість PermGen), code cache | 🔴 | |
| Young Gen (Eden, S0, S1), Old Gen, allocation & promotion | 🔴 | |
| GC алгоритми: Serial, Parallel, G1, ZGC, Shenandoah — коли який | 🔴 | |
| G1 глибоко: regions, mixed GC, humongous objects | 🔴 | |
| GC roots, reachability analysis | 🔴 | |
| Class loading: bootstrap → platform → app, delegation model, context classloader | 🔴 | |
| Strong / Soft / Weak / Phantom references — use cases кожного | 🔴 | |
| Memory leaks — типові причини (listeners, static collections, classloader leaks) | 🔴 | |
| JIT compilation, tiered compilation (C1→C2), inlining, escape analysis | 🔴 | |
| JVM tuning: -Xmx, -Xms, -XX:+UseG1GC, GC logs, safepoints | 🔴 | |
| Profiling: JFR, async-profiler, VisualVM — коли що | 🔴 | |

### 🪞 Reflection & Annotations
| Тема | Статус | Нотатки |
|------|--------|---------|
| Reflection API: Class.forName, getDeclaredMethods, setAccessible | 🔴 | |
| Як Spring використовує reflection (bean creation, DI, AOP) | 🔴 | |
| Custom annotations: @Retention, @Target, annotation processing | 🔴 | |
| Proxy: java.lang.reflect.Proxy — як працює, зв'язок зі Spring AOP | 🔴 | |

### 📦 Serialization
| Тема | Статус | Нотатки |
|------|--------|---------|
| Serializable, serialVersionUID — навіщо | 🔴 | |
| Externalizable — різниця | 🔴 | |
| JSON serialization (Jackson) — @JsonIgnore, @JsonProperty, custom serializers | 🔴 | |
| Проблеми серіалізації: security, versioning, circular references | 🔴 | |

### 🏗️ OOP & Design Patterns
| Тема | Статус | Нотатки |
|------|--------|---------|
| SOLID — по одному прикладу з проекту на кожен | 🔴 | |
| Creational: Singleton (thread-safe варіанти), Builder, Factory Method, Abstract Factory | 🔴 | |
| Structural: Decorator, Proxy, Adapter, Facade | 🔴 | |
| Behavioral: Strategy, Observer, Template Method, Chain of Responsibility | 🔴 | |
| Immutability — як створити immutable клас, defensive copies | 🔴 | |
| Composition vs inheritance — чому "favor composition" | 🔴 | |
| Де в Spring використовуються які патерни (Factory, Proxy, Template, Observer) | 🔴 | |

---

## ✅ Закриті теми
_Сюди переносити теми після статусу 🟢_

---

## ⚠️ Gap'и та слабкі місця
_Сюди записувати що важко, де плутаєшся, що завалив на mock_

---

## 💬 Типові питання на співбесіді

**Warm-up (перевірка базових знань — МУСИШ відповідати миттєво):**
- Чим відрізняється ArrayList від LinkedList? Коли який?
- Як працює HashMap? Що таке collision?
- Що таке deadlock і як його уникнути?
- Різниця між String і StringBuilder?
- Checked vs unchecked exceptions — коли який?

**Middle (основна маса питань):**
- Розкажи про Java Memory Model і happens-before
- Як зробити Singleton thread-safe? Які варіанти?
- Чим відрізняється synchronized метод від synchronized блоку?
- Як працює CompletableFuture? Наведи приклад chaining
- Що таке type erasure і які проблеми це створює?
- Як обробити checked exception в lambda/stream?

**Senior (глибина — тут треба бути впевненим):**
- Поясни як G1 GC вибирає які регіони збирати
- Як ConcurrentHashMap досягає concurrent writes без глобального лока?
- Що таке false sharing і як його уникнути?
- Virtual Threads — переваги, обмеження, pinning проблема
- Як працює escape analysis і як це впливає на перформанс?
- Чому ForkJoinPool.commonPool() може бути проблемою з parallel streams?
- Як Spring використовує Reflection і Proxy під капотом?

---

## 🔄 Щоденні Flashcard питання (5 хв self-check)

Після вивчення теми — щоранку пройдись по цих питаннях. Якщо на будь-яке не можеш відповісти за 10 секунд — тема потребує повторення.

1. Яка внутрішня структура HashMap? Що відбувається при collision?
2. Що гарантує volatile? Чого НЕ гарантує?
3. Назви 3 happens-before rules
4. В чому різниця між ReentrantLock і synchronized?
5. Що таке type erasure? Що працює в compile-time, що в runtime?
6. Як G1 GC відрізняється від Parallel GC?
7. Коли об'єкт стає eligible for GC?
8. В чому різниця між Weak і Soft reference?
9. Що робить CAS? Що таке ABA?
10. Як створити правильний immutable клас?

---

## 📊 Статистика сесій
| Дата | Теми | Прогрес | Нотатки |
|------|------|---------|---------|
| | | | |

---

## 📋 Покроковий план вивчення

### Крок 1 — Collections швидкий прогін (2 дні)
Ти вже знаєш ці теми — мета ПОГЛИБИТИ і ЗАКРІПИТИ для пояснення вголос.
1. HashMap deep: намалюй bucket structure, поясни treeify threshold (8), resize
2. equals/hashCode: напиши приклад де порушення контракту ламає HashMap
3. Generics PECS: поясни чому `List<? extends Number>` read-only
4. **Перевірка:** поясни HashMap за 3 хвилини вголос без підказок → якщо OK → 🟢

### Крок 2 — String + Stream API + Modern Java (2 дні)
1. Stream API: напиши 5 стрімів з реального проекту (фільтрація POI, groupBy category)
2. Collectors: toMap з merge function, groupingBy з downstream collector
3. Java 21 features: Records (використай як DTO), Pattern matching в switch
4. **Перевірка:** code review свого проекту — де Stream API покращить читабельність

### Крок 3 — Exception Handling + Serialization + Reflection (1 день)
1. Custom exception hierarchy для проекту (RouteOptimizationException, PoiNotFoundException)
2. Jackson: як серіалізується openingHours JSON, custom deserializer якщо потрібно
3. Reflection: поясни як Spring @Autowired знаходить бін — step by step
4. **Перевірка:** поясни exception hierarchy свого проекту як design decision

### Крок 4 — Concurrency (3 дні — ЦЕ НАЙВАЖЛИВІША ТЕМА)
1. День 1: volatile vs synchronized на прикладі лічильника, Java Memory Model rules
2. День 2: ExecutorService, CompletableFuture — зроби async виклик Google Places API
3. День 3: Virtual Threads — перепиши один сервіс, порівняй з platform threads
4. **Перевірка:** Senior питання по Concurrency — 30 хв mock з Claude

### Крок 5 — JVM (2 дні)
1. Heap/Stack/Metaspace: що де зберігається, коли StackOverflow, коли OOM
2. G1 GC: regions, mixed GC, humongous allocation — поясни простими словами
3. Memory leak: знайди потенційний leak в проекті (listeners? static collections?)
4. **Перевірка:** поясни весь lifecycle об'єкта від `new` до GC

### Крок 6 — Design Patterns через проект (1 день)
1. Знайди кожен патерн у своєму проекті: Strategy (оптимізатори), Builder (Route), Factory (Spring beans)
2. Поясни де Spring використовує Proxy, Template Method, Observer
3. **Перевірка:** "які патерни ти використав у проекті і чому?" — відповідь за 5 хв
