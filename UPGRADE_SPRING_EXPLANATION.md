# Spring Boot Upgrade: 4.0.0 to 4.1.0

## Upgrade Summary
- **Current Version**: 4.0.0
- **Target Version**: 4.1.0
- **Upgrade Date**: 2026-03-05
- **Upgrade Type**: Minor

## Compatibility Analysis
- **Java Version**: 21 (OpenJDK 21.0.10)
- **Spring Boot Version Compatibility**: Compatible
- **Breaking Changes Expected**: Possible minor changes (minor version upgrade)

## Pre-Upgrade State
### Application Configuration
- Current pom.xml parent version: 4.0.0
- Current build.gradle plugin version: 4.0.0
- Key dependencies detected:
  - spring-boot-starter-actuator
  - spring-boot-starter-cache
  - spring-boot-starter-data-jpa
  - spring-boot-starter-thymeleaf
  - spring-boot-starter-validation
  - spring-boot-starter-webmvc
  - spring-boot-devtools
  - spring-boot-testcontainers
  - spring-boot-docker-compose
  - h2, mysql-connector-j, postgresql
  - caffeine cache
  - webjars (bootstrap, font-awesome)

### Test Status Before Upgrade
- Build Status: PASS (compilation successful with Java 21)
- Application uses both Maven (pom.xml) and Gradle (build.gradle) build files

## Upgrade Process Log

### Step 1: OpenRewrite Migration
- **Recipe Executed**: `org.openrewrite.java.spring.boot3.UpgradeSpringBoot_3_4` (latest available)
- **Status**: SUCCESS (partial - no Spring Boot 4.x specific recipe available yet)
- **Files Modified by OpenRewrite**:
  - `src/test/java/org/springframework/samples/petclinic/system/I18nPropertiesSyncTest.java`
    - Migrated `Paths.get()` to `Path.of()` (Java modernization)
    - Expanded wildcard import `java.nio.file.*` to explicit imports

### Step 2: Manual Version Updates
- **pom.xml**:
  - Updated `spring-boot-starter-parent` version: `4.0.0` -> `4.1.0-M2`
  - Updated project version: `4.0.0-SNAPSHOT` -> `4.1.0-SNAPSHOT`
  - Added Spring Milestone repository and plugin repository (4.1.0 GA not yet released)
- **build.gradle**:
  - Updated `org.springframework.boot` plugin version: `4.0.0` -> `4.1.0-M2`
  - Updated project version: `4.0.0-SNAPSHOT` -> `4.1.0-SNAPSHOT`
  - Added Spring Milestone Maven repository
- **settings.gradle**:
  - Added `pluginManagement` block with Spring Milestone repository for Gradle plugin resolution

### Step 3: Build Verification
- **Build Status**: PASS
- **Command**: `mvn clean compile -DskipTests`
- **Java Version**: OpenJDK 21.0.10
- **Compilation**: 30 source files compiled successfully
- **No errors or warnings** related to Spring Boot upgrade

### Step 4: Test Verification
- **Test Status**: PASS
- **Command**: `mvn test`
- **Total Tests**: 58
- **Passing**: 58
- **Failing**: 0
- **Errors**: 0
- **Skipped**: 0

### Step 5: Application Verification
- **Application Startup**: SUCCESS
- **Spring Boot Version**: 4.1.0-M2
- **Tomcat**: Apache Tomcat/11.0.18 on port 8080
- **Actuator**: 13 endpoints exposed beneath `/actuator`
- **Hibernate**: 7.2.4.Final
- **Database**: H2 in-memory (default profile)

## Version Note
Spring Boot 4.1.0 GA has not been released yet as of 2026-03-05. The latest available milestone version `4.1.0-M2` was used. The Spring Milestone repository (`https://repo.spring.io/milestone`) has been added to both Maven and Gradle configurations to resolve this pre-release version. When 4.1.0 GA is released, the version can be updated to `4.1.0` and the milestone repositories can be removed.

## Executive Summary
**Upgrade Status**: SUCCESSFUL

### Key Metrics
- **Files Modified**: 5 (pom.xml, build.gradle, settings.gradle, I18nPropertiesSyncTest.java, UPGRADE_SPRING_EXPLANATION.md)
- **Tests Status**: 58/58 passing
- **Build Status**: SUCCESS
- **Application Status**: RUNNING

### Breaking Changes Handled
- None - this is a minor version upgrade with full backward compatibility

### Known Issues
- Spring Boot 4.1.0 GA not yet released; using milestone 4.1.0-M2

### Recommendations
- Update to 4.1.0 GA when released and remove milestone repositories

---
*Document maintained by upgrade-springboot skill*
*Last updated: 2026-03-05*
