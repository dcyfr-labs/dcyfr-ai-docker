# AGENTS.md - @dcyfr/ai-docker

**Docker Containerization Template for DCYFR AI Applications**

Version: 0.1.0
Type: Infrastructure template
License: MIT

---

## 🎯 Project Overview

Production-ready Docker containerization templates for:
- Multi-stage Node.js/TypeScript builds
- Docker Compose (development + production)
- Nginx reverse proxy with security hardening
- Kubernetes deployment manifests
- Dockerfile validation and generation tooling

---

## 🏗️ Architecture

### Project Structure

```
dcyfr-ai-docker/
├── Dockerfile                # Multi-stage production build
├── Dockerfile.dev            # Development with hot reload
├── docker-compose.yml        # Development stack
├── docker-compose.prod.yml   # Production stack
├── .dockerignore
├── src/
│   ├── index.ts              # Public API
│   ├── types.ts              # Zod schemas & types
│   ├── validator.ts          # Dockerfile linter
│   ├── generator.ts          # Config generator
│   ├── validate.ts           # CLI validate entry
│   └── generate.ts           # CLI generate entry
├── configs/
│   ├── nginx.conf            # Nginx reverse proxy
│   └── health-check.sh       # Health check script
├── scripts/
│   ├── build.sh              # Image build
│   ├── run.sh                # Stack run
│   └── deploy.sh             # Registry deploy
├── examples/
│   ├── full-stack.yml
│   ├── microservices.yml
│   └── kubernetes/
├── tests/
│   ├── validator.test.ts
│   └── generator.test.ts
└── docs/
    ├── DEVELOPMENT.md
    ├── PRODUCTION.md
    └── TROUBLESHOOTING.md
```

### Key Patterns

**Multi-Stage Builds:**
```
deps → npm ci --omit=dev (production deps)
build → npm ci + tsc (compile)
production → minimal runtime image
```

**Security Hardening:**
- Non-root user (UID 1001)
- Read-only filesystem
- No new privileges
- Resource limits
- Health checks

---

## 🧪 Testing

```bash
npm test              # Run tests
npm run test:watch    # Watch mode
npm run test:coverage # Coverage
```

---

## 📦 Dependencies

### Core
- `zod` — Configuration validation
- `js-yaml` — YAML parsing

### Dev
- `typescript` — Type checking
- `vitest` — Test framework
- `tsx` — TypeScript execution

---

## 🔧 Commands

```bash
npm run validate                    # Validate Dockerfile
npm run generate                    # Generate Docker configs
npm run build                       # Build dev images
npm run build:prod                  # Build production images
npm run up                          # Start dev stack
npm run up:prod                     # Start production stack
npm run down                        # Stop dev stack
npm run logs                        # Follow dev logs
npm run clean                       # Remove containers + volumes
```

---

**Last Updated:** February 5, 2026

## Quality Gates
- TypeScript: 0 errors (`npm run typecheck`)
- Tests: ≥99% pass rate (`npm run test`)
- Lint: 0 errors (`npm run lint`)
