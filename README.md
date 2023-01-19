name: Run Android Unit Tests
on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v1

      - name: set up JDK 11
        uses: actions/setup-java@v3
        with:
          distribution: 'zulu'
          java-version: '11'

      # Execute unit tests
      - name: Unit Test
        run: ./gradlew testDebugUnitTest

      # Report the results
      - name: Android Test Report
        uses: asadmansr/android-test-report-action@v1.2.0
        if: ${{ always() }} # IMPORTANT: run Android Test Report regardless
