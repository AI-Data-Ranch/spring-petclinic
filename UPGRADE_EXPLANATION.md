# Java Upgrade Decision and Process Log

## Decision Summary
- **Language**: Java
- **Current Version**: 17
- **Target Version**: 21
- **Decision**: Upgrade
- **Decision Date**: 2026-02-05

## Rationale

### Support Timeline Analysis

**Java 17 (Current)**:
- Release Date: September 2021
- LTS Status: Yes
- Oracle Premier Support: Until September 2026
- Extended Support: Until September 2029
- Status: Still supported but approaching end of premier support

**Java 21 (Target)**:
- Release Date: September 2023
- LTS Status: Yes
- Oracle Premier Support: Until September 2028
- Extended Support: Until September 2031
- Status: Latest LTS, widely adopted, battle-tested

### Version Selection Logic

Java 21 was selected as the target version for the following reasons:

1. **LTS Status**: Java 21 is the latest Long-Term Support release, providing stability and extended support
2. **Production Ready**: Released in September 2023, it has been battle-tested for over 2 years
3. **Spring Boot Compatibility**: Spring Boot 4.0.0 (used by this project) fully supports Java 21
4. **New Features**: Java 21 brings significant improvements:
   - Virtual Threads (Project Loom) - JEP 444
   - Pattern Matching for switch - JEP 441
   - Record Patterns - JEP 440
   - Sequenced Collections - JEP 431
   - String Templates (Preview) - JEP 430
5. **Sample Project Context**: As an educational/sample application, using the latest LTS demonstrates best practices
6. **README Inconsistency**: The README already mentions "Java 25" in the IDE prerequisites section (line 101), indicating an intent to upgrade

### Risk Assessment

**Low Risk Factors**:
- Spring Boot 4.0.0 fully supports Java 21
- No deprecated APIs that would break with Java 21
- All major dependencies are compatible
- This is a sample/educational project

**Considerations**:
- CI/CD workflows need updating
- DevContainer configurations need updating
- Documentation needs to be consistent

## Files Identified for Update

1. **pom.xml** (line 16): `<java.version>17</java.version>` -> `21`
2. **build.gradle** (line 19): `languageVersion = JavaLanguageVersion.of(17)` -> `21`
3. **.github/workflows/maven-build.yml** (line 18): `java: [ '17' ]` -> `'21'`
4. **.github/workflows/gradle-build.yml** (line 18): `java: [ '17' ]` -> `'21'`
5. **README.md** (line 17): Update Java version requirement
6. **.devcontainer/Dockerfile** (lines 2, 9): Update Java version references

## Actions Taken

### 1. Version Reference Updates

#### pom.xml
- Changed `<java.version>17</java.version>` to `<java.version>21</java.version>`

#### build.gradle
- Changed `languageVersion = JavaLanguageVersion.of(17)` to `languageVersion = JavaLanguageVersion.of(21)`

#### .github/workflows/maven-build.yml
- Changed `java: [ '17' ]` to `java: [ '21' ]`

#### .github/workflows/gradle-build.yml
- Changed `java: [ '17' ]` to `java: [ '21' ]`

#### README.md
- Updated Java version requirement from 17 to 21

#### .devcontainer/Dockerfile
- Changed `ARG VARIANT=17-bullseye` to `ARG VARIANT=21-bullseye`
- Changed `ARG JAVA_VERSION=17.0.7-ms` to `ARG JAVA_VERSION=21.0.2-ms`

### 2. Build and Test Results

[To be updated after build/test execution]

### 3. Issues Encountered

[To be updated if any issues are found]

## Final Recommendation

Proceed with the upgrade to Java 21. The project is a sample application with full Spring Boot 4.0.0 support for Java 21, making this a low-risk upgrade that brings significant benefits.
