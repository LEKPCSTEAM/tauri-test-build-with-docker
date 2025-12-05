# Tauri Multi-Platform Docker Build System

This repository provides a Docker-based build environment for compiling Tauri applications across multiple platforms. It ensures a consistent build environment and eliminates the need for manual dependency management on the host machine.

## Supported Platforms

*   **Linux AMD64** (x86_64)
*   **Linux ARM64** (aarch64) - Uses cross-compilation
*   **Windows 64-bit** (x86_64-pc-windows-gnu)
*   **Windows 32-bit** (i686-pc-windows-gnu)

## Prerequisites

*   Docker
*   Docker Compose

## Project Structure

*   `build/`: Contains Dockerfiles for each platform.
*   `docker-compose.yml`: Defines the build services and configurations.
*   `src-tauri/`: Your Tauri application source code.
*   `.artifacts/`: Directory where build artifacts are exported.

## Usage

To build the application, run the corresponding Docker Compose service. The source code is mounted into the container, and the build artifacts are copied back to the host.

### 1. Build for Linux AMD64

```bash
docker compose up --build build-linux-amd64
```

**Output:** `.artifacts/linux-amd64/`

### 2. Build for Linux ARM64

This uses a cross-compilation environment (Ubuntu AMD64 base with ARM64 toolchain) to ensure stability and performance.

```bash
docker compose up --build build-linux-arm64
```

**Output:** `.artifacts/linux-arm64/`

### 3. Build for Windows 64-bit

```bash
docker compose up --build build-win64
```

**Output:** `.artifacts/win64/`

### 4. Build for Windows 32-bit

```bash
docker compose up --build build-win32
```

**Output:** `.artifacts/win32/`

## Configuration

### Environment Variables

You can configure environment variables in `docker-compose.yml` or use a `.env` file.

*   `TAURI_PRIVATE_KEY`: Path or content of the private key for signing.
*   `TAURI_KEY_PASSWORD`: Password for the private key.

### Customization

To use this template for your project:

1.  Place your Tauri project in the root directory (ensure `src-tauri` exists).
2.  Update `docker-compose.yml` if you need to change image names or build arguments.
3.  Modify the `Dockerfile`s in `build/` if you require additional system dependencies.

## Troubleshooting

*   **Linux ARM64 Bundling**: AppImage generation is currently disabled for ARM64 builds due to Docker limitations. Only `deb` and `rpm` packages are generated.
*   **Windows Builds**: Ensure `wine` is correctly configured if you encounter runtime issues during the build process (handled automatically by the Dockerfile).