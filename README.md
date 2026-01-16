
# Gastarla Monorepo

Aplicación web para **planificar y priorizar gastos únicos** (one‑shot purchases / proyectos personales),
con foco en **decidir qué comprar ahora y qué ahorrar**, usando matrices de decisión y scoring.

El proyecto está pensado como **monorepo** para aprendizaje y uso personal, manteniendo buenas prácticas
de separación entre frontend y backend.

---

## 🧠 Problema que resuelve

Cuando entra dinero destinado a objetivos personales, es difícil decidir:
- qué comprar primero,
- qué conviene postergar,
- cuánto ahorrar para un objetivo grande,
- y por qué una decisión es mejor que otra.

La app transforma una lista de deseos/proyectos en **decisiones claras y explicables**.

---

## 🎯 Alcance (Scope)

### Incluye
- Gastos **únicos** (no recurrentes):
  - cambiar celular
  - arreglos del hogar
  - mejoras de oficina
  - proyectos grandes (garage, sistema eléctrico, etc.)
- Priorización por:
  - urgencia
  - impacto
  - riesgo de postergar
  - costo
  - categoría
- Recomendaciones:
  - “comprar ahora”
  - “ahorrar para este objetivo”
- Visualización mediante matrices y gráficos.

### No incluye
- Gastos básicos (alquiler, comida, servicios)
- Presupuestos mensuales obligatorios
- Manejo de deudas o intereses (por ahora)

---

## 🧩 Arquitectura

Monorepo con **pnpm + Turborepo**.

```
.
├── apps
│   ├── web        # Next.js (frontend)
│   └── api        # NestJS (backend)
├── packages
│   ├── shared     # Dominio compartido (scoring, reglas, tipos)
│   └── db         # Prisma + schema (solo usado por api)
├── pnpm-workspace.yaml
├── turbo.json
└── README.md
```

### Decisión clave de seguridad
- **La base de datos solo es accesible desde `apps/api`**
- El frontend **nunca** tiene acceso directo a DB ni credenciales

---

## 🛠️ Stack tecnológico

### Frontend
- Next.js (App Router)
- React
- TypeScript
- TailwindCSS
- Gráficos: Recharts / similar

### Backend
- NestJS
- TypeScript
- Prisma ORM

### Base de datos
- PostgreSQL (local con Docker, cloud a definir)

### Tooling
- pnpm workspaces
- Turborepo
- Zod (validaciones)
- ESLint / Prettier

---

## 🧮 Modelo de decisión

### Atributos por objetivo
- Categoría
- Costo estimado
- Urgencia (1–5)
- Impacto (1–5)
- Riesgo de postergar (1–5)
- Deadline (opcional)

### Score base (MVP)
```
score = urgencia * 0.4 + impacto * 0.4 + riesgo * 0.2
```

### Matrices
1. Impacto vs Urgencia
2. Riesgo vs Costo

---

## 📊 Funcionalidades previstas (MVP)

- CRUD de objetivos
- Registro de aportes de dinero
- Cálculo de saldo disponible
- Ranking de prioridades
- Recomendación automática:
  - comprar ahora
  - ahorrar para objetivo prioritario
- Dashboard con gráficos

---

## 🚀 Estado actual

- Monorepo configurado
- Next.js + NestJS funcionando
- Paquetes compartidos creados
- Prisma configurado (pendiente migración)
- Variables de entorno: **pendiente (paso 7)**

