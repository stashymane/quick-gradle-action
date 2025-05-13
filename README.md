# Quick Gradle + Java setup action

A composite action that simply runs `actions/setup-java`, fixes `gradlew` permissions if necessary, and runs
`gradle/actions/setup-gradle`. Cache and all.

## Inputs
| Key                |   Default   | Hint                                                                                |
|--------------------|:-----------:|-------------------------------------------------------------------------------------|
| `gradle-cache-key` |             | Required for caching support.<br>[(How do I generate a key?)][encryption key hint]  |
| `jvm-version`      |    `21`     | See [Java version syntax][java version syntax]. Will roughly default to latest LTS. |
| `jvm-distribution` |  `temurin`  | See [Supported distributions][supported distributions].                             |
| `gradlew-path`     | `./gradlew` | Path to the `gradlew` executable file.                                              |

## Outputs
None.

## Example

```yml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Java & Gradle
        uses: stashymane/quick-gradle-action@main
        with:
          gradle-cache-key: ${{ secrets.GRADLE_ENCRYPTION_KEY }}

      - name: Build with Gradle
        run: ./gradlew build
```

[encryption key hint]: https://docs.gradle.org/8.6/userguide/configuration_cache.html#config_cache:secrets:configuring_encryption_key
[java version syntax]: https://github.com/actions/setup-java?tab=readme-ov-file#supported-version-syntax
[supported distributions]: https://github.com/actions/setup-java?tab=readme-ov-file#supported-distributions
