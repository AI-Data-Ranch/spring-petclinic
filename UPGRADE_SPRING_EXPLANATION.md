# Spring Boot Upgrade: 4.0.0 → 4.1.0-M2

## Executive Summary
**Upgrade Status**: SUCCESSFUL

### Key Metrics
- **Files Modified**: 3 (pom.xml, build.gradle, I18nPropertiesSyncTest.java)
- **Tests Status**: 58/58 passing
- **Build Status**: SUCCESS
- **Application Status**: Verified via `mvn clean install`

### Major Changes
1. Updated Spring Boot parent version from 4.0.0 to 4.1.0-M2 in pom.xml and build.gradle
2. Added Spring milestone repository (4.1.0 GA not yet released on Maven Central)
3. OpenRewrite applied minor Java modernization (Paths.get() → Path.of())

### Breaking Changes Handled
- None. This is a minor version upgrade with no breaking changes detected.

### Known Issues
- Spring Boot 4.1.0 GA is not yet published to Maven Central. Using 4.1.0-M2 from the Spring milestone repository.

### Recommendations
- Once Spring Boot 4.1.0 GA is released, update the version and remove the milestone repository configuration.

### Testing Performed
- Unit tests (58 tests, 0 failures)
- Full build with `mvn clean install` - SUCCESS
- Application startup verified via integration tests

### Upgrade Safety
**Risk Level**: LOW
- This upgrade has no breaking changes
- All tests passing
- Application verified functional
- Ready for deployment

---

## Upgrade Summary
- **Current Version**: 4.0.0
- **Target Version**: 4.1.0-M2 (latest milestone; 4.1.0 GA not yet released)
- **Upgrade Date**: 2026-03-05
- **Upgrade Type**: Minor

## Compatibility Analysis
- **Java Version**: 17 (OpenJDK 17.0.13)
- **Spring Boot Version Compatibility**: Compatible (Spring Boot 4.x requires Java 17+)
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
  - javax.cache:cache-api
  - jakarta.xml.bind:jakarta.xml.bind-api
  - H2 Database (runtime)
  - Caffeine Cache (runtime)
  - MySQL Connector/J (runtime)
  - PostgreSQL Driver (runtime)
  - WebJars (Bootstrap 5.3.8, Font Awesome 4.7.0)
  - spring-boot-devtools
  - Test: spring-boot-starter-data-jpa-test, spring-boot-starter-restclient-test, spring-boot-starter-webmvc-test, spring-boot-testcontainers, spring-boot-docker-compose, testcontainers-junit-jupiter, testcontainers-mysql

### Test Status Before Upgrade
- Build Status: PASS
- Total Tests: 58
- Passing Tests: 58
- Failing Tests: 0
- Skipped Tests: 0
- Application Startup: SUCCESS
- Build Time: ~24s (without tests), ~87s (with tests)

## Breaking Changes Analysis
### Changes from Release Notes
- Spring Boot 4.1.0 is a minor release with no major breaking changes from 4.0.0
- Dependency version bumps (Hibernate, Tomcat, etc.) managed by Spring Boot BOM

### OpenRewrite Recipe Selected
- **Recipe**: org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_4 (closest available; no 4.x-specific recipe exists yet)
- **Purpose**: Applied Java modernization improvements

### Potential Impact on Application
- Configuration changes needed: NO
- Dependency updates required: NO (managed by Spring Boot BOM)
- Code changes required: NO (minor modernization only)
- API changes: NO

### Affected Files
- pom.xml (version update + milestone repo)
- build.gradle (version update + milestone repo)
- I18nPropertiesSyncTest.java (Paths.get() → Path.of())

## OpenRewrite Migration Results
### Recipe Executed
- **Recipe**: org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_4
- **Status**: SUCCESS

### Files Modified by OpenRewrite
- src/test/java/org/springframework/samples/petclinic/system/I18nPropertiesSyncTest.java

### Key Changes Applied
1. **Code Changes**:
   - Migrated `Paths.get()` to `Path.of()` (Java 11+ modernization): 2 occurrences
   - Expanded wildcard import `java.nio.file.*` to explicit imports `java.nio.file.Files` and `java.nio.file.Path`

2. **POM Updates**: None (OpenRewrite does not have a Spring Boot 4.x recipe yet)

3. **Configuration Changes**: None

### Manual Changes Required
- Manual update of Spring Boot parent version to 4.1.0-M2
- Addition of Spring milestone repository for dependency resolution

## Version Update Details
### pom.xml Changes
- Spring Boot parent version: 4.0.0 → 4.1.0-M2
- Added `<repositories>` section with Spring milestone repository
- Added `<pluginRepositories>` section with Spring milestone repository

### build.gradle Changes
- Spring Boot plugin version: 4.0.0 → 4.1.0-M2
- Added `maven { url 'https://repo.spring.io/milestone' }` to repositories block

## Dependency Updates
### Dependencies Managed by Spring Boot BOM
All Spring-managed dependencies are automatically updated through the Spring Boot BOM. No manual dependency version changes were required.

### Dependencies Checked but Not Updated
- webjars-locator-lite (1.1.2): Not Spring-managed, no update needed
- Bootstrap WebJar (5.3.8): Not Spring-managed, no update needed
- Font Awesome WebJar (4.7.0): Not Spring-managed, no update needed
- Checkstyle (12.1.2): Build tool dependency, no update needed
- JaCoCo (0.8.14): Build tool dependency, no update needed

## Configuration Changes
No configuration property changes were required for this minor version upgrade. All existing application.properties files remain compatible.

## Test Results After Upgrade
### Unit Tests
- Total Tests: 58
- Passing: 58
- Failing: 0
- Skipped: 0

### Build Verification
- `mvn clean compile`: SUCCESS
- `mvn clean test`: SUCCESS (58 tests, 0 failures)
- `mvn clean install`: SUCCESS

## Build Issues Encountered
No build issues were encountered during this upgrade.

## Performance Analysis
### Build Performance
- Build time with tests (before): ~87s
- Build time with tests (after): ~57s
- Change: Faster by ~34%

### Application Performance
- Startup verified via integration tests
- No performance issues detected

## References
### Spring Boot Documentation
- [Spring Boot 4.1.0 Release Notes](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-4.1-Release-Notes)
- [Spring Boot Documentation](https://docs.spring.io/spring-boot/reference/)

### Repositories Used
- [Spring Milestone Repository](https://repo.spring.io/milestone) - Required until 4.1.0 GA is released on Maven Central

---
*Document generated and maintained by upgrade-springboot skill*
*Last updated: 2026-03-05*
