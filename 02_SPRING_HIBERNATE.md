# Spring & Hibernate — Підготовка до співбесіди
**Чат для:** Spring Boot, Spring Core, Hibernate/JPA, REST, Testing  
**Рівень цілі:** Senior (підтягнути глибину при 4+ роках досвіду)  
**Як використовувати:** вставити цей файл на початку сесії, попросити оновити в кінці

---

## Як починати сесію
- *"Поясни мені як Spring AOP створює proxy, потім перевір моє розуміння"*
- *"Задай мені питання по @Transactional рівня Senior — хочу знайти свої gap'и"*
- *"Зроби code review мого Spring сервісу: [вставити код]"*
- *"Що таке N+1 проблема — поясни і покажи як виправити на прикладі"*

---

## Критерії готовності

- 🟢 Можу пояснити mechanism під капотом + show trade-offs + навести приклад з проекту
- 🟡 Знаю що робить, але не можу пояснити HOW it works internally
- 🔴 Потребує вивчення або глибокого повторення

---

## Теми та прогрес

### 🍃 Spring Core / IoC
| Тема | Статус | Нотатки |
|------|--------|---------|
| IoC контейнер: BeanFactory vs ApplicationContext — різниця і коли який | 🔴 | |
| Bean lifecycle: instantiation → populate properties → BeanPostProcessor → init → destroy | 🔴 | |
| BeanPostProcessor vs BeanFactoryPostProcessor — різниця, приклади | 🔴 | |
| Bean scopes: singleton, prototype, request, session — підводні камені prototype в singleton | 🔴 | |
| @Autowired, @Qualifier, @Primary — порядок резолвінгу | 🔴 | |
| Circular dependency — як виникає, три способи вирішення, чому Spring Boot 3 strict | 🔴 | |
| @Component vs @Bean vs @Configuration (CGLIB proxying @Configuration) | 🔴 | |
| @Conditional, @ConditionalOnProperty, @Profile — autoconfiguration | 🔴 | |
| Spring Boot autoconfiguration — spring.factories / AutoConfiguration.imports, @EnableAutoConfiguration | 🔴 | |
| @SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan | 🔴 | |
| ApplicationEvent, @EventListener — internal event system | 🔴 | |

### 🎯 Spring AOP
| Тема | Статус | Нотатки |
|------|--------|---------|
| AOP концепції: aspect, pointcut, advice (before/after/around), joinpoint | 🔴 | |
| JDK Dynamic Proxy (interface) vs CGLIB Proxy (class) — коли який, Spring Boot default | 🔴 | |
| @Aspect, @Before, @After, @Around — написати logging aspect | 🔴 | |
| Self-invocation проблема — ЧОМУ і ТРИ способи вирішення | 🔴 | |
| Spring AOP vs AspectJ — коли недостатньо Spring AOP | 🔴 | |

### 💸 Транзакції
| Тема | Статус | Нотатки |
|------|--------|---------|
| @Transactional — як працює (proxy → TransactionInterceptor → PlatformTransactionManager) | 🔴 | |
| Propagation: REQUIRED, REQUIRES_NEW, NESTED, SUPPORTS, NOT_SUPPORTED, MANDATORY, NEVER | 🔴 | |
| Isolation levels в Spring і як маплять на DB isolation | 🔴 | |
| Rollback rules: rollbackFor, noRollbackFor, default (unchecked only!) | 🔴 | |
| readOnly=true — що реально робить (Hibernate flush mode, DB hints) | 🔴 | |
| Типові помилки: self-invocation, private method, checked exception без rollbackFor, wrong proxy | 🔴 | |

### 🌐 Spring MVC / REST
| Тема | Статус | Нотатки |
|------|--------|---------|
| DispatcherServlet — request lifecycle (HandlerMapping → HandlerAdapter → ViewResolver) | 🔴 | |
| @RestController, @RequestMapping, @PathVariable, @RequestParam | 🔴 | |
| @RequestBody, @ResponseBody, HttpMessageConverter (Jackson) | 🔴 | |
| @ExceptionHandler, @ControllerAdvice, ProblemDetail (RFC 7807, Spring Boot 3) | 🔴 | |
| ResponseEntity — коли і навіщо, status codes best practices | 🔴 | |
| REST best practices: resource naming, versioning (URL vs header), pagination, HATEOAS | 🔴 | |
| Validation: @Valid, @Validated, custom validators, groups | 🔴 | |
| Content negotiation, custom HttpMessageConverter | 🔴 | |

