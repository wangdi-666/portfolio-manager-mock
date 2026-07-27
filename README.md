# Portfolio Manager

A Spring Boot portfolio manager with:
- Form login (`admin` / `admin123`)
- REST API for add/list/remove portfolio items
- Dashboard summary and allocation pie chart
- MySQL persistence via `JdbcTemplate`

## Tech stack
- Java 17
- Spring Boot 3.3
- Spring Security
- Spring JDBC
- MySQL 8
- Static frontend: Bootstrap + Vanilla JS + Chart.js

## Database
You already created `portfolioDb` with `users` and `portfolio_items` tables. Keep values aligned with:
- `src/main/resources/application.properties`

## Run locally
```powershell
./mvnw spring-boot:run
```

Then open:
- `http://localhost:6300/login.html`

## Test
```powershell
./mvnw test
```

Tests run with an in-memory H2 database using:
- `src/test/resources/application-test.properties`
- `src/test/resources/schema.sql`
- `src/test/resources/data.sql`

## Main API
- `GET /api/auth/me`
- `GET /api/portfolio/items`
- `POST /api/portfolio/items`
- `PUT /api/portfolio/items/{id}`
- `DELETE /api/portfolio/items/{id}`
- `GET /api/portfolio/summary`
- `POST /api/price-snapshots/{ticker}/sync`
- `GET /api/price-snapshots/{ticker}`
- `GET /api/price-snapshots/{ticker}/live`

