# Spring Boot Upgrade: 4.0.0 → 4.1.0

## Upgrade Summary
- **Current Version**: 4.0.0
- **Target Version**: 4.1.0
- **Upgrade Date**: 2026-03-05
- **Upgrade Type**: Minor

## Compatibility Analysis
- **Java Version**: 17.0.13 (OpenJDK)
- **Maven Version**: 3.9.9
- **Spring Boot Version Compatibility**: Compatible (Java 17+ required for Spring Boot 4.x)
- **Breaking Changes Expected**: No (minor version upgrade)

## Pre-Upgrade State
### Application Configuration
- Current pom.xml parent version: 4.0.0
- Key dependencies detected:
  - spring-boot-starter-actuator
  - spring-boot-starter-cache
  - spring-boot-starter-data-jpa
  - spring-boot-starter-thymeleaf
  - spring-boot-starter-validation
  - spring-boot-starter-webmvc
  - spring-boot-devtools
  - javax.cache:cache-api
  - jakarta.xml.bind:jakarta.xml.bind-api
  - h2 (runtime)
  - caffeine (runtime)
  - mysql-connector-j (runtime)
  - postgresql (runtime)
  - webjars-locator-lite 1.1.2
  - bootstrap 5.3.8
  - font-awesome 4.7.0
  - spring-boot-starter-data-jpa-test (test)
  - spring-boot-starter-restclient-test (test)
  - spring-boot-starter-webmvc-test (test)
  - spring-boot-testcontainers (test)
  - spring-boot-docker-compose (test)
  - testcontainers-junit-jupiter (test)
  - testcontainers-mysql (test)

### Configuration Files
- `application.properties` (base config, H2 default)
- `application-mysql.properties` (MySQL profile)
- `application-postgres.properties` (PostgreSQL profile)

### Test Status Before Upgrade
- Build Status: PASS
- Total Tests: 58
- Passing Tests: 58
- Failing Tests: 0
- Skipped Tests: 0
- Build Time: 1 min 27 sec
- Application Startup: SUCCESS (verified via integration tests)

## Breaking Changes Analysis
### Changes from Release Notes
- Minor version upgrade (4.0.0 → 4.1.0) — no major breaking changes expected
- No OpenRewrite recipe available specifically for Spring Boot 4.1 (latest available: `UpgradeSpringBoot_4_0`)

### OpenRewrite Recipe Selected
- **Recipe**: `org.openrewrite.java.spring.boot4.UpgradeSpringBoot_4_0`
- **Purpose**: Apply Spring Boot 4.x migration best practices and modernization

### Potential Impact on Application
- Configuration changes needed: NO
- Dependency updates required: Minor (modular starters migration)
- Code changes required: Minor (Java modernization)
- API changes: NO

### Affected Files (Preliminary)
- `pom.xml` (version bump, dependency cleanup)
- `src/test/java/.../I18nPropertiesSyncTest.java` (Java modernization)

## OpenRewrite Migration Results
### Recipe Executed
- **Recipe**: `org.openrewrite.java.spring.boot4.UpgradeSpringBoot_4_0`
- **Execution Time**: ~41 seconds
- **Status**: SUCCESS

### Files Modified by OpenRewrite
- `pom.xml`
- `src/test/java/org/springframework/samples/petclinic/system/I18nPropertiesSyncTest.java`

### Key Changes Applied
1. **POM Updates**:
   - Spring Boot parent version: 4.0.0 → 4.1.0 (OpenRewrite set 4.0.3, manually updated to 4.1.0)
   - Removed explicit `webjars-locator.version` property (now managed by Spring Boot BOM)
   - Removed explicit version from `webjars-locator-lite` dependency
   - Added `spring-boot-starter-restclient` test dependency (modular starters migration)

2. **Code Changes**:
   - `Paths.get()` → `Path.of()` in I18nPropertiesSyncTest.java (2 occurrences) — Java NIO modernization
   - Wildcard import `java.nio.file.*` → explicit imports `java.nio.file.Files` and `java.nio.file.Path`

3. **Configuration Changes**:
   - No application.properties/yml changes required

### Manual Changes Required
- Updated Spring Boot parent version from 4.0.3 (OpenRewrite default) to 4.1.0 (target version)

## Upgrade Process Log

### Step 1: OpenRewrite Recipe Execution
- Ran `UpgradeSpringBoot_4_0` recipe successfully
- OpenRewrite updated parent to 4.0.3 (latest 4.0.x patch), manually bumped to 4.1.0
- Applied modular starters migration and Java modernization

---
*Document maintained by upgrade-springboot skill*
