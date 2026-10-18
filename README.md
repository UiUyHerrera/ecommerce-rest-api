# ecommerce-rest-api

Backend de una tienda online: cuentas con JWT, roles de cliente y administrador, catálogo con stock, pedidos y estadísticas para el admin. En `public/` hay una página chica que consume la API, para probarla sin Postman.

![Página de prueba: catálogo, carrito y pedidos del usuario](docs/capturas/tienda.png)

Está hecho con Node.js, TypeScript y Express. Los datos van en PostgreSQL a través de Prisma, las entradas se validan con Zod y los tests usan Vitest con Supertest.

## Levantarlo

Necesitás Node.js 20 o más nuevo y Docker.

```bash
npm install
cp .env.example .env
docker compose up -d db
npm run db:migrate
npm run db:seed
npm run dev
```

La API queda en http://localhost:3000, la página de prueba en la raíz y Swagger UI en `/docs`. El seed crea una cuenta de administrador y una de cliente; los datos están en `prisma/seed.ts`.

`JWT_SECRET` es obligatoria: si falta en `.env`, el servidor no arranca.

## Endpoints

| Ruta | Qué hace | Acceso |
|---|---|---|
| `POST /auth/register`, `POST /auth/login` | Crear cuenta y obtener el token | Público |
| `GET /auth/me` | Datos del usuario logueado | Logueado |
| `GET /products`, `GET /products/:id` | Catálogo, con filtros y paginación | Público |
| `POST`, `PATCH`, `DELETE /products` | Alta, edición y baja de productos | Admin |
| `GET /orders`, `GET /orders/:id` | Pedidos propios (el admin ve todos) | Logueado |
| `POST /orders` | Crear un pedido | Logueado |
| `PATCH /orders/:id/cancel` | Cancelar un pedido y devolver el stock | Dueño o admin |
| `GET /users`, `GET /stats` | Usuarios y estadísticas de la tienda | Admin |

El contrato completo está en `docs/openapi.json`.

![Swagger UI con los endpoints de autenticación y productos](docs/capturas/swagger.png)

## Cómo está armado

Cada recurso pasa por las mismas capas: la ruta valida el request con su esquema Zod, el controlador traduce HTTP y el servicio tiene la lógica y habla con Prisma. Los errores se tiran como `HttpError` y un único middleware los convierte en la respuesta.

```
src/
  routes/        rutas y validación
  controllers/   request y response
  services/      lógica de negocio y Prisma
  schemas/       esquemas Zod
  middlewares/   auth, admin, validación y errores
prisma/          esquema, migraciones y seed
tests/           tests de integración
```

Algunas decisiones:

- Los precios y totales son `Decimal` en la base y en el código, nunca `float`.
- Crear un pedido es una sola transacción: se verifican los productos, se descuenta el stock y se guarda el pedido con el precio de ese momento. El descuento es un update condicional (`stock >= cantidad`), así dos pedidos simultáneos no pueden vender la misma última unidad. Cancelar un pedido también es una transacción, y devuelve el stock.
- Helmet, CORS y un límite de requests por IP vienen activados por defecto.

## Tests

```bash
npm test
```

Son tests de integración contra una base real, la de `TEST_DATABASE_URL`, que se limpia antes de cada corrida. Cubren autenticación, productos, pedidos (incluido el caso de dos compras simultáneas de la última unidad) y estadísticas. GitHub Actions los corre contra un PostgreSQL 16 en cada push a main y en cada pull request.
