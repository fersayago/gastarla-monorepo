
# Setup TODO – Estado de instalación

Este documento lista **lo que falta completar** y **cómo seguir** desde el punto actual.

Estado actual: **Paso 7 – Variables de entorno (backend)**

---

## ✅ Completado hasta ahora

- pnpm + Turborepo configurado
- Monorepo con:
  - apps/web (Next.js)
  - apps/api (NestJS)
  - packages/shared
  - packages/db
- Workspaces funcionando
- Dependencias locales linkeadas
- Git limpio (sin node_modules)
- Prisma instalado y schema definido

---

## ⏳ Paso 7 – Variables de entorno (pendiente)

### Backend (`apps/api`)

Crear archivo:

```
apps/api/.env
```

Contenido mínimo:

```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/objectives?schema=public"
```

Notas:
- Este archivo **no se versiona**
- Agregar `.env` al `.gitignore` (ya hecho)

---

## ⏳ Paso 8 – Base de datos local (Postgres)

### Opción recomendada: Docker

En la raíz del repo:

```yaml
# docker-compose.yml
services:
  postgres:
    image: postgres:16
    container_name: gastarla_db
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: objectives
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

Levantar DB:

```bash
docker compose up -d
```

---

## ⏳ Paso 9 – Prisma

Desde la raíz:

```bash
pnpm db:migrate
pnpm db:generate
```

Opcional:

```bash
pnpm db:studio
```

---

## ⏳ Paso 10 – NestJS: PrismaService

Crear servicio para exponer Prisma en `apps/api`:

- `PrismaService`
- Inyectarlo en módulos

Objetivo:
- Centralizar acceso a DB
- Facilitar testing

---

## ⏳ Paso 11 – Módulos backend (MVP)

### Objetives
- POST /objectives
- GET /objectives
- PATCH /objectives/:id

### Contributions
- POST /contributions
- GET /balance

### Recommendations
- GET /recommendations
  - ranking
  - objetivo recomendado
  - matrices

---

## ⏳ Paso 12 – Dominio compartido (`packages/shared`)

Implementar:
- computeScore()
- getImpactUrgencyQuadrant()
- getRiskCostQuadrant()
- recommendNextAction()

Debe ser:
- framework agnostic
- testeable
- sin acceso a DB

---

## ⏳ Paso 13 – Frontend

- Configurar `NEXT_PUBLIC_API_URL`
- Dashboard inicial
- Gráficos:
  - Scatter Impacto vs Urgencia
  - Top prioridades
- Vista de recomendación principal

---

## 🔍 Decisiones pendientes

- [ ] Auth (¿sí/no? ¿NextAuth?)
- [ ] Cloud DB (Neon / Supabase)
- [ ] Seed inicial de datos
- [ ] Tests unitarios (shared + api)
- [ ] Deploy (Vercel + backend separado)

---

## 🧭 Regla de oro del proyecto

- Frontend **nunca** accede a DB
- Toda la lógica vive en backend o shared
- Simplicidad > sobre‑arquitectura

---

Estado actual: **listo para continuar desde Paso 7**
