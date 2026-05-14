# Boson Parent POM

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-17%2B-orange.svg)](https://adoptium.net/)
[![Maven](https://img.shields.io/badge/Maven-3.8%2B-red.svg)](https://maven.apache.org/)

The Boson Parent POM is the shared Maven build foundation for all [Boson Network](https://github.com/bosonnetwork) Java projects. It centralizes compiler settings, plugin version pins, and common build behaviors so that every downstream module inherits a consistent, reproducible build configuration.

---

## What This Repository Provides

This repository contains a single `pom.xml` that acts as the parent for all Boson Java subprojects (Core, Services, Clients, etc.). It does **not** contain any source code.

Its purpose is to:

- Enforce **Java 17** as the language level across the entire ecosystem.
- Pin **exact versions** of all shared Maven plugins so builds are reproducible regardless of the local Maven version.
- Define **common build behaviors** — output layout, dependency bundling, source and Javadoc JAR attachment, and GPG artifact signing — so each child module does not have to repeat them.

---

## Using the Parent POM

To use this POM as a parent in a Boson subproject, declare it at the top of the child `pom.xml`:

```xml
<parent>
    <groupId>io.bosonnetwork</groupId>
    <artifactId>boson-parent</artifactId>
    <version>${boson.version}</version>
</parent>
```

The parent POM must be installed into the local Maven repository before child modules can resolve it. See [Build & Install](#build--install) below.

---

## Build & Install

### Prerequisites

| Requirement | Version |
|---|---|
| Java JDK | 17 or later |
| Apache Maven | 3.8 or later |

### Clone

```bash
git clone https://github.com/bosonnetwork/Boson.Parent.git
cd Boson.Parent
```

### Install to local Maven repository

```bash
./mvnw install
```

This installs `boson-parent-<version>.pom` into `~/.m2/repository/io/bosonnetwork/boson-parent/` so that child projects can resolve it locally during development.

---

## Updating Plugin Versions

To upgrade a managed plugin, update the corresponding `<version>` property in `pom.xml` and run:

```bash
./mvnw verify
```

Check the [Maven Plugin Releases](https://maven.apache.org/plugins/) page for the latest stable versions. After updating, bump the parent POM's own version if the change is significant, then reinstall locally and update all child projects to reference the new parent version.

---

## Contributing

We welcome contributions from the open-source community. To get started:

1. Fork this repository and create a feature branch.
2. Make your changes.
3. Ensure `./mvnw verify` passes.
4. Open a pull request with a clear description of the change.

Please read our [Code of Conduct](CODE_OF_CONDUCT.md) before contributing.

---

## License

This project is licensed under the [MIT License](LICENSE).