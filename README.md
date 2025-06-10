# Jenkins Pipeline Demo

This repository contains a minimal Java application with a more detailed Jenkins
Pipeline. It shows a typical CI/CD flow using Maven and JUnit.

## Project Structure

```
.
├── Jenkinsfile           # Jenkins Pipeline definition
├── pom.xml               # Maven build file
└── src
    ├── main
    │   └── java/com/example/App.java
    └── test
        └── java/com/example/AppTest.java
```

## Jenkins Pipeline Overview

The pipeline defined in `Jenkinsfile` performs the following stages:

1. **Checkout** – pulls the source code from SCM.
2. **Build** – compiles the Java sources using Maven.
3. **Unit Test** – runs JUnit tests and publishes the results.
4. **Package** – packages the application into a JAR (tests are skipped here to speed up packaging).
5. **Archive Artifact** – archives the generated JAR in Jenkins.

Additional pipeline options include keeping the last 10 builds, preventing
concurrent runs, and timestamping the log output.

## Running Locally

To build and test the project locally, you need JDK 11 and Maven installed:

```bash
mvn clean verify
```

This will compile the application, run the tests, and package the JAR file
under `target/`.
