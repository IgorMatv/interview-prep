# Tourist Route Optimizer — Project Context

## Concept
Day planner for tourists and locals.
User says: "Saturday, Kyiv, 10:00–18:00, museums and parks, walking"
→ gets a full day schedule with optimized route, travel times, and opening hours considered.

## Behavior Rules
- Do NOT explain code unless explicitly asked
- Do NOT add comments unless the logic is non-obvious
- After completing a task, show only what was created/changed
- If something can be done in multiple ways, pick the best one and do it — don't ask
- When asked "why", explain briefly

## Tech Stack
- Java 21, Spring Boot 3.x, Maven
- Spring Data JPA + Hibernate
- Spring Security + JWT
- PostgreSQL (coordinates as DECIMAL lat/lng)
- Redis (caching routes, POI lists, public share links)
- Kafka (route.created, route.published events)
- Docker + Docker Compose
- Swagger/OpenAPI
- JUnit 5 + Mockito + Testcontainers

## Domain Model

### User
- id, email, password, role (USER, ADMIN)
- savedPois (favorites)
- routes (history)

### Poi
- id, name, googlePlaceId
- latitude, longitude
- category (MUSEUM, PARK, RESTAURANT, CHURCH, GALLERY, OTHER)
- city
- openingHours (JSON: {"mon": "09:00-18:00", ...})
- avgVisitDuration (minutes, default per category)
- rating (aggregated from user thumbs)

### Route
- id, user, city, date
- startTime, endTime
- travelMode (WALKING, TRANSIT)
- status (DRAFT, SAVED, PUBLISHED)
- shareToken (UUID, nullable — for public link)
- stops (ordered list of RouteStop)
- totalDistance (meters)
- totalDuration (minutes)

### RouteStop
- id, route, poi
- position (order in route)
- plannedArrival, plannedDeparture (LocalTime)
- visitDuration (minutes — user defined or default)
- fixedTime (boolean — if true, arrival time is locked)
- notes

## Project Structure
```
src/main/java/com/example/touristroute/
├── auth/
│   ├── AuthController.java
│   ├── AuthService.java
│   ├── JwtUtil.java
│   ├── JwtAuthFilter.java
│   ├── User.java
│   ├── UserRepository.java
│   ├── RegisterRequest.java
│   └── LoginResponse.java
├── poi/
│   ├── PoiController.java
│   ├── PoiService.java
│   ├── PoiRepository.java
│   ├── Poi.java
│   ├── PoiCategory.java        (enum)
│   ├── PoiRequest.java
│   ├── PoiResponse.java
│   └── PlacesApiClient.java    (Google Places integration)
├── route/
│   ├── RouteController.java
│   ├── RouteService.java
│   ├── RouteRepository.java
│   ├── Route.java
│   ├── RouteStop.java
│   ├── RouteStopRepository.java
│   ├── TravelMode.java         (enum)
│   ├── RouteRequest.java
│   ├── RouteStopRequest.java
│   ├── RouteResponse.java
│   └── optimizer/
│       ├── RouteOptimizer.java         (orchestrator)
│       ├── HaversineCalculator.java    (distance)
│       ├── NearestNeighborStrategy.java
│       ├── TwoOptStrategy.java
│       └── TimelineBuilder.java        (builds schedule with times)
├── rating/
│   ├── RatingController.java
│   ├── RatingService.java
│   └── Rating.java             (userId, poiId, positive boolean)
├── share/
│   ├── ShareController.java
│   └── ShareService.java       (generate/resolve shareToken)
├── kafka/
│   ├── RouteEventProducer.java
│   └── RouteEventConsumer.java
├── common/
│   ├── GlobalExceptionHandler.java
│   ├── SecurityConfig.java
│   └── RedisConfig.java
└── TouristRouteApplication.java
```

## API Endpoints

### Auth
- POST /api/auth/register
- POST /api/auth/login

### POI
- GET  /api/pois?city=Kyiv&category=MUSEUM&page=0
- GET  /api/pois/{id}
- GET  /api/pois/search?query=golden+gate+kyiv     ← Google Places
- GET  /api/pois/suggestions?city=Kyiv&category=MUSEUM
- POST /api/pois/{id}/rate                         ← thumbs up/down
- POST /api/users/me/favorites/{poiId}
- GET  /api/users/me/favorites

### Route
- POST /api/routes/optimize                        ← build optimized route
- POST /api/routes                                 ← save route
- GET  /api/routes/{id}
- GET  /api/users/me/routes                        ← history
- DELETE /api/routes/{id}

### Share
- POST /api/routes/{id}/share                      ← generate public link
- GET  /api/routes/shared/{token}                  ← public access

## Key Business Logic

### Route Optimization Flow
1. Receive RouteRequest (city, startTime, endTime, travelMode, list of stops)
2. For each stop: resolve visitDuration (user defined → category default)
3. Filter: check opening hours for the planned day → warn if closed
4. Optimize order: NearestNeighbor → 2-opt improvement
5. Respect fixedTime stops (keep their position and time, optimize around them)
6. Build timeline: assign plannedArrival/Departure to each stop
7. Check total fits within startTime–endTime → warn if overflow
8. Return RouteResponse with full schedule

### Opening Hours Check
- Poi.openingHours stored as JSON: {"mon":"09:00-18:00","tue":"09:00-18:00",...,"sun":"closed"}
- On optimization: check if plannedArrival falls within open hours for route date's weekday

### Travel Time Estimation
- WALKING: haversine distance / 80 meters per minute (~4.8 km/h)
- TRANSIT: haversine distance / 200 meters per minute (rough estimate)

## Redis Caching Strategy
- POI lists by city+category: TTL 6 hours (@Cacheable)
- Optimized routes: TTL 1 hour (key = hash of poiIds + travelMode + startTime)
- Evict POI cache on rating update (@CacheEvict)
- Public share links: TTL 7 days (manual Redis set)

## Kafka Events
- route.created  → {userId, routeId, city, stopCount}
- route.saved    → {userId, routeId}
- poi.rated      → {userId, poiId, positive}
Consumer: log events + update POI rating aggregate

## Key Commands
```bash
docker-compose up -d
mvn spring-boot:run -Dspring-boot.run.profiles=dev
mvn test
mvn clean package
```

## Current Status
### Completed
- [ ] nothing yet

### In Progress
- [ ] Step 1: Project scaffold

### Next Task
> Create Spring Boot project with Docker Compose (PostgreSQL + Redis + Kafka)

---

## Step Checklist
- [ ] Step 1  — Scaffold: Spring Boot + Docker Compose
- [ ] Step 2  — POI module: Entity, Repository, Service, Controller, DTOs
- [ ] Step 3  — Auth: JWT register/login
- [ ] Step 4  — Route core: entities (Route, RouteStop), basic save/get
- [ ] Step 5  — Route optimizer: Haversine + NearestNeighbor + 2-opt
- [ ] Step 6  — Timeline builder: assign times, check opening hours, overflow warning
- [ ] Step 7  — Redis caching
- [ ] Step 8  — Kafka events
- [ ] Step 9  — Google Places API integration
- [ ] Step 10 — Rating module
- [ ] Step 11 — Share module (public link)
- [ ] Step 12 — Tests: unit + integration (Testcontainers)
- [ ] Step 13 — Deploy: Dockerfile + Railway + GitHub Actions
- [ ] Step 14 — Polish: README + Swagger
