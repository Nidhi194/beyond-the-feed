# Beyond the Feed

A full-stack digital magazine exploring Instagram's influence on modern life.

## Structure

- `frontend/` React, JSX, Bootstrap, React Router, CSS and API integration
- `backend/` Java 8 Maven WAR, Servlet MVC, JDBC and JSP
- `database/` MySQL schema, foreign keys, constraints and seed content

## Run the frontend

```powershell
cd frontend
npm install
npm run dev
```

The UI calls `GET /api/articles`. It shows seeded preview content until the Java API is available.

## Core API flow

- `GET /api/categories` loads category names and descriptions from MySQL.
- `GET /api/articles` loads published articles, including their category and full body.
- `GET /api/articles/{slug}` loads one article when a detail route needs it.
- `GET /api/comments?articleId={id}` loads approved comments for an article.
- `POST /api/comments` saves a comment with `{ "articleId": 1, "body": "..." }`.

The React app calls these endpoints through the Vite `/api` proxy. Java Servlets handle HTTP, DAOs contain the SQL, and `DatabaseConnection` supplies the JDBC connection.

## Run the API

1. Create `database/schema.sql` in MySQL.
2. Set `DB_URL`, `DB_USER`, and `DB_PASSWORD` in `backend/src/main/java/com/beyondthefeed/util/DatabaseConnection.java` or supply equivalent environment variables.
3. Build `cd backend; mvn package` and deploy `target/beyond-the-feed-api.war` to Tomcat 9+.
4. Point the frontend dev proxy to the Tomcat port in `frontend/vite.config.js`.