### 🔒 Spring Security
| Тема | Статус | Нотатки |
|------|--------|---------|
| Security filter chain — порядок фільтрів, SecurityFilterChain bean (new style) | 🔴 | |
| Authentication vs Authorization, AuthenticationProvider, UserDetailsService | 🔴 | |
| JWT: структура (header.payload.signature), validation, refresh token rotation | 🔴 | |
| @PreAuthorize, @Secured, SpEL expressions | 🔴 | |
| CSRF — коли потрібен (stateful), коли вимкнути (stateless JWT) | 🔴 | |
| CORS — що, навіщо, як конфігурувати в Spring | 🔴 | |
| OAuth2 / OpenID Connect — основи, flow types (authorization code, client credentials) | 🔴 | |
| Password encoding: BCrypt, Argon2 — чому не MD5/SHA | 🔴 | |

### ⚡ Async Processing
| Тема | Статус | Нотатки |
|------|--------|---------|
| @Async, @EnableAsync — як працює, thread pool configuration | 🔴 | |
| TaskExecutor конфігурація — чому default SimpleAsyncTaskExecutor погано | 🔴 | |
| CompletableFuture в Spring контексті | 🔴 | |
| Spring WebFlux vs Spring MVC — реактивний стек, коли виправданий | 🔴 | |

### 🗃️ Hibernate / JPA
| Тема | Статус | Нотатки |
|------|--------|---------|
| Entity lifecycle: transient → persistent → detached → removed, persistence context | 🔴 | |
| Fetch types: LAZY vs EAGER, LazyInitializationException — причини і рішення | 🔴 | |
| N+1 проблема — причина, detection (Hibernate logging), рішення (JOIN FETCH, @EntityGraph, @BatchSize) | 🔴 | |
| @OneToMany, @ManyToOne, @ManyToMany — mappedBy, orphanRemoval, best practices | 🔴 | |
| CascadeType — що робить кожен, чому CascadeType.ALL небезпечно | 🔴 | |
| Hibernate L1 кеш (Session/EntityManager) vs L2 кеш (SessionFactory, EhCache/Caffeine) | 🔴 | |
| Optimistic locking (@Version) vs Pessimistic locking (LockModeType) | 🔴 | |
| JPQL vs Criteria API vs Native query vs Spring Data query derivation | 🔴 | |
| Spring Data JPA: Specifications (dynamic queries), Projections (interface/class), @Query | 🔴 | |
| Liquibase / Flyway — навіщо, migration strategies, zero-downtime changes | 🔴 | |
| Dirty checking, flush modes (AUTO, COMMIT), batch inserts/updates | 🔴 | |

### 🧪 Testing (КРИТИЧНО для Senior)
| Тема | Статус | Нотатки |
|------|--------|---------|
| Testing pyramid: unit → integration → E2E — баланс для Spring | 🔴 | |
| JUnit 5: @Test, @BeforeEach, @ParameterizedTest, @Nested, assertions | 🔴 | |
| Mockito: @Mock, @InjectMocks, @Spy, when/thenReturn, verify, ArgumentCaptor | 🔴 | |
| @SpringBootTest — коли використовувати, чому повільно | 🔴 | |
| Slice tests: @WebMvcTest, @DataJpaTest, @JsonTest — що підіймають | 🔴 | |
| @MockBean vs @Mock — різниця, коли який | 🔴 | |
| Testcontainers — integration тести з реальною PostgreSQL/Redis/Kafka | 🔴 | |
| MockMvc — тестування контролерів без підняття сервера | 🔴 | |
| Test fixtures, Test Data Builder pattern | 🔴 | |

---

## ✅ Закриті теми

---

## ⚠️ Gap'и та слабкі місця

---

## 💬 Типові питання на співбесіді

**Warm-up (мусиш відповідати миттєво):**
- Що таке IoC і DI? Чим відрізняються?
- Яка різниця між @Component і @Bean?
- Що таке LAZY vs EAGER fetching?

