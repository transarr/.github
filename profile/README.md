# Transarr

**Self-hosted subtitle translation orchestration service for personal media servers**

<div align="center">

[![Docker](https://img.shields.io/badge/Docker-Available-2496ED?logo=docker)](https://github.com/orgs/transarr/packages)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.7.2-blue?logo=typescript)](https://www.typescriptlang.org/)

**Pipeline:** `INGEST → ANALYZE → DECIDE → TRANSLATE → SYNC → VALIDATE → DELIVER`

</div>

---

## 🎯 What is Transarr?

Transarr is a **self-hosted subtitle orchestration service** designed for personal media servers. It automatically analyzes, translates, synchronizes, validates, and delivers subtitles for your media collection.

### Key Features

- 🌍 **Offline Translation** - Neural translation using Argos Translate (8 language pairs)
- 🔄 **Pipeline Architecture** - Modular stages: Ingest → Analyze → Translate → Sync → Validate → Deliver
- 🐳 **Docker-First** - Pre-built images on GitHub Container Registry
- 🎨 **Web UI** - Simple React interface for job management
- 🚀 **REST API** - Programmatic access for automation
- 📦 **Monorepo** - pnpm workspaces with TypeScript
- 🔒 **Security** - Pinned versions, CVE-free dependencies

---

## 🏗️ Architecture

Transarr is composed of two main services:

| Service | Description | Repository |
|---------|-------------|------------|
| **transarr-app** | NestJS backend + React frontend | [transarr/transarr-app](https://github.com/transarr/transarr-app) |
| **transarr-whisper** | Python translation service | [transarr/transarr-whisper](https://github.com/transarr/transarr-whisper) |

### Component Breakdown

```
transarr/
├── transarr-app/
│   ├── src/              # NestJS API
│   ├── client/           # React UI
│   └── packages/         # Shared packages
│       ├── core/         # Types & interfaces
│       ├── llm/          # Translation logic
│       └── utils/        # Utilities
└── transarr-whisper/     # Argos Translate service
```

---

## 🚀 Quick Start

### Using Pre-built Images (Recommended)

```bash
# Clone the main orchestrator repository
git clone https://github.com/transarr/transarr.git
cd transarr

# Pull and start services
docker compose pull
docker compose up -d

# Access the UI
open http://localhost:3000
```

### Development Setup

```bash
# Clone with submodules
git clone --recursive https://github.com/transarr/transarr.git
cd transarr

# Install dependencies
cd apps/app
pnpm install

# Start services
pnpm run dev:api    # Terminal 1
pnpm run dev:web    # Terminal 2
```

---

## 📦 Repositories

### Main Repository

**[transarr/transarr](https://github.com/transarr/transarr)** - Orchestrator repository with Git submodules

### Component Repositories

**[transarr/transarr-app](https://github.com/transarr/transarr-app)** - Full-stack monorepo
- NestJS backend (port 3000)
- React 19 frontend
- pnpm workspaces
- TypeScript 5.7.2

**[transarr/transarr-whisper](https://github.com/transarr/transarr-whisper)** - Translation service
- Flask server (port 5000)
- Argos Translate 1.9.6
- 8 language pairs pre-installed

---

## 🐳 Docker Images

Pre-built images are automatically published to GitHub Container Registry on every commit to main.

| Image | Description | Size |
|-------|-------------|------|
| `ghcr.io/transarr/transarr-app:latest` | NestJS + React | ~500MB |
| `ghcr.io/transarr/transarr-whisper:latest` | Python translation | ~2GB |

### Pull Images

```bash
docker pull ghcr.io/transarr/transarr-app:latest
docker pull ghcr.io/transarr/transarr-whisper:latest
```

### Available Tags

- `latest` - Latest main branch build
- `v1.0.0` - Semantic version tags
- `main-abc1234` - Specific commit SHA

---

## 📖 Documentation

- **[Main README](https://github.com/transarr/transarr)** - Getting started guide
- **[MVP Specification](https://github.com/transarr/transarr/blob/main/Transarr_MVP_Spec.md)** - Complete project specification
- **[Docker Guide](https://github.com/transarr/transarr/blob/main/DOCKER.md)** - Docker images and deployment
- **[Testing Guide](https://github.com/transarr/transarr/blob/main/TESTING.md)** - Testing instructions
- **[App README](https://github.com/transarr/transarr-app/blob/main/README.md)** - Monorepo structure
- **[Whisper README](https://github.com/transarr/transarr-whisper/blob/main/README.md)** - Translation service

---

## 🛠️ Technology Stack

**Backend:**
- NestJS 10.4.16
- TypeScript 5.7.2
- Node.js 20.12.2

**Frontend:**
- React 19.0.1
- Vite 6.4.1
- TypeScript 5.7.2

**Translation:**
- Python 3.11
- Flask 3.1.0
- Argos Translate 1.9.6

**DevOps:**
- Docker & Docker Compose
- pnpm 9.1.1
- GitHub Actions

---

## 🌐 Supported Languages

### Translation Pairs

- English ↔ Spanish
- English ↔ French
- English ↔ German
- English ↔ Portuguese

---

## 🤝 Contributing

We welcome contributions! Please see our contributing guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Workflow

```bash
# Clone with submodules
git clone --recursive https://github.com/transarr/transarr.git

# Work on app component
cd apps/app
git checkout -b feature/my-feature

# Work on whisper component
cd ../../services/whisper
git checkout -b feature/my-feature
```

---

## 🔒 Security

All packages use strict pinned versions (no `^` or `~`). Versions verified free of known CVEs as of December 2025.

Run security audits:

```bash
cd apps/app
pnpm audit --audit-level=moderate
```

### Known Issues

- `multer@1.4.4-lts.1`: Transitive dependency from `@nestjs/platform-express`
  - Multiple DoS vulnerabilities
  - Mitigation: This project does NOT use file upload features
  - Tracked in: [Issue #XX]

---

## 📝 License

MIT License - see [LICENSE](https://github.com/transarr/transarr/blob/main/LICENSE) for details

Copyright (c) 2025 transarr

---

## 🔗 Links

- **GitHub Organization**: https://github.com/transarr
- **Docker Packages**: https://github.com/orgs/transarr/packages
- **Issues**: https://github.com/transarr/transarr/issues
- **Discussions**: https://github.com/transarr/transarr/discussions

---

<div align="center">

**Built with ❤️ for personal media servers**

[Get Started](https://github.com/transarr/transarr) • [Documentation](https://github.com/transarr/transarr#documentation) • [Docker Hub](https://github.com/orgs/transarr/packages)

</div>
