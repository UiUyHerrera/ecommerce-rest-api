# E-commerce REST API

API REST para una plataforma de comercio electrónico, construida con Node.js, TypeScript, Express y PostgreSQL. Incluye autenticación, gestión de productos, carrito y pedidos, documentación y pruebas.

[English version](#english)

## Funcionalidades

- Registro e inicio de sesión con JWT y roles.
- CRUD de productos, carrito de compras y pedidos.
- Control de inventario y rutas de administración.
- Validación de datos con Zod.
- Documentación Swagger/OpenAPI y pruebas de integración con Vitest.
- PostgreSQL gestionado con Prisma y entorno local con Docker Compose.

## Tecnologías

Node.js · TypeScript · Express · PostgreSQL · Prisma · JWT · Zod · Vitest · Docker

## Requisitos

- Node.js y npm.
- Docker y Docker Compose.

## Instalación y ejecución

~~~bash
npm install
cp .env.example .env
docker compose up -d db
npm run db:migrate
npm run db:seed
npm run dev
~~~

Completa las variables de entorno en .env antes de iniciar la API. Las cuentas que crea el seed son únicamente para desarrollo local; no las uses en producción y cambia cualquier credencial de ejemplo antes de desplegar.

## English

A REST API for an e-commerce platform built with Node.js, TypeScript, Express, and PostgreSQL. It includes authentication, product management, carts and orders, API documentation, and tests.

### Features

- Registration and sign-in with JWT and role-based access.
- Product CRUD, shopping carts, and orders.
- Inventory management and administrative endpoints.
- Request validation with Zod.
- Swagger/OpenAPI documentation and integration tests with Vitest.
- PostgreSQL managed with Prisma and a local Docker Compose environment.

### Stack

Node.js · TypeScript · Express · PostgreSQL · Prisma · JWT · Zod · Vitest · Docker

### Requirements

- Node.js and npm.
- Docker and Docker Compose.

### Install and run

~~~bash
npm install
cp .env.example .env
docker compose up -d db
npm run db:migrate
npm run db:seed
npm run dev
~~~

Set the required environment variables in .env before starting the API. Seeded accounts are for local development only; never use them in production, and replace any sample credentials before deployment.
﻿# Backend REST API

API REST para una tienda online hecha con Node.js, TypeScript, Express y PostgreSQL.

## Funciones

- Registro e inicio de sesión
- JWT y roles de usuario
- CRUD de productos
- Carrito y pedidos
- Control de stock
- Panel de administración mediante API
- Validación con Zod
- Tests de integración
- Docker
- Swagger

## Tecnologías

- Node.js
- TypeScript
- Express
- PostgreSQL
- Prisma
- JWT
- Zod
- Vitest
- Docker

## Instalación

```bash
npm install
cp .env.example .env
docker compose up -d db
npm run db:migrate
npm run db:seed
npm run dev
```

## Cuentas de prueba

El seed crea dos cuentas, solo para uso en desarrollo local:

- `manolo@example.com` / `admin123` (admin)
- `pepeito@example.com` / `cliente123` (cliente)
