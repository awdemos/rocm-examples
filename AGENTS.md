# ROCm Examples Agent Guide

A curated collection of HIP and ROCm library examples for beginners and advanced users. Examples are grouped by topic and are mostly self-contained CMake projects.

## Repository Layout

- `HIP-Basic/` — minimal HIP kernels with no external dependencies.
- `HIP-Doc/` — examples referenced in the HIP documentation.
- `Libraries/` — examples for ROCm libraries (rocBLAS, hipBLAS, etc.).
- `Applications/` — larger applications using HIP acceleration.
- `Systems/` — GPU-direct storage and ROCm systems examples.
- `AI/` — AI/ML examples.
- `Tutorials/` — code accompanying the HIP tutorials.
- `Common/` — shared helper code and headers.
- `CMakeLists.txt` / `Makefile` — top-level build orchestration.
- `Dockerfiles/` — container environments for building examples.

## Build Commands

### Top-level CMake

```bash
mkdir build && cd build
cmake .. -DCMAKE_CXX_COMPILER=hipcc -DCMAKE_PREFIX_PATH=/opt/rocm
make -j$(nproc)
```

### Makefile (select examples)

```bash
make -C HIP-Basic  # or any category directory
```

### Docker

```bash
docker build -f Dockerfiles/ubuntu-jammy.Dockerfile -t rocm-examples .
```

## Test Commands

Examples are executable binaries; run them manually after building:

```bash
./build/HIP-Basic/hip_basic_hello_world
```

There is no centralized test runner. Each category directory typically has its own README with per-example instructions.

## Lint / Code Style

- C/C++ examples follow the project `.clang-format` config; use `clang-format -i` on modified files.
- Keep examples self-contained; avoid introducing new dependencies unless necessary.
- Update category READMEs when adding or modifying examples.

## Key Conventions

- Use `hipcc` as the C++ compiler for HIP examples.
- Prefer the `Common/` headers for shared utilities rather than duplicating code.
- Each example directory should contain a README explaining what it demonstrates and how to run it.

## Common Gotchas

- Many library examples require matching ROCm versions and installed library packages.
- Windows examples reference Visual Studio solution files; Linux developers can ignore them or use CMake.
- GPU architecture-specific code may need `-DCMAKE_HIP_ARCHITECTURES=gfx90a` or similar.
