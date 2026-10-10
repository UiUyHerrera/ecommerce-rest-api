# E-commerce REST API

API REST para una tienda online: usuarios, productos, pedidos y estadísticas para administradores. Incluye una demo web simple en `public/` que consume la API.

**Stack:** Node.js, TypeScript, Express, PostgreSQL, Prisma, Zod, JWT, Vitest, Docker.

## Qué tiene

- Registro e inicio de sesión con JWT y contraseñas con bcrypt.
- Roles de usuario y administrador, con middleware que protege las rutas de admin.
- CRUD de productos con control de stock.
- Pedidos que descuentan stock dentro de una transacción.
- Validación de cada request con esquemas Zod.
- Manejo de errores centralizado, Helmet, CORS y límite de requests.
- Documentación OpenAPI en `/docs` con Swagger UI.
- Tests de integración con Vitest y Supertest contra una base de datos de prueba.

## Estructura

```
src/
  routes/        rutas de Express
  controllers/   reciben el request y responden
  services/      lógica de negocio y acceso a datos con Prisma
  schemas/       validaciones Zod
  middlewares/   auth, admin, validación y errores
prisma/          esquema, migraciones y seed
tests/           tests de integración
```

## Correrlo

Requiere Node.js 20+ y Docker.

```bash
npm install
cp .env.example .env
docker compose up -d db
npm run db:migrate
npm run db:seed
npm run dev
```

La API queda en `http://localhost:3000` y la documentación en `http://localhost:3000/docs`.

## Tests

```bash
npm test
```

Usan la base de `TEST_DATABASE_URL`, que se limpia antes de cada corrida.
