# Tauri 2 Multi-Platform Build System (Linux + Windows 32/64)

This repository contains a Docker-based build system designed to compile a Tauri application for the following platforms:

- Linux AMD64 (x86_64)
- Linux ARM64 (aarch64)
- Windows 64-bit (x86_64-pc-windows-gnu)
- Windows 32-bit (i686-pc-windows-gnu)

All builds run inside Docker containers, ensuring a reproducible and consistent environment across all hosts.

Build artifacts are exported to:

```
.artifacts/<platform>/
```

---

# Project Structure

```
project/
│
├─ build/
│   ├─ linux/
│   │   ├─ Dockerfile.amd64
│   │   └─ Dockerfile.arm64
│   └─ windows/
│       ├─ Dockerfile.win64
│       └─ Dockerfile.win32
│
├─ src-tauri/
├─ .artifacts/
│   ├─ linux-amd64/
│   ├─ linux-arm64/
│   ├─ win32/
│   └─ win64/
│
├─ docker-compose.yml
└─ README.mdBuild Commands
```

---

## 1. Build for Linux AMD64

```
docker compose up --build build-linux-amd64
```

Output directory:

```
.artifacts/linux-amd64/bundle/
```

---

## 2. Build for Linux ARM64

```
docker compose up --build build-linux-arm64
```

Output directory:

```
.artifacts/linux-arm64/bundle/

```

---

## 3. Build for Windows 64-bit (x86_64-pc-windows-gnu)

```
docker compose up --build build-win64
```

Output directory:

```
.artifacts/win64/release/
```

---

## 4. Build for Windows 32-bit (i686-pc-windows-gnu)

```
docker compose up --build build-win32
```

Output directory:

```
.artifacts/win32/release/
```

---

# Output Locations

All build outputs are exported to the `.artifacts` directory:

| Platform | Path |
| --- | --- |
| Linux AMD64 | `.artifacts/linux-amd64/bundle/` |
| Linux ARM64 | `.artifacts/linux-arm64/bundle/` |
| Windows 64-bit | `.artifacts/win64/release/` |
| Windows 32-bit | `.artifacts/win32/release/` |