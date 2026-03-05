# Java Upgrade Decision and Process Log

## Decision Summary
- **Language**: Java
- **Current Version**: 17
- **Target Version**: 21
- **Decision**: Upgrade
- **Decision Date**: 2026-03-05

## Rationale

### Support Timeline Analysis
- **Java 17 (LTS)**: Released September 2021, premier support until September 2026, extended support until September 2029.
- **Java 21 (LTS)**: Released September 2023, premier support until September 2028, extended support until September 2031.
- Java 21 is the latest battle-tested LTS release, widely adopted in production environments.

### Version Selection Logic
- Java 21 was chosen as it is the latest LTS version with broad ecosystem support.
- Spring Boot 4.0.0 (used by this project) fully supports Java 21.
- Java 21 introduces significant features: virtual threads, pattern matching for switch, record patterns, sequenced collections, and more.
- As a sample/reference application, upgrading to the latest stable LTS ensures the project demonstrates current best practices.

### Risk Assessment
- **Low risk**: Java 21 is fully backward-compatible with Java 17 code.
- Spring Boot 4.0.0 officially supports Java 21.
- All major dependencies (H2, MySQL Connector, PostgreSQL driver, Caffeine, etc.) are compatible with Java 21.
- No breaking changes expected for this codebase.

## Actions Taken

### 1. Version Reference Updates

| File | Change |
|------|--------|
| `pom.xml` | `<java.version>17</java.version>` -> `<java.version>21</java.version>` |
| `build.gradle` | `JavaLanguageVersion.of(17)` -> `JavaLanguageVersion.of(21)` |
| `.github/workflows/maven-build.yml` | `java: [ '17' ]` -> `java: [ '21' ]` |
| `.github/workflows/gradle-build.yml` | `java: [ '17' ]` -> `java: [ '21' ]` |
| `.devcontainer/Dockerfile` | `VARIANT=17-bullseye` -> `VARIANT=21-bullseye`, `JAVA_VERSION=17.0.7-ms` -> `JAVA_VERSION=21.0.3-ms` |
| `README.md` | Updated Java version references from 17 to 21 |

### 2. Build and Test Results
- **Build**: `mvn clean verify` completed successfully (BUILD SUCCESS)
- **Tests**: 58 tests run, 0 failures, 0 errors, 0 skipped
- **JaCoCo**: Code coverage report generated successfully (22 classes analyzed)
- **JAR**: `spring-petclinic-4.0.0-SNAPSHOT.jar` built and repackaged successfully
- **Java Version Used**: OpenJDK 21.0.10 (build 21.0.10+7-Ubuntu-122.04)

### 3. Issues Encountered
- No issues encountered. The upgrade was seamless with no code changes required.

## Final Recommendation
Upgrade to Java 21 LTS is recommended and straightforward for this Spring Boot 4.0.0 project. The upgrade provides access to modern Java features, improved performance, and extended support timeline.
