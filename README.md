# Hashtag Service

Standalone service reserved for hashtag extraction, indexing, lookup, and trend aggregation in the FAANG platform.

## Current status

This repository is an early Spring Boot scaffold. It starts as an independent service and exposes Actuator health information, but it does not yet contain a hashtag domain API, persistence, Elasticsearch integration, a Docker image, or deployment manifests.

The running platform continues to initialize `hashtags_index` through `faang-infra` and treats hashtag indexing as part of Post Service. Do not deploy this project as a service until ownership is migrated explicitly.

## Quick start

Prerequisites:

- Java 25+

Build and test:

```sh
./gradlew clean build
```

Run locally:

```sh
./gradlew bootRun
```

The service listens on `http://localhost:8084` by default. Its health endpoint is `GET /actuator/health`; override the port with `HASHTAG_SERVICE_PORT`.

## CI

[GitHub Actions](.github/workflows/ci.yml) builds and tests pushes and pull requests on `dev-local`.

## Required implementation work

- Define ownership boundaries with Post Service.
- Define the hashtag extraction, indexing, query, and trend APIs.
- Integrate Elasticsearch with explicit index mappings and migrations.
- Add unit and integration tests.
- Add configuration, a Dockerfile, and runtime health checks.
- Add Compose and Kubernetes resources only after the application is deployable.

## Repository files

- Build: [build.gradle.kts](build.gradle.kts)
- Settings: [settings.gradle.kts](settings.gradle.kts)
- Configuration: [src/main/resources/application.yaml](src/main/resources/application.yaml)
- Entry point: [HashtagServiceApplication.java](src/main/java/faang/school/hashtagservice/HashtagServiceApplication.java)
- CI: [.github/workflows/ci.yml](.github/workflows/ci.yml)

**Note:** Base code structure and architecture patterns are based on the [FAANG School](https://github.com/faang-school) educational project.