**Middle (основна маса):**
- Як Spring управляє транзакціями? Як @Transactional працює під капотом?
- Що таке N+1 проблема і як її вирішити? Як виявити?
- Поясни Bean lifecycle в Spring
- Як працює Spring Security filter chain?
- Як тестуєш Spring додаток? Які типи тестів пишеш?

**Senior (тут визначається рівень):**
- Чому @Transactional не працює при self-invocation? Як вирішити?
- Поясни різницю між JDK Proxy і CGLIB. Коли Spring використовує кожен?
- Що відбудеться якщо @Transactional(REQUIRES_NEW) викликати з іншого @Transactional методу?
- Як вирішуєш circular dependency? Чому Spring Boot 3 зробив strict mode?
- Розкажи про Hibernate persistence context. Що таке dirty checking? Коли flush?
- Як проектуєш тестування для мікросервісу? Де Testcontainers, де моки?
- readOnly=true в @Transactional — що реально відбувається на рівні Hibernate і БД?
- Як обрати між @WebMvcTest і @SpringBootTest?

---

## 🔄 Щоденні Flashcard питання

1. Як @Transactional працює під капотом? (proxy → interceptor → manager)
2. Чому self-invocation обходить @Transactional?
3. REQUIRED vs REQUIRES_NEW propagation — що відбувається при exception в nested?
4. Як Spring резолвить bean при кількох кандидатах? (порядок: @Primary → @Qualifier → by name)
5. Що підіймає @WebMvcTest? Що НЕ підіймає?
6. Як Hibernate визначає які поля змінились? (dirty checking через snapshot)
7. N+1: чому JOIN FETCH краще за EAGER у @OneToMany?
8. Різниця між L1 і L2 cache в Hibernate?
9. Коли вимикати CSRF в Spring Security?
10. Чому @Configuration проксується через CGLIB?

---

## 📊 Статистика сесій
| Дата | Теми | Прогрес | Нотатки |
|------|------|---------|---------|
| | | | |

---

## 📋 Покроковий план вивчення

### Крок 1 — Spring Core deep dive (2 дні)
1. Bean lifecycle: напиши BeanPostProcessor що логує створення кожного біна
2. @Configuration CGLIB proxying: поясни що буде якщо виклик @Bean метод всередині @Configuration
3. Circular dependency: навмисно створи → побач помилку → виправ 3 способами
4. **Перевірка:** поясни autoconfiguration flow без підказок

### Крок 2 — AOP + Транзакції (2 дні)
1. Logging aspect для RouteOptimizer: @Around з часом виконання
2. Self-invocation: навмисно зроби помилку → виправ через self-injection
3. REQUIRED vs REQUIRES_NEW: зроби тест де nested rollback НЕ ролбечить parent і навпаки
4. **Перевірка:** "чому @Transactional на private метод не працює?" — відповідь за 30 сек

### Крок 3 — Hibernate/JPA deep (3 дні)
1. N+1: включи `spring.jpa.show-sql=true` → знайди N+1 → виправ JOIN FETCH + @EntityGraph
2. @Version: додай optimistic locking в Route, напиши тест на concurrent update
3. Spring Data Specifications: dynamic filtering POI по city + category + rating range
4. Liquibase: створи міграції для всіх таблиць, зроби refactoring міграцію
5. **Перевірка:** поясни повний lifecycle запиту від HTTP до SQL і назад

### Крок 4 — Testing (2 дні — MUST HAVE для Senior)
1. Unit тести для RouteOptimizer (Mockito)
2. @WebMvcTest для PoiController (MockMvc + @MockBean)
3. @DataJpaTest для PoiRepository
4. Integration test з Testcontainers (PostgreSQL + Redis)
5. **Перевірка:** "як би ти покрив тестами новий endpoint від unit до integration?"

### Крок 5 — Security + REST best practices (1 день)
1. JWT flow: register → login → get token → protected endpoint → 401 without token
2. @PreAuthorize: ADMIN може видаляти POI, USER ні
3. ProblemDetail (RFC 7807): GlobalExceptionHandler з стандартним error format
4. **Перевірка:** поясни security filter chain для JWT request
